# Reference data type

### Primitive data type

- 변수에 저장되는 자료들
    
    ```jsx
    var name = 'john';
    var age = 20
    ```
    

### Reference data type(참조데이터타입)

- Array,Object 자료형이 참조데이터 타입이다
    
    ```jsx
    var person = {name:'kim'}
    var person1 = {name: 'park'}
    
    //
    person1 == person //두개는 다른 화살표이므로 같지가 않다
    ```
    
- 복사
    
    ```jsx
    let 이름1 = {name : '김'}
    let 이름2 = 이름1
    이름1.name = '박'
    
    console.log(이름1) //박
    console.log(이름2) //박
    ```
    
    위와같이 이름 2에는 할당을 안해줬는데 바뀌는것을 볼 수 있다 왜냐하면 같은 화살표로 메모리에 있는 객체에 참조하고 있기때문이다.
    
- 함수를 이용해 object를 변경하면 어떻게 될까?
    
    ```jsx
    let 이름1 = {name:'김'}
    
    function 변경(obj){
    	obj = {name : 'park'}
    }
    
    변경(이름1) //{name:'김'} 출력
    
    //(자바스크립트의 시점)
    var 이름1 = { name : '김' };
    function 변경(obj){
      obj = { name : 'park' };
    }
    변경(var obj = 이름1);
    ```
    
    - 왜 이런 현상이 발생할까?
        
        이게 발생하는이유는 함수 파라미터에있는 obj는 새로운 변수를 생성하는 개념이다
        
        그러므로 obj역시 다른 화살표를 만들기때문에 `obj ⇒ {name:’park’}`
        
        `이름1 ⇒ {name:’김’}` 이렇게 되기때문에 함수를 이용해 변경할 수 없다.