# Object.create(), class 상속

### Object.create()사용하기

```jsx
let 부모 = { name : 'Kim', age : 50 };
let 자식 = Object.create(부모);

console.log(자식.age); //50나옴
```

자식이 성공적으로 부모 속성을 상속했음

age를 바꾸고싶으면

```jsx
자식.age = 20;
console.log(자식.age) //20나옴
```

이제 자식.age는 부모로부터 상속받은 50이 나오지않을것이다 그이유는?

`특정 자료를 꺼낼때 순서가있으니까 자식이 20이 나오는것이다` 

---

### 자식으로부터 또 상속받은 손자

```jsx
var 부모 = { name : 'Kim', age : 50 };
var 자식 = Object.create(부모);
자식.age  = 20;

var 손자 = Object.create(자식);

console.log(손자.age); //20출력 
```

이렇게 계속 상속을 해주면된다.

---

### ES6 class 키워드로 구현하는 constructor문법

```jsx
class 부모 {
  constructor(){
    this.name = 'Kim';
		this.sayHi = function(){console.log('hello')}
  }
}

let 자식 = new 부모();
```

---

### 상속가능한 함수를 추가하는방법

1. constructor안 에추가하는방법
    
    ```jsx
    class 부모 {
      constructor(){
        this.name = 'Kim';
        this.sayHi = function(){ console.log('hello') }
      }
    }
    
    var 자식 = new 부모();
    ```
    
    위와같이 만들면 자식은 부모에있는 sayHi 함수를 마음껏 사용 할 수 있다.(손자 역시도)
    
2. 기계의 prototype에 추가하는 방법
    
    ```jsx
    class 부모 {
      constructor(){
        this.name = 'Kim';
      }
      sayHi(){ 
        console.log('hello') 
      }
    }
    
    let 자식 = new 부모();
    ```
    
    자식은 sayHi함수를 쓸 수 있지만 자유롭게 쓰지는못한다
    
    **`constructor`** 안에서 메서드를 정의하는 방식은 각 인스턴스가 메서드의 독립적인 복사본을 갖게 해서 더 많은 유연성과 독립성을 제공하지만, 메모리 사용량이 더 많습니다. 반면에, **`constructor`** 밖에서 메서드를 정의하는 방식은 메모리 사용을 최적화하고 일관성을 유지하지만, 모든 인스턴스가 같은 메서드를 공유하게 됩니다.
    

---

### constructor안에 파라미터추가

```jsx
class 부모 {
  constructor(이름, 나이){
    this.name = 이름;
    this.age = 나이;
  }
  sayHi(){
    console.log('안녕');
  }
  sayHello(){
    console.log('안녕하세요');
  }
}

let 자식 = new 부모('Park', 30);
```

---

### extends,super

부모유전자에서 extends로 물려받아 사용가능하며 자식이 부모의 유전자를 물려받아 사용하고싶을때 사용

```jsx
class 할아버지{
  constructor(name){
    this.성 = 'Kim';
    this.이름 = name;
  }
	sayHi(){
    console.log('안녕 나는 할아버지')
  }
}
class 아버지 extends 할아버지{
	constructor(name){
		super(name); //super에는 할아버지의 constructor안의 내용이 다들어가있다
    this.나이 = 50;
  }
	sayHi2(){
    console.log('안녕 나는 아버지');
    super.sayHi(); //할아버지에 있는 함수를 가져오고싶을때 이렇게 가져오면됨
  }
}
```

1. constructor안에 super을 사용하면 class의 constructor
2. prototype 함수 안에 쓰면 부모 class의 prototype

---

### getter , setter

오브젝트 함수내의 함수들을 괄호없이 쓸 수 있게해주는 키워드

`데이터의 무결성을 보존하기 위해 쓰는 키워드`

```jsx
let 사람 = {
  name : 'Kim',
  age : 30,
  nextAge(){
    return this.age + 1
  }
}
```

미래를 생각하면 개발자들은 내년 나이를 출력해주는 함수를 `만들어 사용` 한다. 

- 왜이렇게하는가?
    1. object안의 데이터가 복잡할수록 함수 만들어 놓는게 데이터 꺼내기 쉬움
    2. 내부에 있는 name,age 변수를 건드리지않아서 실수를 방지 할 수 있음

---

### 함수로 object나이를 수정

```jsx
let 사람 = {
  name : 'Kim',
  age : 30,
  setAge(나이){
    this.age = parseInt(나이)
  }
}
```

사람.age = 40 으로도 수정이가능하지만 `데이터 수정을 위한 함수를 만들어 사용한다` 왜냐하면 데이터가 자체가 바뀌기 때문 `사람.setAge(40)` 이렇게 쓰면 자유롭게 나이변경가능

---

### 함수 쓰기 복잡하다면 get/set키워드를 붙이자 (클래스,Object에 사용가능)

- 소괄호 써야하고 데이터 집어넣기 복잡해지므로 쓰는거임
    
    ```jsx
    let 사람 = {
      name : 'Kim',
      age : 30,
      set setAge(나이){
        this.age = parseInt(나이)
      }
    }
    
    사람.setAge = 40; //set키워드를 추가하면 이렇게 변경가능
    ```
    
    ```jsx
    let 사람 = {
      name : 'Kim',
      age : 30,
      get nextAge(){
        return  this.age + 1  
      }
    }
    
    console.log( 사람.nextAge ) //get 키워드를 추가하면 이렇게 함수를 사용가능
    ```
    
    - set함수는 `한개의 파라미터가 꼭 존재해야함`
    - get함수는 `파라미터가 있으면 안되고 함수내에 return이 있어야함`
    
    ```jsx
    class 사람 {
      constructor(){
        this.name = 'Park';
        this.age = 20;
      }
      get nextAge(){
        return this.age + 1
      }
      set setAge(나이){
        this.age = 나이;
      }
    }
    
    var 사람1 = new 사람();
    사람1.nextAge; //나이 한살추가
    사람1.setAge = 50; //50으로변경
    ```