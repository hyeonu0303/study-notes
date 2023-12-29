# 변수(var let const Hoisting)

### var let const 차이

- var
    
    재선언 O ,재할당 O,범위 function(){}
    
- let
    
    재선언 O, 재할당 X, 범위 {}
    
- const
    
    재선언 X, 재할당 X, 범위 {}
    

- 예외
    
    const변수에 object를 담으면 object내의 데이터는 변경가능
    
    ```jsx
    const obj = {name : 'kim'}
    obj.name = 'Park'
    ```
    
    이유: obj에 재할당한게 아니므로 변경이된다 이럴때는 
    
    ```jsx
    Object.freeze(obj)
    ```
    
    이렇게 하면 변경이 절대 불가능해진다.
    

---

### 변수의 범위

- var
    
    var의 범위는 function이다
    
    ```jsx
    function 함수(){
      var 이름 = 'Kim';
      console.log(이름); //가능
    }
    
    console.log(이름); //에러
    ```
    
- let
    
    let의 범위는 {}
    
    ```jsx
    if ( 1 == 1 ){
      let 이름 = 'Kim';
      console.log(이름); //가능
    }
    
    console.log(이름); //에러
    ```
    

---

### Hoisting

- 호이스팅현상은 자바스크립트에서 함수, 변수등 먼저 함수의 선언부분을 평가단계에서 먼저 선언
    
    이러면 undefined로 먼저 정의된다.
    
    ```jsx
    let 이름 = 'kim'; //선언
    -----------------------
    let 이름; //hoisting현상
    이름 = 'kim' 
    -----------------------
    함수() //실행됨 'hello'출력
    function 함수(){ //함수도 hoisting현상으로 평가단계에서 먼저 선언됨
    	conosle.log('hello');
    }
    ```
    

---

### 전역변수

- 전역변수는 가능하다면 안만드는게 좋다 하지만 만들어야한다면
    
    ```jsx
    window.나이 = 20;
    ```
    
    이런식으로 만들어 사용하는게 좋다
    

---

### 연습문제

- 연습문제
    
    1번
    
    ```jsx
    함수();
    function 함수(){
    	console.log(안녕);
    	let 안녕 = 'hello';
    }
    ```
    
    let변수는 undefined를 자동으로 할당해주지않음 그래서 에러남
    
    2번
    
    ```jsx
    함수();
    var 함수 = function (){
    	console.log(안녕);
    	var 안녕 = 'Hello';
    }
    ```
    
    3번
    
    ```jsx
    let a = 1;
    var 함수 = function(){
    	a = 2;
    }
    console.log(a);
    ```
    
    4번
    
    ```jsx
    let a = 1;
    var b = 2;
    window.a = 3;
    window.b = 4;
    
    console.log(a+b);
    ```
    
    5번
    
    ```jsx
    for(var i = 1; i < 6; i++){
    	setTimeout(function(){console.log(i);},i*1000);
    }
    ```
    