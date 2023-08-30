# Spring boot
---
## 회원 관리 예제 - 웹 MVC 개발
---
### 회원 웹 기능 - 홈화면 추가   
홈 컨트롤러 추가    
``` java
package hello.hellosping.controller;

import org.springframework.stereotype.Controller;
import org.springframework.web.bind.annotation.GetMapping;

@Controller
public class HomeController {

    @GetMapping("/")
    public String home(){
        return "home";
    }
}
```

회원 관리용 홈   
``` html   
<!DOCTYPE html>
<html xmlns:th="http://www.thymeleaf.org">
<body>

<div class="container">
  <div>
    <h1>Hello Spring</h1>
    <p>회원기능</p>
    <p>
      <a href="/members/new">회원가입</a>
      <a href="/members">회원 목록</a>
    </p>
  </div>
</div><!-- /container -->

</body>
</html>
```
> 참고 : 컨트롤러가 정적 파일보다 우선순위가 높다.   
---
### 회원 웹 기능 - 등록   
**회원 등록 폼 개발**   

회원 등록 폼 컨트롤러   
``` java   
@Controller
public class MemberController {

    private final MemberService memberService;

    @Autowired
    public MemberController(MemberService memberService){
        this.memberService = memberService;
    }

    @GetMapping("/members/new")
    public String createForm() {
        return "members/createMemberForm";
    }
}
```

회원 등록 폼 HTML`(resources/templates/members/creatdMemberform)`   
``` html
<!DOCTYPE html>
<html xmlns:th="http://www.thymeleaf.org">
<body>

<div class="container">

  <from action="/members/new" method="post">
    <div class="form-group">
      <lavel for="name">이름</lavel>
      <input type="text" id="name" name="name" placeholder="이름을 입력하세요">
    </div>
    <button type="submit">등록</button>
  </from>

</div> <!--- /container --->

</body>
</html>
```   
---
### 회원 웹 기능 - 조회   

회원 컨트롤러에서 조회 가능   
``` java
@GetMapping("/members")
    public String list(Model model) {
        List<Member> members = memberService.findMembers();
        model.addAttribute("members",members);
        return "members/memberList";
    }
```   

회원 리스트 HTML   
``` html
<!DOCTYPE html>
<html xmlns:th="http://www.thymeleaf.org">
<body>

<div class="container">
  <div>
    <table>
      <thead>
      <tr>
        <th>#</th>
        <th>이름</th>
      </tr>
      </thead>
      <tbody>
      <tr th:each="member : ${members}">
        <td th:text="${member.id"></td>
        <td th:text="${member.name}"></td>
      </tr>
      </tbody>
    </table>
  </div>

</div> <!--- /container --->

</body>
</html>
```
---