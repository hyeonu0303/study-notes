# import export

### import export 사용시 내가원하는 변수,함수,class만 다른 파일로 보낼 수 있음

- 변수가 한개일때
    
    ```html
    <!--import를 사용할려면 module로 설정해주어야함-->
    <script type="module">
    	import a from 'library.js';
    </script>
    ```
    
    ```jsx
    //library.js
    let a = 10;
    export default a;
    ```
    
- 변수를 여러개 내보내고싶을때
    
    ```jsx
    //library.js
    let a = 10;
    let b = 20;
    export {a,b};
    ```
    
    ```html
    <script>
    	import {a,b} from 'library.js';
    	console.log(a);
    </script>
    ```
    
- export default와 export {변수명}의 차이
    
    export default는 `import시엔 변수명을 새롭게 작명가능하다`
    
    export {변수명1,변수명2}는 `import 할때 정확한 변수명을 적어야한다`
    
    `동시사용가능`
    
    ```jsx
    var a = 10;
    var b = 20;
    var c = 30;
    export {a, b};
    export default c;
    //--------------------------
    
    <script type="module">
      import c, {a,b} from 'library.js';
      console.log(c);
    </script>
    ```
    
- 변수명이 맘에들지않으면 as 키워드로 수정가능
    
    ```jsx
    import c, {a as 폭발} from 'library.js';
    ```
    
- import시 변수가 너무많으면 * 사용
    
    ```jsx
    import c, * as 변수모음 from 'library.js';
    ```