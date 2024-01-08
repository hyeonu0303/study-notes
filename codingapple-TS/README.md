# TypeScript 문법정리

### tsconfig.json

```tsx
{
 "compilerOptions": {

  "target": "es5", // 'es3', 'es5', 'es2015', 'es2016', 'es2017','es2018', 'esnext' 가능
  "module": "commonjs", //무슨 import 문법 쓸건지 'commonjs', 'amd', 'es2015', 'esnext'
  "allowJs": true, // js 파일들 ts에서 import해서 쓸 수 있는지 
  "checkJs": true, // 일반 js 파일에서도 에러체크 여부 
  "jsx": "preserve", // tsx 파일을 jsx로 어떻게 컴파일할 것인지 'preserve', 'react-native', 'react'
  "declaration": true, //컴파일시 .d.ts 파일도 자동으로 함께생성 (현재쓰는 모든 타입이 정의된 파일)
  "outFile": "./", //모든 ts파일을 js파일 하나로 컴파일해줌 (module이 none, amd, system일 때만 가능)
  "outDir": "./", //js파일 아웃풋 경로바꾸기
  "rootDir": "./", //루트경로 바꾸기 (js 파일 아웃풋 경로에 영향줌)
  "removeComments": true, //컴파일시 주석제거 

  "strict": true, //strict 관련, noimplicit 어쩌구 관련 모드 전부 켜기
  "noImplicitAny": true, //any타입 금지 여부
  "strictNullChecks": true, //null, undefined 타입에 이상한 짓 할시 에러내기 
  "strictFunctionTypes": true, //함수파라미터 타입체크 강하게 
  "strictPropertyInitialization": true, //class constructor 작성시 타입체크 강하게
  "noImplicitThis": true, //this 키워드가 any 타입일 경우 에러내기
  "alwaysStrict": true, //자바스크립트 "use strict" 모드 켜기

  "noUnusedLocals": true, //쓰지않는 지역변수 있으면 에러내기
  "noUnusedParameters": true, //쓰지않는 파라미터 있으면 에러내기
  "noImplicitReturns": true, //함수에서 return 빼먹으면 에러내기 
  "noFallthroughCasesInSwitch": true, //switch문 이상하면 에러내기 
 }
}
```

---

### union type

유니온 타입은 | OR연산자로 타입이 여러개 들어올 수 있다가 지정해주는것이다.

```tsx
let 이름: string | number = 'park';
```

### any type

아무자료나 넣을 수 있는 타입 (변수 타입 해제 기능 이런 용도로 씀)

```tsx
let 이름 : any = 'kim';
이름 = 123
이름 = undefined //아무거나 들어 올 수 있음 
```

### unknown type

1. unknown역시 모든타입을 넣어줄 수 있다
2. unknown 타입을 다른곳에 집어넣으려고하면 실드가 발동해서 에러남

```jsx
let 이름 :unknown;

let 변수1 :string = 이름; //에러발생 any는 이러질 않음
```

---

### 함수에 type을 지정하는방법

```tsx
type FuncType:(arg:number)=>{return number}
const func:FuncType = (arg) => {
	return 1
}

//일반적으로 지정하는방법
const func1 = (...args:(string|number)[]):void => {
	console.log(args)
}

```

### Narrowing문법

타입이 union type이거나할때 타입을 하나로 지정해주게 할려는것 

```tsx
const getNumber = (x:string|number) => {
	//return x + 1; 에러발생 => 타입이 number로 정확하지않아서
	if(x && typeof x === 'number')
		return x + 1
	else if(x && typeof x == 'string')
		return x + '안녕'
	else 
		return 0
}
```

### Type Assersion(as)

as를 활용해 number로 생각해달라고 코드를 짬

```tsx
const func = (arg:number|string):number => {
	return arg(as number) + 1
}
console.log(123)
```

- as키워드 사용시 특징
    1. union type같은 복잡한 타입을 하나의 타입으로 줄이는 역할
    2. 타입실드 임시해제용
    3. ‘123’ as number+ 1 해도 1231출력 ⇒ 실제로 타입을 변경해주는건 아니기떄문
- as문법을 사용하는 시점
    1. 왜 타입이 에러나는지 정말 모르겠는 상황
    2. as를 붙일려는 변수의 타입이 100% 확실한 상황에서만 사용 (타입 확실한데 컴파일러가 에러날때)

---

### type 키워드

