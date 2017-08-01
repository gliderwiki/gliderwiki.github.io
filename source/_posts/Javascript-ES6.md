---
title: Javascript-ES6 part 1
date: 2017-08-01 17:30:34
categories:
- Front
- Javascript
tags: [Javascript, ES6]
---

![ECMAScript 6](/images/js/es6/es6.jpeg "ES6")
## let, const 

기존 ES5에서는 변수를 선언할 때 var 키워드를 사용하였다.
그러나 var의 경우 전역변수로 간주되거나 의도치 않게 중복된 변수 선언을 한다던가 
변수 호이스팅(Variable Hoisting)이 일어나 변수를 선언하기 전에 참조가 가능한 문제가 발생하게 된다.

이 때문에 예기치 못한 참조나 의존으로 인한 side effect이 있어 복잡도가 증가하기 때문에 var의 단점을 보완한 let과 const 라는 키워드를 정의하였다.

#### let 

let은 Block-level scope를 갖는다. 코드 블럭 외부에서 참조할 경우 ReferenceError 가 발생한다. 
또한 let으로 선언된 변수를 중복해서 선언할 경우 Syntax에러가 발생한다. 

```javascript
var global = "abc";
function variable() {
  let local = "123";
  
  console.log('local : ' + local); // 123
}

variable();

console.log('global : ' + global);  // abc 
console.log('window.global : ' + global); // abc 
console.log('local : ' + local);  // ReferenceError: local is not defined
``` 

이와 같이 블럭 외부에서 참조할 경우 레퍼런스 에러가 발생하는 것을 확인할 수 있다. 
전역적 값을 갖는 변수로 인한 문제를 해결하기 위해 지역 변수의 스코프를 갖는 동시에 중복선언이 되지 않기 때문에 가급적 코드 블럭 내에서는 let을 이용하여 변수를 선언하는게 좋다. 

### const 

변하지 않는 값을 위해 사용하는데, let과 비슷하지만 const는 초기화 이후 재할당이 금지 된다. 
또한 선언과 동시에 초기화를 해주어야 한다. 그렇지 않을 경우 아래와 같은 에러가 발생한다.

`SyntaxError: Missing initializer in const declaration` 

const가 재할당을 할수 없다고는 하나 객체 리터럴의 경우 값의 추가 혹은 할당된 객체의 내용은 변경할 수 있다. 
객체 리터럴의 경우 const에 지정된 주소값의 변경이 되지 않는것이지 객체의 프로퍼티 값은 변경이 가능하다. 

```javascript
function myList() {
  const list = ["java", "javascript", "mysql"];
  console.log('list = ' + list); // java,javascript,mysql
  
  list.push("node");
  console.log('push list = ' + list); // java,javascript,mysql,node
}

myList();
```


## Template Literal
백틱 문자 ` 를 이용한 멀티 라인 지원과 값 내의 이스케이프 문자열 치환을 해결하였다. 


## Spread Operator 

## Destructuring 

## Map, WeakMap 

Map은 Key와 Value을 서로 연결(매핑)시켜 저장하며 저정된 순서대로 각 요소들을 반복적으로 접근할 수 있도록 한다. 
 
> [Map API 확인하기](https://developer.mozilla.org/ko/docs/Web/JavaScript/Reference/Global_Objects/Map) 


```javascript 
let myMap = new Map([
      ['key1' , 'value1'],
      ['key2' , 'value2']
]);
```



## Set, WeakSet

#### Set 
Set운 중복을 허용하지 않는 값들의 집합이다. 입력된 순서에따라 저장된 요소를 반복처리할 수 있다.
또한 배열과 달리 delete 메소드를 이용하여 요소의 값을 삭제할 수 있으며, indexOf 메소드로 값을 확인하는것 보다 has 가 더 빠르다
 
> [Set Api 확인하기](https://developer.mozilla.org/ko/docs/Web/JavaScript/Reference/Global_Objects/Set) 
 
 
```javascript
let mySet = new Set();
mySet.add("1st");
mySet.add("2nd");
mySet.add("3rd");

mySet.forEach(function(value) {
    console.log("value = " + value);
});
```

순차적으로 값이 출력되는 것을 확인 할 수 있다.

Set 내부에 특정한 값이 존재하는지 체크하려면 아래와 같다. 
```javascript
if (mySet.has("1st")) {
... 
} 
```

Set 내부의 값을 삭제하려면 delete 메소드를 이용한다.
```javascript
mySet.delete("1st");
```

#### WeakSet 