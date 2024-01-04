# constructor

### constructor

- Object를 생성하는 기계
    
    형식이 같은 object를 계속 만들어내는것이다
    
    ```jsx
    function Student(name,age){ //constructor문법은 대문자로적음
      this.name = name; //this는 새로생성되는 object를 뜻함
      this.age = age;
      this.sayHi = function(){
         console.log(`안녕하세요${this.name}입니다.`)
      }
    }
    
    let 학생1 = new Student('Kim',15); //object뽑힘 {}게 남음 
    학생1.sayHi();
    let 학생2 = new Student('Park',14);
    ```
    
    상속임
    
    기계라는 constructor가 가진 name,age 속성을 그대로 물려받아서 object를 뽑아주는걸 상속이라고함