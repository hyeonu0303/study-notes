# Template literals/tagged literals/Spread Operator

### Template literals

```jsx
let 문자 = `안녕 하세요 ${변수}`
```

- 띄어쓰기 가능
- HTML작성할때도 유용

---

### Tagged Literals

- 문자 해체분석기능을 만들어줌 ⇒ 단어순서를 바꾸거나 변수 제거해줄수있음

```jsx
let 변수 = '손흥민';
function 해체분석기(문자들,변수들){
	console.log(문자들[1] + 변수들); //출력:입니다손흥민
}
해체분석기 `안녕하세요 ${변수} 입니다`;
```

---

### Spread Operator

- 괄호제거 해주는 연산자
    
    ```jsx
    let array = ['hello','world'];
    console.log(array); //[hello,world]
    console.log(...array); //hello,world
    ```
    
- 활용
    1. Array 합치기/복사에 사용
        - 합치기
        
        ```jsx
        let a = [1,2,3];
        let b = [4,5];
        let c = [...a,...b];
        ```
        
        위와같은 합성에도 사용
        
        - 복사
        
        ```jsx
        //얕은복사
        let a = [1,2,3];
        let b = a;
        console.log(a),console.log(b);
        a[3] = 4 //b는 a배열을 참조하고있으므로 b도 4가 추가된다.
        //위와같은걸방지하기위해를 한다
        //깊은복사
        let a = [1,2,3];
        let b = [...a];
        a[3] = 4;
        console.log(a); //[1,2,3,4]
        console.log(b); //[1,2,3]
        //이러면 값 공유가 이러나지 않는다.
        ```
        
        - object역시 사용가능
        
        ```jsx
        let o1 = {a:1, b:2};
        let o2 = {c:3, ...o1};
        console.log(o2); // {a:1, b:2, c:3}
        ```
        
        - 참고
            
            ```jsx
            let o1 = { a : 1, b : 2};
            let o2 = { a : 3, ...o1 };
            console.log(o2);
            ```
            
            이렇게 a가 중복 발생시 뒤에 오는 a가 이김
            
            spread연산자는 함수소괄호, 오브젝트 중괄호내, 어레이 대괄호내에서 보통사용해야함
            
    2. Array를 파라미터형태로 집어넣고 싶을때 사용
        
        ```jsx
        function sum(a,b,c){
        	console.log(a + b + c)
        }
        
        let array = [10,20,30];
        
        sum(array[0], array[1], array[2]) //귀찮은방식
        sum(...array); //더편리함
        sum.apply(undefined, array); //옛날방식
        ```
        
    
    ---
    
    ### apply, call 함수
    
    ```jsx
    /*
      상황: 인사라는 함수를 person2에도 적용하고싶음 
      객체 상속기능구현할때 많이쓰임
    */
    let person = {
        인사 : function(){
          console.log(this.name + '안녕')
        }
    }
      
    let person2 = {
        name : '손흥민'
    }
    
    person.인사.apply(person2); //person.인사()라는 함수를쓰는데 person2라는 오브젝트에 있는 함수처럼 실행하라는 뜻
    //실행할함수.apply(적용할곳)
    //apply는 배열,call은 1,2,3 이런식으로 넣을수있다는 차이점이 존재
    person.인사.apply(person2, [1,2]) //person.인사(1)이적용됨
    person.인사.call(person2, 1,2)
    
    function sum(a,b,c){
    	console.log(a + b + c)
    }
    
    let array = [10,20,30];
    sum.apply(undefined, array); //옛날방식
    //undefiend에 적용해서 실행해달라는걸 알수있다. 즉 아무곳에도 적용해서 실행하지 않게하기 위해 적은내용이다.
    ```