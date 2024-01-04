# Prototype

### Prototype은 유전자 역할을 해주는 비밀공간이다

```jsx
function 기계(){
	this.name = 'kim';
  this.age = 15;
}

let 학생1 = new 기계();
let 학생2 = new 기게();

console.log(기계.prototype);

기계.prototype.gender = '남'

cosnole.log(학생1.gender); //'남'이 출력됨
```

기계 즉, 부모의 유전자에 `{gender,’남’}` 을 저장해줌으로써 학생1과 학생2는 gender 속성을 쓸 수 있게됨

---

### 작동원리

- `학생1.gender` 가 `남` 이 출력되는이유
    
    JS는 오브젝트에서 값을 출력할때 순서를 물어보기때문
    
    1. 학생1에 직접 gender라는 값이있는가? ⇒ 없음
    2. 그럼 부모 유전자에 gender라는 값이있는가? ⇒있음 
    3. 그럼 부모의 부모 유전자에 gender라는 값이 있는가? ⇒ (만약 위에 없었따면 이렇게찾음)
    
    이런 방식으로 찾기때문에 `학생1.gender` 는 남 이 출력됨
    

---

### JS내장함수 toString()을 쓸 수 있는이유

이유는 간단하다 위와같은 작동원리처럼 계속 물어보면서 찾아가기때문이다

이러면 `Array.prototype.toString()`을  이해 할 수 있게된다.

```jsx
let arr = [1,2,3] //개발할때
let arr = new Array(1,2,3) //컴퓨터작동방식
```

이러면 `Array라는 기계로부터 자식을 하나 새로 뽑아주세요` 라는 뜻이되어서 Array의 유전자에있는 map,forEach등등 사용할 수 있게된다

---

### prototype으로 상속시크는것과 constructor로 상속시키는것의 차이

자식들의 값을 직접 소유하게만들고싶다 ⇒ constructor

부모나 가지고 있고 그걸 참조해서 쓰게 만들고싶다 ⇒ prototype

---

### prototype은 consturcotr 함수에만 몰래생성됨

- 일반적으로 object, array 만들어도 여기엔 prototype이 없다
    
    ```jsx
    let arr = [1,2,3];
    console.log(arr.prototype) //=> 아무것도없음
    let obj = {'name':'kim'}
    console.log(obj.prototype) //=> 아무것도없움
    ```
    
- 내 부모님 유전자를 찾고싶으면 __proto__ 를 출력해보면됨
    
    ```jsx
    function 기계(){
      this.name = 'Kim';
      this.age = 15;
    }
    var 학생1 = new 기계();
    console.log(학생1.__proto__); //기계.prototype과 같은값이 나옴
    console.log(기계.prototype);
    ```
    
    즉, __ proto__ 는 `부모의 prototype` 을 의미한다고 알아두면됨
    
- __proto__를 직접등록하면 object끼리 상속구현가능
    
    ```jsx
    var 부모 = { name : 'Kim' };
    var 자식 = {};
    
    자식.__proto__ = 부모;
    console.log(자식.name);
    ```
    
    이렇게하면 자식의 부모유전자는 부모 오브젝트가 되는것이다. 이렇게되면 자식은 자식.name을 자유롭게 사용가능