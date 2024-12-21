


Loopify 서비스에 라이브 스트리밍 기능을 추가하면서 채팅 페이지를 만들었다.
채팅 페이지로 접속할 수 있게
```js
@Controller('')  
export class ViewController {
@Get('chat/:roomId')  
  @UseGuards(AuthGuard('jwt'))  
  @Render('chat')  
  showChat(  
    @UserInfo() user: UserEntity,  
    @Param('roomId')  
    roomId: string,  
  ) {  
    return {  
      roomId,  
      user,  
    };  
  }  
}
```

이렇게 작성한 이후에 서버를 키고
브라우저의 주소창에 
localhost:3000/chat/room1을 입력해서 이동하려고 하니까

```json
{"message":"Unauthorized","statusCode":401}
```

인가 부분에서 넘어가지 않았다.


문제 원인을 계속 찾지 못하고 헤매다가 Postman을 이용해 showChat api에 요청을 보내면서
점점 원인을 좁혀 나가기 시작했다

![[Pasted image 20241213123308.png]]
postman으로 동일한 api 요청을 보내니까 status code 200으로 응답하고
채팅방 페이지를 올바르게 제공해준다

![[Pasted image 20241213124148.png]]

그래서 브라우저 환경에서 localstorage 를 확인해보니까
token이 제대로 있는걸 확인하고
token이 있는데 왜 안될까? 라고 생각하고
다른 UseGuard()를 통해 인가처리 해주는 기능들을 살펴 보면서 원인을 알게 됐다.



이 토큰을 request header에 넣어서 보내줘야 되는데 그냥 URL로 이동하면
바로 showChat 핸들러로 요청이 전송 돼서
사실상 request header에 token 값이 전달이 안되고 있는 상황이라고 추측했다

내 추측이 맞는지 확인하기 위해
새로운 커스텀 가드를 작성했다
```ts
import { CanActivate, ExecutionContext, Injectable } from '@nestjs/common';  
  
@Injectable()  
export class HeaderLoggerGuard implements CanActivate {  
  canActivate(context: ExecutionContext): boolean {  
    const request = context.switchToHttp().getRequest();  
    console.log('Request Headers:', request.headers); // 모든 헤더 출력  
    return true; // 인증 로직 추가 가능  
  }  
}
```

```ts
@Get('chat/:roomId')  
@UseGuards(HeaderLoggerGuard, AuthGuard('jwt'))  // 새로 만든 커스텀 가드 적용
@Render('chat')  
showChat(  
  @UserInfo() user: UserEntity,  
  @Param('roomId')  
  roomId: string,  
) {  
  return {  
    roomId,  
    user,  
  };  
}
```

이렇게 하고
브라우저에서 URL을 통해서 showChat 핸들러에 요청을 보내봤다

```json
Request Headers: {
  host: 'localhost:3000',
  connection: 'keep-alive',
  'sec-ch-ua': '"Google Chrome";v="131", "Chromium";v="131", "Not_A Brand";v="24"',
  'sec-ch-ua-mobile': '?0',
  'sec-ch-ua-platform': '"macOS"',
  'upgrade-insecure-requests': '1',
  'user-agent': 'Mozilla/5.0 (Macintosh; Intel Mac OS X 10_15_7) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/131.0.0.0 Safari/537.36',
  'sec-purpose': 'prefetch;prerender',
  purpose: 'prefetch',
  accept: 'text/html,application/xhtml+xml,application/xml;q=0.9,image/avif,image/webp,image/apng,*/*;q=0.8,application/signed-exchange;v=b3;q=0.7',
  'sec-fetch-site': 'none',
  'sec-fetch-mode': 'navigate',
  'sec-fetch-user': '?1',
  'sec-fetch-dest': 'document',
  'accept-encoding': 'gzip, deflate, br, zstd',
  'accept-language': 'ko-KR,ko;q=0.9,en-US;q=0.8,en;q=0.7',
  cookie: 'Webstorm-e82104a9=f434c5e7-7311-4d22-90d0-b1e9dc4857b5',
  'if-none-match': 'W/"85e-lbLGPHswLpWGC83C4O3XKuV/EB8"'
}
```

들어온 request header을 보면
Authorization 이라는 부분이 없는것을 확인할 수 있다.

그리고
내가 웹페이지에서 버튼을 만들어서
요청을 보내봤다

```js
const chatBtn = document.getElementById('chatBtn');  
chatBtn.addEventListener('click', async () => {  
  const roomId = 'room1'; // 방 ID 설정  
  const token = localStorage.getItem('token'); // 로컬 스토리지에서 JWT 가져오기  
  
  if (!token) {  
    alert('로그인이 필요합니다.');  
    window.location.href = '/login';  
    return;  }  
  
  const response = await fetch(`/chat/${roomId}`, {  
    method: 'GET',  
    headers: {  
      Authorization: `Bearer ${token}`, // 헤더에 JWT 추가  
    },  
  });  
  
  if (response.ok) {  
    const html = await response.text();  
    document.open();  
    document.write(html);  
    document.close();  
  } else {  
    alert('접속 권한이 없습니다.');  
  }  
});
```

이렇게 버튼을 만들고

이 버튼을 통해서 request를 보냈다

```js
Request Headers: {
  host: 'localhost:3000',
  connection: 'keep-alive',
  'sec-ch-ua-platform': '"macOS"',
  authorization: 'Bearer eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJpZCI6OSwiZW1haWwiOiJjaG9pMTYyODlAbmF2ZXIuY29tIiwibmFtZSI6Iuy1nOqwle2YhCIsIm5pY2tuYW1lIjoiTnRlcjk5IiwiaXNTb2NpYWwiOmZhbHNlLCJpYXQiOjE3MzQwNjEwNzF9.bGJHn2fmciQvu-ivh1RZYgPpBXDVLd4dIz0loW0LtHc',
  'user-agent': 'Mozilla/5.0 (Macintosh; Intel Mac OS X 10_15_7) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/131.0.0.0 Safari/537.36',
  'sec-ch-ua': '"Google Chrome";v="131", "Chromium";v="131", "Not_A Brand";v="24"',
  'sec-ch-ua-mobile': '?0',
  accept: '*/*',
  'sec-fetch-site': 'same-origin',
  'sec-fetch-mode': 'cors',
  'sec-fetch-dest': 'empty',
  referer: 'http://localhost:3000/myChannel',
  'accept-encoding': 'gzip, deflate, br, zstd',
  'accept-language': 'ko-KR,ko;q=0.9,en-US;q=0.8,en;q=0.7',
  cookie: 'Webstorm-e82104a9=f434c5e7-7311-4d22-90d0-b1e9dc4857b5',
  'if-none-match': 'W/"85e-lbLGPHswLpWGC83C4O3XKuV/EB8"'
}
```


당연하게도 헤더에 authorization 이라는 키 값이 생긴걸 볼 수 있다

jwt 토큰 값을 넣어서 보내주고 있으니까

![[Pasted image 20241213140804.png]]

채팅창도 정상적으로 접속된다.



