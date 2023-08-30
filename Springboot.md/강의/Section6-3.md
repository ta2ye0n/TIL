# Spring boot
---
## 스프링 DB 접근 기술
---
### 스프링 데이터 JPA
스프링 부트와 JPA만 사용해도 개발 생산성이 정말 많이 증가하고, 개발해야할 코드도 확연히 줄어듭니다 여기에 스프링 데이터 JPA를 사용하면 기존의 한계를 넘어 마치 마법처럼, 리포지토리에 구현 클래스 없이 인터페이스 만으로 개발을 완료할 수 있습니다 그리고 반복 개발해온 기본 CRUD 기능도 스프링 데이터 JPA가 모두 제공합니다
실무에서 관계형 데이터베이스를 사용한다면 스프링 데이터 JPA는 이제 선택이 아니라 필수입니다
> 주의: 스프링 데이터 JPA는 JPA를 편리하게 사용하도록 도와주는 기술입니다 따라서 JPA를 먼저 학습한 후에 스프링 데이터 JPA를 학습해야 합니다   
- 앞의 JPA 설정을 그래도 사용한다   

**스프링 데이터 JPA 회원 리포지토리**   
``` java
package hello.hellosping.repository;

import hello.hellosping.domain.Member;
import org.springframework.data.jpa.repository.JpaRepository;

import java.util.Optional;

public interface SpringDataJpaMemberRepository extends JpaRepository<Member, Long>, MemberRepository{
    @Override
    Optional<Member> findByName(String name);
}
```

**스프링 데이터 JPA회원 리포지토리를 사용하도록 스프링 설정 변경**   
``` java
package hello.hellosping.service;

import hello.hellosping.repository.MemberRepository;
import org.springframework.beans.factory.annotation.Autowired;
import org.springframework.context.annotation.Bean;
import org.springframework.context.annotation.Configuration;

@Configuration
public class SpringConfig {

    private final MemberRepository memberRepository;

    @Autowired
    public SpringConfig(MemberRepository memberRepository) {
        this.memberRepository = memberRepository;
    }

    @Bean
    public MemberService memberService() {
        return new MemberService(memberRepository);}
}
```
- 스프링 데이터 JPA가 `SpringDataJpaMemberRepository`를 스프링 빈으로 자동 등록해준다   

**스프링 데이터 JPA 제공 클래스**   
![](https://www.notion.so/image/https%3A%2F%2Fs3-us-west-2.amazonaws.com%2Fsecure.notion-static.com%2F7e749f29-3d6d-4437-a1ce-a622bbe272b7%2FUntitled.png?table=block&id=9b4e26e7-9a7d-44d5-bb76-01e1d90d64f1&spaceId=b453bd85-cb15-44b5-bf2e-580aeda8074e&width=2000&userId=80352c12-65a4-4562-9a36-2179ed0dfffb&cache=v2)

**스프링 데이터 JPA 제공 기능**   
- 인터페이스를 통한 기본적이 CRUD   
- `findByName()`,`findByEmail()` 처럼 메서드 이름 만으로 조회 기능 제공   
- 페이징 기능 자동 제공   

> 참고 : 실무에서는 JPA와 스프링 데이터 JPA를 기본으로 사용하고, 복잡한 동적 쿼리는 Querdsl이라는 라이브러리를 사용하면 된다 Querydsl을 사용하면 쿼리도 자바 코드로 안전하게 작성할 수 있고, 동적 쿼리도 편리하게 작성할 수 있다. 이 조합으로 해결하기 어려운 쿼리는 JPA가 제공하는 네이티브 쿼리를 사용하거나, 앞서 학습한 스프링 JdbdTemplate를 사용하면 된다.