- type이 너무길때 따로 빼서 사용
- type 재사용 할 수 있음
- 재정의불가 같은 type또 쓸 수 없음

```tsx

type Person = {
	name:string,
	age:number,
	height:number
}

let person:Person = {name:'Park', age:26, height:173}
```

### readonly

```tsx
const obj = {
	name:'park'
	age: 26
}

obj.name = 'kim'

console.log(obj.name) //'Kim' 출력
```

object에서 const 변수를 사용해도 object 안에 속성을 변경할 수 있다 ⇒ 변수에 재할당이 아니기때문 ⇒ TS에서 이걸 막아줄려면 readonly 키워드사용

```tsx
const obj = {
	readonly name:'park'
	age: 26
}

obj.name = 'kim' //에러발생
```

### type키워드 합치기

```tsx
type Name = string;
type Age = number;
type newType = Name | Age
```

### Object에 타입을 지정할경우

```tsx
type PositionX = { x: number };
type PositionY = { y: number };
type XandY = PositionX & PositionY
let 좌표 :XandY = { x : 1, y : 2 }
```

---

### Literal Types

특정문자 같은걸로 타입을 지정해주는것 

```tsx
let john: '존'
let kim : '김'
let 방향 = 'left' | 'right'
```

### as const

```tsx
let 자료 = {
	data:'read'
} as const

const func = (arg:'read') => { //read로 literal type사용불가
	
}

func(자료.data) 
```

