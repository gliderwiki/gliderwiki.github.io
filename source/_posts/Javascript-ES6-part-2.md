---
title: Javascript-ES6 part 2
date: 2017-08-02 05:13:11
categories:
- Front
- Javascript
tags: [Javascript, ES6]
---

![ECMAScript 6](/images/js/es6/es6.jpeg "ES6")

## Arrow Function 
화살표 함수 표현(arrow function expression)은 익명 함수 표기법으로 function 표현에 비해 구문이 짧고, 자신의 this, arguments, super 등을 바인딩 하지 않는다.

기본 표기법은 아래와 같다.

`() => { ... }`

Identifier => Expression 형태의 구문인데 아래 그림을 보면 더 정확하게 이해할 수 있을것이다.

![Arrow Function](/images/js/es6/arrow.png)

전달하고자 하는 파라미터가 하나일 경우 괄호를 생략할 수 있고, 리턴 되는 리터럴에 따라 body를 감싸서 보낼 수 도 있다..

 
{% codeblock lang:javascript Example %}
params => ({foo: bar})
{% endcodeblock %}

아래의 예제를 살펴보면 기존 구문과의 차이에 대해서 명확히 알 수 있다.
둘다 동일한 기능을 수행한다. 
```javascript
var lang = [
  "Javascript",
  "ASP",
  "JAVA",
  "Python"
];

var normal = lang.map( function(s) { return s.length });

var arrow = lang.map( s => s.length );

console.log('normal = ' + normal);
console.log('arrow = ' + arrow);

```

함수의 본문은 return을 생략할 수 있다. 

{% codeblock lang:javascript Example %}

var func = x => x * x;                  // 간결한 구문, "return" 생략 
var func = (x, y) => { return x + y; }; // 블록 본문일 경우 "return" 명시 
{% endcodeblock %}

객체 리터럴은 괄호로 감싸야 한다. 

아래의 예제를 보자 
```javascript
var lang = [
  "Javascript",
  "ASP",
  "JAVA",
  "Python"
];

const myLanguage = lang.map( (value) => {
  return `Hello ${value} World\n`;
});

console.log(myLanguage);
```
return 구문을 생략할 경우 undefined 가 lang의 갯수만큼 출력될 것이다. 

애로우 펑션의 가장 큰 장점은 복잡한 수준의 코드를 간결하게 할 수 있다는 점이다.
map, filter, reduce등을 이용하면 수십라인의 코드도 몇라인 수준의 명확한 코드로 작성될 수 있다. 

아래의 예제를 살펴보자. 

```javascript
const arrays = ['cherry', 'orange', 'apple', 'applemango',
                'banana', 'orange', 'apple', 'applemango',
                'banana', 'cherry', 'orange', 'watermelon' ];

const groups = arrays.reduce( (total, fruit) => {
  total[fruit] = (total[fruit] || 0) + 1 ;
  return total;
} , {})
console.log(groups)

// { apple: 2,  applemango: 2,  banana: 2,  cherry: 2,  orange: 3,  watermelon: 1 }
```


arrays 안에 있는 자료를 그룹핑 카운트 하는 예제이지만 이와 같이 
map, filter, reduce와 같은 함수형 프로그래밍을 지원하는 메서드와 같이 사용하면 코드의 양이 줄어들고 강력한 기능을 제공할 수 있다.
 
#### arrow function의 this context 

아래의 예제를 살펴보자. 
{% codeblock lang:javascript function 의 this %}
const thisObj = {
    run() {
        setTimeout(function () {
            console.log(this === window); 
        }, 1000);
    }, 
    printRun() {
        console.log('Hello Arrow Function!');
    }
}

thisObj.run();
{% endcodeblock %}


true 가 출력되는 것을 확인할 수 있다.
따라서 thisObj안의 setTimeout 함수 내부에서 this.printRun()을 호출하게 되면 this를 통한 내부 호출을 하지 않기 때문에 에러가 발생하게 된다.
this 가 thisObj의 printRun()을 호출하고자 할 때에는 setTimeout().bind(this)로 감싸주어야 정상적으로 접근이 된다.
Arrow function일 경우 반대의 상황이 벌어진다.

{% codeblock lang:javascript arrow function 의 this %}
const thisObj = {
    run() {
        setTimeout( () => {
            console.log(this === window); // false
            this.printRun();
        }, 1000);
    }, 
    printRun() {
        console.log('Hello Arrow Function!');
    }
}

thisObj.run();
{% endcodeblock %}

arrow function 으로 변환한 내부에서는 this가 window 가 아닌 thisObj를 가르킨다. 
따라서 따로 bind(this)를 통해 처리 하지 않더라도 정상적으로 내부의 printRun() 메서드가 호출이 되는 것을 확인할 수 있다. 



## Class 

Javascript 는 프로토타입 기반의 객체지향 프로그래밍이 가능하다.
이를 위해 prototype 이나 Object.create 구문등으로 Class스럽게 코드를 작성했지만 ES6에서는 Class 가 지원이 되었다.
 
{% codeblock lang:javascript %}
class Member {
  constructor(userId) {
	this._userId = userId;
  }

  findId() {
	return 'Member ID = ' + this._userId;
  }
}

class Login extends Member {
  findId() {
	return '[Login findId] ' + super.findId();
  }
}

var member = new Member('GLiDER');
console.log(member.findId()); // Member ID = GLiDER

var login = new Login('QuicK');
console.log(login.findId()); // [Login findId] Member ID = QuicK
{% endcodeblock %}


## Module
 

## New Built-In Methods 