## SSR
Server Side Rendering 의 약자
서버로부터 완전히 만들어진 html 파일을 받아와 페이지 전체에 랜더링 하는 방식.

1. 서버에 요청을 보낸다
2. Server는 'Ready to Render'. 즉, 즉시 렌더링 가능한 html파일을 만든다.
3. 클라이언트에 전달되는 순간, 이미 렌더링 준비가 되어있기 때문에 HTML은 즉시 렌더링 된다. 그러나 사이트 자체는 조작 불가능하다. (Javascript가 읽히기 전이다.)
4. 클라이언트가 자바스크립트를 다운받는다.
5. 다운 받아지고 있는 사이에 유저는 컨텐츠는 볼 수 있지만 사이트를 조작 할 수는 없다. 이때의 사용자 조작을 기억하고 있는다.
6. 브라우저가 Javascript 프레임워크를 실행한다.
7. JS까지 성공적으로 컴파일 되었기 때문에 기억하고 있던 사용자 조작이 실행되고 이제 웹 페이지는 상호작용 가능해진다.

## CSR

1. User가 Website 요청을 보냄.
2. CDN이 HTML 파일과 JS로 접근할 수 있는 링크를 클라이언트로 보낸다.
CDN : aws의 cloudflare를 생각하면 됨. 엔드 유저의 요청에 '물리적'으로 가까운 서버에서 요청에 응답하는 방식

3. 클라이언트는 HTML과 JS를 다운로드 받는다.
(이때 SSR과 달리 유저는 아무것도 볼 수 없다.)
생략
4. 다운이 완료된 JS가 실행된다. 데이터를 위한 API가 호출된다.
(이때 유저들은 placeholder를 보게된다. )
5. 서버가 API로부터의 요청에 응답한다.
6. API로부터 받아온 data를 placeholder 자리에 넣어준다. 이제 페이지는 상호작용이 가능해진다.
