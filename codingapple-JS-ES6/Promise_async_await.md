# Promise / async/await

```jsx
let promise = new Promise((resolve,rejct)=>{
	resolve();
});
promise.then(()=>{
	console.log('성공');
}).catch(()=>{
	
})
```

- Promise가 콜백함수보다 좋다고 하는 이유
    1. 콜백함수와는 다르게 순차적으로 뭔가를 실행할 때 코드가 옆으로 길어지지 않음
    2. 콜백함수는 불가능한 `실패시 특정코드실행` 코드를 짤 수 있음(catch) 

```jsx
var 프로미스 = new Promise(function(성공, 실패){
  var 어려운연산 = 1 + 1;
  성공(어려운연산);
});

프로미스.then(function(결과){
  console.log('연산이 성공했습니다' + 결과)
}).catch(function(){
  console.log('실패했습니다')
});
```

---

### Promise의 몇가지 특징

1. new Promise()로 생성된 변수를 콘솔창에 출력해보면 현재 상태를 알 수 있음
    - 성공/실패 판정 전에는 <pending>
    - 성공후 <fulfilled>
    - 실패후 <rejected>
2. Promise는 동기를 비동기로 만들어주는 코드가 아니다
    - 코딩을 예쁘게 해주는 해주는 디자인 패턴임
    - Promise에 10초걸리는 연산을 시키면 10초동안 브라우저가 멈출거임
    - 비동기로 처리해주는건 오직 setTimeout,ajax,evenetListener임 `오해금지`

---

### async 키워드를 쓰면 Promise오브젝트가 저절로 생성됨

- new Promise() 할필요없음 (async (ES8))
    
    ```jsx
    async function sum(){
    	1+1
    }
    //이 함수 자체가 Promise가 됨 그러므로 then사용가능
    sum().then(()=>{
    	console.log('더하기 성공')
    })
    
    //값을 쓰고싶다면
    async function sum(){
    	return 1+1
    }
    //이 함수 자체가 Promise가 됨 그러므로 then사용가능
    sum().then((res)=>{
    	console.log(res) //2 출력
    })
    
    //then쓰기가 귀찮음
    async function sum(){
    	let calculate = new Promise((resolve,reject)=>{
    		let result = 1+ 1;
    		resolve(result);
    	})
    	let result = await calculate //calculate Promise를 기다린다음에 완료되면 결과를 변수에 담아줌
    	console.log(result);
    }
    ```