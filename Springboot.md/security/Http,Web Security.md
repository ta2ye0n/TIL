# Spring
---
## Spring Security
---
### HttpSecurity
```java
Ex) 

@Bean
    public SecurityFilterChain filterChain(HttpSecurity http) throws Exception {
        http
                .authorizeRequests()
                .antMatchers("/user").hasRole("USER")
                .antMatchers("/manager").hasRole("MANAGER")
                .anyRequest().authenticated()

        .and()
                .formLogin();
        return http.build();
    }
```
antMatchers의 endPoint에 대한 `인증을 무시`한다

-> `취약점에 대한 보안`이 필요할 때 사용한다

---
### WebSecurity
```java
Ex)

@Bean
    public WebSecurityCustomizer webSecurityCustomizer(){
        return (web) ->{
            web.ignoring().requestMatchers(PathRequest.toStaticResources().atCommonLocations());
            web.ignoring().antMatchers("/favicon.ico", "/resources/**", "/error");
        };
    }
```
`antMatchers`의 endPoint에 대한 Spring Security Filter Chain을 거치지 않기 때문에 `인증과 인가를 거치지 않는다`
`Security Context`를 설정하지 않고, `Security Features(Secure headers, CSRF protecting 등)`가 사용되지 않는다
Cross-Site-Scriptin(XSS), content-sniffing에 대한 `endPoints 보호`가 제공되지 않는다

->인증, 인가 서비스가 필요하지 않은 `정적 자원`("/favicon.ico", "/resources/**", "/error") 이나 `로그인 페이지, public 페이지`에 사용한다

---
### WebSecurity vs HttpSecurity
HttpSecurity 보다 WebSecurity가 `우선적으로 고려`된다

만약 WebSecurity, HttpSecurity에 모두 설정을 한 경우 HttpSecurity에 인가 설정은 `무시`된다
```java
Ex)

@Override
public void configure(WebSecurity web) throws Exception {
    web
        .ignoring()
        .antMatchers("/publics/**");
}

@Override
protected void configure(HttpSecurity http) throws Exception {
    http
        .authorizeRequests()
        .antMatchers("/admin/**").hasRole("ADMIN")
        .antMatchers("/publics/**").hasRole("USER") // no effect
        .anyRequest().authenticated();
}
```