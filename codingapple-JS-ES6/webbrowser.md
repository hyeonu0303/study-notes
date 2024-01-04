# 웹브라우저 동작원리

### 자바스크립트에서 처리가 오래걸리는 코드를만나면

서버로의 ajax요청, 이벤트리스너, setTimeout이런코드들이 처리하는데 시간이 오래걸림

이런것들은 코드가 실행될때 WebAPI에 잠시 머물러있다가 완료가 되는 시점에 Stack으로 보내짐 

ajax요청, 이벤트리스너,setTimeout 이런 코드가 실행준비가 되면

Queue로 집어넣고 Stack이 비어있을때만 차례로 넣어서 실행해줌 (Queue는 들어온순서대로)

### Stack이 바쁘면 웹사이트가 버벅거림

```jsx
for (let i = 0; i < 1e10; i++) {
  i++;
}
```

이렇게 오래걸리는 코드가있다고 해보자. 이코드는 바로 stack에서 실행되는데 계산하는데 엄청오래걸릴것이다

이런 경우 

- setTimeout을 통해 따로 빼놓고 돌아가게끔 해주는게 좋다
    
    0초마다 Queue로 보내기떄문에 그 사이사이에 사용자의 이벤트리스너 이런코드가 실행가능하게된다.
    
- Web worker사용
    
    다른 JS파일을 이용해서 그 파일에서 힘든 연산을 시키고 완료되면 값을 가져오라고 시킴
    
    ```jsx
    (메인 js 파일)
    var myWorker = new Worker('worker.js'); 
    
    w.onmessage = function(e){
      console.log(e.data) //이러면 1 나올듯
    };
    ```
    
    ```jsx
    (worker.js 파일)
    
    var i = 0;
    postMessage(i + 1); //postMessage라는 특별한 함수가 있음
    ```
    
    이러면 worker.js에서 작업이 완료될 시 postMessage()이렇게 실행하면 다른파일로 완료된 결과값을 전달해줄수있고, 이러면 Stack이 바빠지지 않는다