---
tags:
  - 내일배움캠프
---

### HTTP 통신에서 쿠키가 필요한 이유

HTTP 통신은 Stateless 하기 때문에 
* stateless 하다는 각 요청이 독립적이라는 뜻으로 클라이언트의 상태를 서버가 기억하지 않는다는 뜻
로그인 정보를 유지하려면 쿠키 같이 로그인 정보를 저장한것이 필요 서버를 통해 쿠키를 받고 이 쿠키를 웹 브라우저가 갖고 있는다 그리고 이제 요청을 보낼 때 쿠키를 함께 보내 내가 로그인한 사용자라는것을 서버에 알려준다

### http 헤더

헤더를 3부분으로 나눌 수 있음
general header, request / response header , entity header

내가 알고자 했던 Authorization과 cookie는 request header에 있음

> Authorization
> 인증 방법에는 다양한 방법이 존재해서 각 방식마다 Authorization에 들어가는 value값이 다르다.
> 각 인증마다 적절한 value를 넣어줘야함


varchar vs text 의 차이는 값의 참조 여부
참조X           참조 O

Document.db는 한번에 다 때려넣을 수 있다.

objectId