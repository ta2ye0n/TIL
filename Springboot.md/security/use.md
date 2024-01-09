# spring boot
---
## Security
---
### 사용하기
---
### 라이브러리 추가   
Maven 사용
```java
...
<dependency>
    <groupId>org.springframework.boot</groupId>
    <artifactId>spring-boot-starter-security</artifactId>
</dependency>
....
```
Gradle 사용
```java
dependencies{
	...
	implementation 'org.springframework.boot:spring-boot-starter-security'
}
```
버전 지정을 안하면 가장 최신의 버전 라이브러리를 가져오게 된다

스타터를 설정하면 `자동 설정` 클래스들이 동작한다
- http://localhost:8080을 입력하면 시큐리티가 만든 로그인 폼이 나오게 된다
- 계정의 비밀번호는 `콘솔에 표시`되고 아이디는 `user`이다

---
### DB에 연결하여 저장된 계정으로 로그인하기
```java
@Getter
@Setter
public class UserDetailsImpl implements UserDetails {
	
	// User 엔티티 타입의 참조변수 선언
	private User user;
	
	public UserDetailsImpl(User user) {
		this.user = user;
	}

	// User Entity가 가지고 있는 권한 목록을 저장하여 리턴한다.
	@Override
	public Collection<? extends GrantedAuthority> getAuthorities() {
		// 권한 목록을 저장할 컬렉션
		Collection<GrantedAuthority> roleList = new ArrayList<>();
		
		// 권한 설정
		roleList.add(new GrantedAuthority() {
			
			@Override
			public String getAuthority() {
				return "ROLE_" + user.getRole();
			}
		});
		
		return roleList;
	}

	@Override
	public String getPassword() {
		// {noop}은 비밀번호를 암호화하지 않도록 하는 접두사다.
		return "{noop}" + user.getPassword();
	}

	@Override
	public String getUsername() {
		return user.getUsername();
	}

	// 계정이 만료됐는지 여부를 리턴한다.
	@Override
	public boolean isAccountNonExpired() {
		return true;
	}

	// 계정이 잠겨있는지 여부를 리턴한다.
	@Override
	public boolean isAccountNonLocked() {
		return true;
	}

	// 비밀번호가 만료됐는지 여부를 리턴한다.
	@Override
	public boolean isCredentialsNonExpired() {
		return true;
	}

	// 계정의 활성화 여부를 리턴한다.
	@Override
	public boolean isEnabled() {
		return true;
	}
}
```
- `UserDetails`를 상속받아 오버라이드한 메서드를 설정아여 DB에 저장된 계정으로 로그인할 수 있다
- UserDetails는 입력받은 User객체가 `정상 로그인` 할 수 있는지 확인하는 클래스이다

> 다음 과정까지 거쳐야 로그인 할 수 있다
---
### JPA 연결
```java
@Service
public class UserDetailsServiceImpl implements UserDetailsService {

	@Autowired
	private UserRepository userRepository;
	
	@Override
	public UserDetails loadUserByUsername(String username) throws UsernameNotFoundException {
		User principal = userRepository.findByUsername(username).get();
		return new UserDetailsImpl(principal);
	}
}
```
- `UserDetailsService`를 상속받은 클래스를 활용한다
- JPA를 사용하여 DB에 저장된 User객체를 받고, 받은 User 객체를 `UserDetails를 상속받은 클래스`에 넣어주고 결과를 리턴받으면 된다

---
### Configuration 만들기
```java
@Configuration
@RequiredArgsConstructor
@EnableWebSecurity
class SecurityConfig extends WebSecurityConfigurerAdapter{

    private final MemberDetailService detailService;
    
    /**
    * Spring Security의 앞단 설정을 할수 있다.
    * debug, firewall, ignore등의 설정이 가능
    * 단 여기서 resource에 대한 모든 접근을 허용하는 설정할수도 있는데
    * 그럴경우 SpringSecuity에서 접근을 통제하는 설정은 무시해버린다.
    */
      @Override
    public void configure(WebSecurity web) throws Exception {
        web.ignoring().antMatchers("/h2-console/**");
    }
    
    /**
    * Spring Security 기능 설정을 할수 있다.
    * 특정 리소스에 접근하지 못하게 하거나 반대로 로그인, 회원가입 페이지외에 인증정보가 있어야
    * 접근할 수 있도록 설정할 수 있다.
    * 특정 리소스의 접근허용 또는 특정 권한 요구,로그인, 로그아웃, 로그인,로그아웃 성공시 Event
    * 등의 설정이 가능하다.
    */
    @Override
    protected void configure(HttpSecurity http) throws Exception {
        http.csrf().disable();
        
        // 요청에 대한 설정
        // permitAll시 해당 url에 대한 인증정보를 요구하지 않는다.
        // authenticated시 해당 url에는 인증 정보를 요구한다.(로그인 필요)
        // hasAnyRole시 해당 url에는 특정 권한 정보를 요구한다.
        // resources에 대해 접근혀용을 해야지 브라우저에서 로그인없이 js파일이나 css파일에 접근할 수 있다.
        http
                .authorizeRequests() // 요청에 대한 설정
                .antMatchers("/notice/**").permitAll() 
                .antMatchers("/main").permitAll()
                //.antMatchers("/js/**").permitAll()
                //.antMatchers("/css/**").permitAll()
                .antMatchers("/resources/**").permitAll()
                .antMatchers("/admin/**").hasAnyRole("ADMIN") 
                .anyRequest().authenticated()
                .and()
                .formLogin()
                .loginPage("/login")
                .loginProcessingUrl("/member/login")
                .defaultSuccessUrl("/main",true)
                .permitAll()
                .and()
                .logout()
                .logoutUrl("/member/logout")
                .logoutSuccessUrl("/login")
                .logoutSuccessHandler(logoutHnadler).permitAll();
    }
    
    /**
    * 사용자 인증 관련 설정
    * Custom User Detail Service를 지정하고 PasswordEncoder을 사용해서 비밀번호를 암호화 할 수 있다.
    * 참고로 비밀번호는 같은 암호화방식을 사용해서 Database에 저장해야지 인증가능하다.
    */
    @Override
    protected void configure(AuthenticationManagerBuilder auth) throws Exception {
        auth.userDetailsService(detailService).passwordEncoder(getPasswordEncoder());
    }

    @Bean
    public BCryptPasswordEncoder getPasswordEncoder(){
        return new BCryptPasswordEncoder();
    }
}
```
- fromLogin을 사용하여 login을 진행할 url을 지정하거나 login 성공시 이동 url, loginpage를 지정하거나 logout을 사용하여 로그아웃 설정을 할 수 있다