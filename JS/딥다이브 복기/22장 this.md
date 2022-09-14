this란?

자신을 참조하는 방법

아래의 객체 리터럴 같은 경우 재귀적으로 자신을 참조하는데 이런 방식은 바람직하지 않음.

```jsx
const circle = {
	radius = 5,
	getDiameter() {
		return 2 * circle.radius; // 자기 자신을 재귀적으로 참조
	}
}
```

this 바인딩은 함수 호출 방식에 따라 달라짐.

- 바인딩이란? : 식별자와 값을 연결하는 과정

객체에서의 this : 객체 그 자체

생성자 함수에서의 this : 생성될 객체 인스턴스

```jsx
console.log(this) // {} node 환경이라서 빈 객체임.

const circle = {
  radius: 2,
  getDiameter() {
    console.log(this);
    // return radius * 2; // radius is not defined
  },
};

circle.getDiameter(); // { radius: 2, getDiameter: [Function: getDiameter] }

function circle2(radius) {
  this.radius = radius;
  console.log(this);
}

circle2.prototype.getDiameter = function () {
  console.log("inner", this);
};

const Circle = new circle2(5); // circle2 { radius: 5 }
Circle.getDiameter(); // circle2 { radius: 5 }
```

1. **일반함수의 호출**
    
    **일반함수와 화살표함수는?**
    
    ```jsx
    function normalFunction() {
      console.log(this);
    }
    
    const arrowFunction = () => {
      console.log(this);
    };
    
    const Normal = new normalFunction(); // normalFunction {}
    normalFunction(); // window
    
    const Arrow = new arrowFunction(); // arrowFunction is not a constructor
    arrowFunction(); // window
    ```
    
    - 결과
        
        ![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/b33d71f7-35e9-4b9a-aeb8-e5ace8fc3e41/Untitled.png)
        
        arrowFunction은 prototype이 없으므로 constructor, 생성자 함수가 될 수 없다.
        
    - 생성자 함수에서 this바인딩과 인스턴스가 생성되는 과정
        1. 빈 객체를 생성
        2. 이 빈 객체를 this와 바인딩 시킴
        3. 생성자 함수 안의 코드를 따라 this의 인스턴스를 채워 나간다.
        4. 이 this를 반환한다.
    
    - 렉시컬 스코프(함수 상위 스코프 결정 방식), this 바인딩 시점 차이
        - 렉시컬 스코프 : 함수가 정의되는 시점
        - this 바인딩 : 함수가 호출되는 시점
    
    일반 함수의 this는 모두 전역 객체가 바인딩됨
    
    객체 내의 콜백함수도 일반함수로 호출된다면 this에 전역객체가 바인딩됨.
    
    객체 내의 중첩함수도 일반함수로 호출된다면 this에 전역객체가 바인딩됨.
    
    중첩함수, 콜백함수는 외부 함수를 돕는 헬퍼 함수로 많이 쓰이는데
    
    외부 함수의 메서드와 this가 달라져 버린다면 헬퍼함수로서의 동작하기가 매우 어려움.
    
    **그럴 때 쓰는 것이 Function.prototype.apply, call, bind .**