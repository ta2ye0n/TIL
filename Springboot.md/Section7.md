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
```
