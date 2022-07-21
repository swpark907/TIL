map을 통해서 여러개의 useRef를 부여하고 싶을 떄가 있다.

만약

```
something.map(item =>
  <div ref={somethingRef}>
    {item}
  </div>
)
```

위와 같이 부여를 할 경우 ref는 하나에만 부여되기 때문에

가장 마지막에 생성된 item에만 ref가 부여된다.

이럴 경우 const somethingRef = useRef([]);

위 처럼 배열로 초기화를 시킨 후
```
something.map(item =>
  <div ref={somethingRef.current.push(item)}>
    {item}
  </div>
)
```
이렇게 current.push(item)를 해주면 여러개의 ref를 생성하여 useRef의 배열안에서 관리할 수 있다.