[`자료.data`](http://자료.data) 는  string타입이어서 `arg:’read’` 를 사용하지 못한다 그러므로 `as const`를 활용한다

- as const 기능
    1. 타입을 object의 value로 바꿔줌 
    2. readonly로 변경해줌

---

### DOM Manupulation

html 조작과 변경에 있어 type을 어떻게 지정해줄지에대한 문제

```tsx
<h4 id="title">안녕하세요</h4>
<a href="naver.com">링크</a>
<button id="button">버튼</button>

<script src="변환된 자바스크립트파일.js"></script>
```

- 타입체크하는 4가지방법(instanceof를 주로 사용)

```tsx
//narrowing
let 제목 = document.querySelector('#title');
if (제목 != null) {
  제목.innerHTML = '반갑소'
}

//instanceof
let 제목 = document.querySelector('#title');
if (제목 instanceof HTMLElement) {
  제목.innerHTML = '반갑소'
}

//assertion
let 제목 = document.querySelector('#title') as HTMLElement;
제목.innerHTML = '반갑소'

//optional chaining
let 제목 = document.querySelector('#title');
if (제목?.innerHTML != undefined) {
  제목.innerHTML = '반갑소'
}
```

---

### Class에 type지정하는방법

```tsx
class Person{
	name:string,
	age:string
	constructor(name:string,age:number){
		this.name = name;
		this.age = age;
	}
}
```

---

### Object에 사용하는 interface 문법

```tsx
interface Person {
	name:string,
	age:number
}

let person:Person = {name:'kim', age:25}
```

이렇게 위와같이 interface를 사용함으로써 타입지정을해줄 수 있다 extends역시 가능한데

### extends

```tsx
interface Person {
	name:string,
	age:number
}

interface Park extends Person{
	school:string
}

let person:Park = {name:'park', age:26, school:'namkang'}
```

### type키워드와 interface키워드 차이점

1. extends 문법이 약간다르다
    
    ```tsx
    interface Animal { 
      name :string 
    } 
    interface Cat extends Animal { 
      legs :number 
    }
    
    //type
    type Animal = { 
      name :string 
    } 
    type Cat = Animal & { legs: number }
    ```
    
2. type은 중복선언이안되지만 interface는 중복선언가능

### 둘은 어떻게 구별해서사용하는가?

1. 남이 나의 코드를 이용해서 사용할시 Interface 아니면 type
2. object자료형은 interface 다른 자료형은 type 이런식으로도 사용

---

### rest parameter, destructuring 타입지정하는방법

- rest parameter

```tsx
const pr = (...rest:number[]) => { //배열형식으로지정 
	console.log(rest) //[1,5,2,3,4,5]
}
pr(1,5,2,3,4,5)
```

- destructuring

```tsx
let {name,age}:{name:string,age:nubmer} = {name:'park', age:25} //destructuring문법
let person:{name:string,age:nubmer} = {name:'park', age:25} 
const pr = ({name,age}:{name:string,age:number}):void => {
	console.log(name,age) //park,25
}
pr(person); 

let [a,b,c] = [1,2,3];
let num = [1,2,3]
const destructuringArrPr = ([a,b,c]:number[]) => {
	console.log(a,b,c) // 1,2,3
}

destructuringArrPr(num)

```

---

### 복잡한것들 쉽게 Narrowing 해줄 수 있는 방법

### in 연산자로 object 자료 narrowing

```tsx
type Fish = {swim :string};
type Bird = {fly :string};

const func = (animal:Fish|Bird) => { //이런 literal type
	//narrowing 방법
	if("swim" in Fish){
		return animal.swim
	}
	return animal.fly
}
```

### class로부터 생산된 Object면 instanceof로 narrowing

```tsx
let 날짜 = new Date();
if(날짜 instanceof Date){
	console.log('true')
}
```

### object가 많아서 literal type으로 지정했을때 narrowing방법

```tsx
type Car = {
  wheel : '4개',
  color : string
}
type Bike = {
  wheel : '2개',
  color : string
}

function 함수(x : Car | Bike){
  if (x.wheel === '4개'){
    console.log('the car is ' + x.color)
  } else {
    console.log('the bike is ' + x.color)
  }
}
```

`literal type으로 선언된 속성이 뭔지 찾아내면 narrowing가능`

---

### Never type

Never type은 이렇게 설명할 수 있다. 함수가 끝나지않을때 등장하고 코드이상하게 짜면 등장한다.

```tsx
//에러는 함수를 끝내는게 아니므로 never type이 된다.
function 함수(){
  throw new Error()
}

let 함수2 = function (){
  throw new Error()
}

```

---

### public private 키워드

class 에서 사용할 수 있는 키워드이다 

`public` class안에서든 밖에서든 자식이든 변수, 함수등을 사용할 수 있게해준다

```tsx
class Person{
	public name:string;
	public age:number;

	constructor(name:string, age:number){
		this.name = name;
		this.age = age
	}
} 

let person = new Person('park',26)
person.name = 'kim'
//자식인 person의 name이 kim으로변경할 수 있다
```

`private`는 class안에서만 사용가능한데 자식은 사용할 수 없다 (변경불가능)

```tsx
class Person{
	public name:string;
	public age:number;
	private familyName:string = 'park'	
	constructor(name:string, age:number){
		this.name = name;
		this.age = age
		let name = this.familyname + this.name; //가능
	}
} 

let person = new Person('hyeon',26)
person.name = 'kim' //가능
person.familyName = 'han' // 불가능
```

### protected

`protected` 키워드는 `private` 와 유사하지만 조금 다르다 class를 extends했을때 this로 사용할 수 있으나 자식에선 역시나 변경불가능하다

```tsx
class Person{
	public name:string;
	public age:number;
	protected familyName:string = 'park'	
	constructor(name:string, age:number){
		this.name = name;
		this.age = age
		let name = this.familyname + this.name; //가능
	}
} 

class Park extends Person{
	constructor(){
		super()
		let fullName = this.familyName + this.name
	}
}

let person = new Person('hyeon',26)
person.name = 'kim' //가능
person.familyName = 'han' // 불가능
```

### static

static은 class에 직접 변수나 함수를 부여하고싶을때 사용

```tsx
class User{
	x=10;
	y=10;
}
let park = new User();
park.x//가능
User.x//불가능

class User{
	static x=10;
	y=10;
}
let park = new User();
park.x//불가능
User.x//가능
```

- 예제

```tsx
class User { 
  static skill = 'js'; 
  intro = User.skill + '전문가입니다'
}
var hyeon = new User();
console.log(hyeon)

User.skill = 'ts'
let choi = new User();
console.log(choi) // User.skill 이 ts로 변경되어있음

//수정함수를 사용해서 변경하는게 더 바람직하다
```

---

### import export

```tsx
//a.ts
export type Name = 'string' | boolean;
export type Age = (a:number) => number

//b.ts
import {Name,Age} from './a.ts'
let 이름:Name = 'park' //사용가능
```

- 과거엔 namespace사용

```tsx
//a.ts
namespace MyNameSpace{
	export interface PersonInterface {age : number};
	export type NameType = number | string; 
}

//b.ts
/// <reference path="./a.ts" />
let 이름: MyNameSpace.NameType = 'minsu';

//이렇게하면 중복을 방지할 수 있어서 namespace를 사용했다. 
//예제
type Dog = string;
interface Dog { name : string };

let dog1 :Dog = 'bark';
let dog2 :Dog = { name : 'paw' }
//해답
namespace GoodDog {
  export type Dog = string;
}
namespace BadDog {
  export interface Dog { name : string };
}

let dog1 :GoodDog.Dog = 'bark';
let dog2 :BadDog.Dog = { name : 'paw' }
```

---

### Generic

Generic은 파라미터처럼 타입을 입력할 수 있게해줌

`extends` 여기서 쓰임은 number라는 type인지 체크해주는 기능

```tsx
const pr = <T extends number>(arg:T):T => {
		return arg + 1 	
}

pr<number>(10) // 11출력

interface lengthCheck {
  length : number
}
function 함수<MyType extends lengthCheck>(x: MyType) {
  return x.length
}

let a = 함수<string>('hello')  //가능
let a = 함수<number>(1234) //에러남
```

---

### React에서 type을 사용하는방법

함수 변수 정의부분 타입지정을 할 수 있다, props에 정의만 잘해줘도됨

---

### array자료에 쓸 수 있는 tuple type

```tsx
let 멍멍:[string,boolean] = ['dog',true] 

type Num = [number,number?, number] //이렇게 사용못함 왜냐면 중간에 하나가 빌 수 있어서
```

이런식으로 순서에 맞춰서 타입을 지정해줄 수 있다 좀더 엄격

---

### declare 키워드

`declare` 쓰면 이미 정의된 변수나 함수를 재정의 할 수 있음 (type도)

```tsx
//data.js
let a = 10;
let b = {name : 'kim'}

//index.ts
declare let a :number;
console.log(a+1);
```

`a 라는 변수를 이 파일에 잠깐 정의해주세요` 라는 뜻이며 declare 이게 붙은 코드는 js로변환되지않음

그래서 자바스크립트로만 작성된 외부 라이브러리들을 쓸 때도 나름 유용합니다.

타입스크립트 버전이 없다면 직접 declare로 타입작성하면 됩니다.

ts 파일들은 변수만들 때 타입까먹어도 자동으로 타입지정이 되어있으니 굳이 쓸 이유는 없습니다

근데 여러분이 tsconfig.json 안에 allowJs 옵션을 true로 켜두면

js파일도 타입지정이 알아서 implicit 하게 됩니다.

리액트 같은 프로젝트에서 유용

### Ambient Module

이상한기능을하는 TS.. import export 없이 다른파일에서 타입을 가져다 쓸 수 있음

```tsx
//data.ts
type Age = number;
let 나이 : Age = 20;

//index.ts
console.log(나이 + 1) //가능
let 철수 :Age = 30; //가능
```

ts에 입력한 변수와 타입은 global변수 취급을 받음 ⇒ ambient module이라고 칭함

반면에 `import export 키워드가 적어도 하나 있으면 그 파일은 로컬 모듈이 된다`

`export{}` 붙여야함

### declar global

로컬에서 전역변수로 만들고 싶을때 ⇒ 잘 쓸일 없음

```tsx
declare global {
	type Dog = string;
}
```

일종의 namespace 문법과 같다고 보면됨

---

### .d.ts파일

타입의 정의만 넣을 수 있는파일명이다 

### 레퍼런스용으로 사용할려면?

```tsx
//tsconfig.json
{
    "compilerOptions": {
        "target": "es5",
        "module": "es6",
        "declaration": true, //추가
    }
}
```

index.d.ts파일이 생김

### export 없이 d.ts파일을 글로벌 모듈 만들기

원래 d.ts 파일은 import export 없어도 로컬모듈입니다.

그래서 다른 ts파일에서 import를 해서 쓸 수 밖에 없는데

이게 귀찮으면 d.ts를 글로벌 모듈로 만들어보십시오.

파일이 많아지면 섞이기 때문에 굳이 왜 하나 싶지만

프로젝트 내에 types/common 이런 폴더 두개를 만드시고

tsconfig.json 파일에 **"typeRoots": ["./types"]** 이런 옵션을 추가해주면 됩니다.

이러면 ts 파일 작성할 때 타입없으면 자동으로 여기서 타입 찾아서 적용해줌

- 다만 이걸 쓸 경우 파일명.d.ts 자동생성 기능은 끄는게 좋을 듯 합니다.
- d.ts 파일명은 기존 ts 파일명과 안겹치게 작성하는게 좋습니다.
- 하지만 이런거 쓰다가 로컬 타입과 저런 글로벌 타입이 겹치면 어쩌쥬 역시 import export가 안전합니다.
- 그래서 보통은 d.ts 파일 만들어서 글로벌 타입보관함으로 쓰는 경우는 별로 없습니다.

### [Definitely Typed](https://github.com/DefinitelyTyped/DefinitelyTyped)  < = 여기를 이용하면 라이브러리 타입정의가 있음

---

### implements

class가 interface의 정의된 속성을 가지고 있는지 체크하는문법

‼️타입을 바꿔주는것이아닌 체크만하는것 

```tsx
interface CarType {
  model : string,
  price : number
}

class Car implements CarType {
  model : string;
  price : number = 1000;
  constructor(a :string){
    this.model = a
  }
}
let 붕붕이 = new Car('Ferrari');
```

---

### index signatures

object용 타입을 만들고싶은데 뭐가 들어올지모를때 사용

```tsx
interface StringOnly{
	[key: string] : string
}

let obj :StringOnly = {
	name : 'kim',
	age : '20',
	location : 'seoul'
}

interface StringOnly {
  [key: number]: string,
}

let obj :StringOnly = {
  0 : 'kim'
  1 : '20',
  2 : 'seoul'
}
```

### Recursive Index Signatures

자신을 type으로 하고 출력되는걸 number로 해줌으로써 타입을 지정해준다

```tsx
interface MyType {
  'font-size': MyType | number
}

let obj = {
  'font-size' : {
    'font-size' : {
      'font-size' : 14
    }
  }
}
```

---

### keyof 연산자

keyof는 object에 사용하면 object 타입이 가지고있는 모든 key값을 union type으로 합쳐서 내보냄 즉, literal type이 됨 

```tsx
interface Person {
  age: number;
  name: string;
}
type PersonKeys = keyof Person;   //"age" | "name" 타입됩니다
let a :PersonKeys = 'age'; //가능
let b :PersonKeys = 'ageeee'; //불가능

interface Person {
  [key :string]: number;
}
type PersonKeys = keyof Person;   //string | number 타입됩니다
let a :PersonKeys = 'age'; //가능
let b :PersonKeys = 'ageeee';
```

### Mapped Types

object안에 있는 속성들을 전부 바꿔주고싶을때 사용

```tsx
type Car = {
  color: boolean,
  model : boolean,
  price : boolean | number,
};

type TypeChanger <MyType> = {
  [key in keyof MyType]: string; //여기가핵심
};

type 새로운타입 = TypeChanger<Car>;

let obj :새로운타입 = {
  color: 'red',
  model : 'kia',
  price : '300',
}
```

keyof 는 key값을 union type으로 합쳐주는 기능을한다 in 키워드는 오브젝트에서 key값중에 `“color”` 가 있으면 string으로 바꿔라 약간 이런식으로 흘러간다.

그러면 obj에 새로운타입을 적용하면 string으로 바뀌는것

---

### Type을 조건문으로 만들때

타입을 조건문으로 만들때 `extends키워드와 삼항연산자`를 이용 

```tsx
type Age<T> = T extends string ? string : unknown;
let age : Age<string> //age는 string 타입
let age2: Age<number> //age는 unknown타입됨

/*
Q. 그럼 파라미터로 array 자료를 입력하면 array의 첫 자료의 타입을 그대로 남겨주고,
array 자료가 아니라 다른걸 입력하면 any 타입을 남겨주는 타입은 어떻게 만들면 될까요?
*/

type FirstItem<T> = T extends any[] ? T[0] : any

let age1 :FirstItem<string[]>;
let age2 :FirstItem<number>;
```

### infer키워드

infer 키워드는 `지금 입력한 타입을 변수로 만들어줌` 

1. infer는 조건문안에서만 사용가능
2. 우측에 자유롭게 작명해주면 타입을 T에서 유추해서 R이라는 변수에 집어넣어라라는 뜻
3. R을 조건식 안에서 맘대로 사용가능

`타입파라미터에서 타입을 추출해서 쓰고싶을 때 쓰는 키워드`

1. array안에 있던 타입이 어떤 타입인지 뽑아서 변수로 만들어 줄 수 있음

```tsx
type 타입추출<T> = T extends (infer R)[] ? R : unknown; 
type NewType = 타입추출< boolean[] > // NewType 은 boolean 타입
```

1. 함수의 return 타입이 어떤 타입인지 뽑아서 변수로 사용가능

```tsx
type 타입추출<T> = T extends (()=>infer R) ? R : unknwon;
type NewType = 타입추출<()=>number> // NewType은 number 타입
```