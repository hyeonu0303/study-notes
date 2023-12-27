# Lect01~06

## this의 의미

### 1.그냥 쓰거나 함수 안에서 쓰면 this는 window를 뜻함

```jsx
console.log(this)
function thisShow(){
	console.log(this) //strict mode에선 undefined
}
window.thisShow()
```

![Untitled](https://github.com/hyeonu0303/study-notes/assets/56960705/66f06457-9548-4a94-96f2-592d858e78f7)


- window는 모든 전역변수,함수, DOM을 보관하고 관리하는 전역객체
    
    ```jsx
    let x = 300;
    ```
    
    위와같은 전역변수도 만들었을때 이 값을 보관해줌
    

---

### 2.object 자료형 내 메소드에선 this값은 그 오브젝트를 뜻함

```jsx
let obj = {
      data: 'kim',
      func : function(){
        console.log(this) // 함수를 가지고 있는 오브젝트를 뜻함 obj1내용나옴
      },
      data1:{
        func1: function(){
          console.log(this) // data1 내용나옴, arrow func는 최상위 window가 뜸
        }
      }
    }
obj.func()
obj.data1.func1()
```

![Untitled 1](https://github.com/hyeonu0303/study-notes/assets/56960705/6c887093-acba-48ea-855b-3c37f0ac41db)


this를 오브젝트 내의 메소드에서 사용했을때 오브젝트를 출력해준다는걸 외우고있는게 좋음

---

### 3.constructor 안에서 쓰면 constructor로 새로생성되는 오브젝트를 뜻함

- 자바스크립트에서 오브젝트를 비슷한걸 여러개 만들고싶은경우 constructor를 만들어사용함
    
    쉽게말하면 오브젝트를 만들어주는 기계
    
    ```jsx
    function 기계(){
    	this.이름 = 'Kim' //this는 기계로부터 새로 생성될 오브젝트
    }
    let obj2 = new 기계();
    ```
    
    new 기계()는 생성자 함수를 사용하여 새 객체를 생성하고,  새로 생성되는 오브젝트에  `이름` 속성을 가지고있고 값은 `Kim` 이라는 값을 넣을수있게된다. (this라는 키워드 덕분에)
    

---

### 4.eventlistener 안에서 쓰면 this는 e.currentTarget의미

```jsx
document.getElementById('버튼').addEventListener('click', function(e){
  console.log(this)
});
```

this를 출력해보면 `버튼` 에대한 HTML요소가 나온다.

하지만 콜백함수에서 this를 쓰면 일반함수에서 쓴것과 같으므로 window객체가 나온다 (주의)

```jsx
document.getElementById('button').addEventListener('click',function(e){
	// console.log(this); //e.currentTarget
	// console.log(e.currentTarget);
	let array = [1,2,3];
	array.forEach(function(a){
		console.log(this);//일반함수에서 그냥 this사용했으니 window가 나옴
  });
})
```

```jsx
let obj3 = {
  name: ['김','이','박'],
  func: function(){
    console.log(this); //이것과 똑같음
    obj3.name.forEach(()=>{
      console.log(this); //(function작성시)일반함수안에서 쓰였으므로 window객체가 나옴, arrow func는 내부에서 쓴 this와 똑같은 값을가지고잇음
    })
  }
}

obj3.func()
```

---

## Arrow function

- 쓰는이유
    1. 함수의 본연 기능을 아주 잘표현한다
        - 함수는 여러가지 기능을 하는 코드 단어를 묶고싶을때
        - 입출력 기능을 만들때
    
    이럴때 함수를 사용하는데 arrow function을 사용하면 `입출력기능`을 아주 직관적으로 잘 표현해준다
    
    ```jsx
    let doubleValue = (x) => {return x * 2} //이해하기 더 쉬워짐 function에 비해
    let doubleValue = x => x * 2 이런식으로 생력가능
    
    doubleValue(5) // 출력 10
    ```
