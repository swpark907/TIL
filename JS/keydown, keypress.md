- keydown -> keypress -> keyup 순으로 이벤트가 일어난다.

- keypress는 먹히는 key가 제한적이다. 

- keypress가 활성화 되는 key

  - 영문

  - 숫자

  - Enter

  - Space

- keydown과 keyup은 실행 되었을 때 한번만 이벤트가 발생하는데 반해
keypress는 누르고 있으면 지속적으로 실행된다.

- 예를들어 space를 쭉 누르고 있는 경우
keydown 1번 실행 -> keypress 여러번 실행 -> keyup 1번 실행 순으로 된다.