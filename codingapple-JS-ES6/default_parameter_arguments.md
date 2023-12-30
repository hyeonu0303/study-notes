# default parameter/arguments

### 함수의 default 파라미터 넣기

- 함수를 만들때 default 파라미터를 넣어줄 수 있음
    
    ```jsx
    function sum (a,b = 10) {
    	console.log(a+b);
    }
    sum(1);
    ```
    
- 함수도 가능
    
    ```jsx
    function 임시함수(){
    	return 10
    }
    
    function sum (a,b = 임시함수()){
    	console.log(a + b)
    }
    sum(3);
    ```
    

---

### 함수의 arguments

- 함수의 모든 파라미터들을 전부 한꺼번에 다룰 수 있음
    
    ```jsx
    function func(a,b,c){
    	console.log(arguments);
    }
    
    func(2,3,4); //[2,3,4] 출력
    
    //반복문사용시
    function func(a,b,c){
    	for(let i = 0; i < arguments.length; i++)
    		console.log(arguments[i])
    }
    ```
    

---

### Rest 파라미터

- …기호로 파라미터 들을 배열에 담아줌
    
    ```jsx
    function restFunc(...rest){
    	console.log(rest) // [1,2,3,4,5,6,7]
    }
    
    restFunc(1,2,3,4,5,6,7)
    
    //이렇게 사용하면 앞에 두개 빼고 나머지를 배열로 감싸줌
    function restFunc(a,b,...rest){
    	console.log(rest) // [3,4,5,6,7]
    }
    
    restFunc(1,2,3,4,5,6,7)
    ```
    
- 연습문제
    
    ```jsx
    /*
    데이터분석 하는 사람들이 자주 만들어 쓰는 함수가 있습니다. 
    
    알파벳들의 출현 갯수를 세어주는 함수입니다. 우리도 한번 만들어봅시다. 
    
     
    
    글자세기('aacbbb') 라고 입력하면 콘솔창에
    
    { a : 2, b : 3, c : 1 }
    
    ▲ 이렇게 출력해주는 글자세기() 라는 함수를 만들고 싶습니다.
    
    쉽게말하자면 입력한단어에 들어있는 알파벳의 갯수를 세어서 오브젝트에 기록해주고 출력까지 해주는 함수입니다. 
    
    글자세기라는 함수를 어떻게 만들면 될까요?
    
    */
    const 글자세기 = (char) => {
      let arr = [...char];
      console.log(arr);
      let obj = {};
      arr.forEach((el,idx)=>{
          
        //객체에 []표기법을 사용하면 obj.el이지만 []를 사용하면 변수를 키로 사용할수있게 된다.
        //즉, el이 'a'라면 obj['a']와 같게 된다. 그러면 'a'속성에 접근이가능하다.
        console.log(obj[el])
        if(obj[el] > 0)
          obj[el] = obj[el] + 1;
        else
          obj[el] = 1;
        })
    
        console.log(obj);
         //같은문자찾아서 object에 담아주면됨
    }
    
    ```