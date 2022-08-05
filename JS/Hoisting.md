## Hoisting
### 호이스팅이란?
자바스크립트는 한 줄씩 순차적으로 코드를 실행하는 **런타임** 시점에 앞서 그 이전의 단계에서 변수선언이 실행됨. -> 자바스크립트가 실행될 때 필요한 변수값들을 모두 모아 **유효범위의 최상단**으로 끌어올림. 이를 호이스팅이라 한다.

- let/const 뿐만 아니라 function, class 키워드를 사용해서 선언하는 모든 식별자도 호이스팅이 일어난다. 하지만 TDZ (Temporal Dead Zone)에 의해 제약을 받는다.

### var
ES5까지 변수를 선언할 수 있는 유일한 방법.
중복선언이 가능하여 오류를 발생시킬 여지가 있음.
```
var i = 1;

for(var i = 0; i < 5; i++){
  console.log(i) // 0,1,2,3,4
}

console.log(i) // 5
```
위 코드처럼 i가 원치않게 변해버림. 또한
```
console.log(foo) // undefined 선언 및 초기화

var foo;
console.log(foo) // undefined

foo = 1;
console.log(foo) // 1
```
이처럼 선언단계에서 변수의 존재를 알리고 그 즉시 undefined로 초기화시킨다.

따라서 스코프에 변수가 존재하기 때문에 오류가 나지 않는다.

### let
- ES6에서 나온 문법으로 중복선언이 금지된다.

```
let bar = 234;
let bar = 456; // SyntaxError: Identifier 'bar' has already been declared
```
- 함수레벨 스코프를 따르는 var와 달리 블록레벨 스코프를 따른다.
- 선언단계와 초기화 단계가 분리되어 진행된다. 암묵적으로 선언단계가 먼저 실행되지만 초기화 단계는 변수 선언문에 도달했을 때 실행된다.
```
let foo = 1; // 전역변수
{
  console.log(foo); // ReferenceEroor: Cannot access 'foo' before initialization;
  let foo = 2; // 지역변수
}
```
호이스팅이 일어나지 않는다면 console.log에서 전역변수인 1을 출력할텐데

호이스팅이 일어나기 때문에
블록 안에서 foo가 일단 선언되고 console은 그 foo의 선언때문에 에러를 발생시킨다. 초기화되지 않아서.
따라서 호이스팅은 일어나나 일어나지 않는 것처럼 작동한다.