# Spring boot
---
## AOP
---
### AOP가 필요한 상황
- 모든 메소드의 호출 시간을 측정하고 싶다면?   
- 공통 관심 사항(cross-cutting concern) vs 핵심 관심 사항(core concern)   
- 회원 가입 시간, 회원 조회 시간을 측정하고 싶다면?      
![](https://encrypted-tbn0.gstatic.com/images?q=tbn:ANd9GcRp26ymT8i31QKyWhR6v5cw_KdDMcx-JAFkxYhJOgcf1PhUNRM1L_AraM7xgP9GOs-fRsk&usqp=CAU)   

**MemberService 회원 조회 시간 측정 추가**   
``` java
package hello.hellosping.service;

@Transactional
public class MemberService {

    private final MemberRepository memberRepository;

    @Autowired
    public MemberService(MemberRepository memberRepository) {
        this.memberRepository = memberRepository;
    }

    // 회원가입
    public Long join(Member member){

        long start = System.currentTimeMillis();

        try {
            // 같은 이름이 있는 중복 회원 X
            validateDuplicateMember(member); // 중복 회원 검증
            memberRepository.save(member);
            return member.getId();
        } finally {
            long finish = System.currentTimeMillis();
            long timeMs = finish -start;
            System.out.println("join = " + timeMs + "ms");
        }
    }

    private void validateDuplicateMember(Member member){
        memberRepository.findByName(member.getName()).ifPresent(member1 -> {
                    throw new IllegalStateException("이미 존재하는 회원입니다.");
                });
    }

    // 전체 회원 조회
    public List<Member> findMembers() {
        long start = System.currentTimeMillis();
        try {
            return memberRepository.findAll();
        } finally {
            long finish = System.currentTimeMillis();
            long timeMs = finish - start;
            System.out.println("findMembers " + timeMs + "ms");
        }
    }
}
```

**문제**   
- 회원가입, 회원조회에 시간을 측정하는 기능은 핵심 관심 사항이 아니다
- 시간을 측정하는 로직은 공통 관심 사항이다   
- 시간을 측정하는 로직과 핵심 비즈니스의 로직이 섞여서 유지보수가 어렵다   
- 시간ㅇ르 측하는 로직을 별도의 공통 로직으로 만들기 매우 어렵다   
- 시간을 측정하는 로직을 변경할 때 모든 로직을 찾아가면서 변경해야 한다   
---
### AOP 적용
- AOP : Aspect Oriented Programming   
- 공통 관심 사항(cross-cutting concern) vs 핵심 관심 사항(core concern) 분리   
![](https://images.velog.io/images/rladuswl/post/e19f44a4-fb53-45a2-a409-d35521942a9a/%EC%BA%A1%EC%B2%98.JPG)

**시간 측정 AOP 등록**   
``` java
package hello.hellosping.aop;

import org.aspectj.lang.ProceedingJoinPoint;
import org.aspectj.lang.annotation.Around;
import org.aspectj.lang.annotation.Aspect;
import org.springframework.stereotype.Component;

@Aspect
@Component
public class TimeTraceAop {

    @Around("execution(* hello.hellospring..*(..))")
    public Object execute(ProceedingJoinPoint joinPoint) throws Throwable {
        long start = System.currentTimeMillis();
        System.out.println("START: " + joinPoint.toString());
        try {
            return joinPoint.proceed();
        } finally {
            long finish = System.currentTimeMillis();
            long timeMs = finish - start;
            System.out.println("END: " + joinPoint.toString() + " "+ timeMs + "ms");
        }
    }
}
```
**해결**   
- 회원가입, 회원 조회등 핵심 관심사항과 시간을 측정하는 공통 관심 사항을 분리한다   
- 시간을 측정하는 로직을 별도의 공동 로직으로 만들었다   
- 핵심 관심사항을 깔끔하게 유지할 수 있다   
- 변경이 필요하면 이 로직만 변경하면 된다   
- 원하는 적용 대상을 선택할 수 있다   

#### 스프링의 AOP 동작 방식 설명

**AOP 적용 전 의존관계**   
![](https://velog.velcdn.com/images/z00m__in/post/2e980169-0a75-425c-af8b-f401c35365f6/image.PNG)   

**AOP 적용 후 의존관계**   
![](https://velog.velcdn.com/images/ghenmaru/post/151aceda-f145-45df-8330-e9de8110a2b6/image.png)

**AOP 적용 전 전체 그림**   
![](https://velog.velcdn.com/images%2Fsorzzzzy%2Fpost%2Ff64a4a68-8871-45a2-b459-831a57c17090%2F%E1%84%89%E1%85%B3%E1%84%8F%E1%85%B3%E1%84%85%E1%85%B5%E1%86%AB%E1%84%89%E1%85%A3%E1%86%BA%202021-08-16%20%E1%84%8B%E1%85%A9%E1%84%8C%E1%85%A5%E1%86%AB%201.23.10.png)   

**AOP 적용 후 전체 그림**   
![](https://velog.velcdn.com/images/z00m__in/post/25c40b55-495f-430a-b662-9006a7a862cc/image.PNG)   

- 실제 Proxy가 주입되는지 콘솔에 출력해서 확인하기
