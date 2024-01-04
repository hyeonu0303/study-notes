# async/sync & callback

### 자바스크립트는 항상 동기식처리를 한다 (synchronous)

동기식처리란 한번에 코드 `한줄씩 차례차례 실행되는것을 의미` 

```jsx
console.log(1);
console.log(2);
console.log(3);
//1,2,3한줄 씩 실행 동기적임
```

```jsx
console.log(1);
setTimeout(function(){console.log(2)}, 1000);
console.log(3);
```

이코드를 보면 1,3이 출력되고 1초후에 setTimeout이 나온다 왜이러냐면

`특수한 코드들을 발견하면 약간 제쳐두고 다른 코드부터 실행` 하려고하기때문이다.

이러한 처리방식을 `비동기(asyncronous)` 라고 한다 

### 비동기적으로 실행하는 함수들

`setTimout`, `addEventLinstener`, `ajax` 

크롬은 이런 특별한 코드들을 만나면 잠깐대기실에 두고 준비가 완료되면 다시 실행시킴

⇒ 이래서 재랜더링을 안하고 바로 바뀌는거임