---
layout: post
title: "JavaScript Prototype"
date: 2022-09-22
categories:
- JavaScript
tags:
- JavaScript
- Prototype
- Object
- Prototype Object
- Prototype Chain
- Object.getPrototypeOf(obj)
- constructor
- instanceof
- ECMAScript 2015
- Class
- extends
- super
- get
- set
---

나는 왜 짧게 요약하지 못하는가.. 왜 다 중요하게 느껴지는가   
그것이 문제로다.

---

JS는 **Prototype(원형 객체)기반 언어(prototype-based language)**이다.~~(처음알았다 ㄷㄷ 함수형이라고만 알았는데 이게뭐야)~~

## MDN:Object prototypes

객체를 상속하기 위해 프로토타입을 사용한다. 모든 객체들이 method와 property를 상속받기위한 template이다.(Prototype object를 가짐) 상위의 객체의 method와 property를 가질 수 있는걸 **Prototype Chain**이라고 한다.

> Ref: 객체의 prototype(Object.getPrototypeOf(obj))함수 또는 ~~deprecated된 `__proto__`~~ 과 생성자의 prototype의 property 차이를 알아야된다. 전자는 개별 객체의 속성, 후자는 생성자의 속성. Object.getPrototypeOf(new Foobar())의 return값은 Foobar.prototype이다.

### Prototype Object 이해

일반적으로 생성한 객체의 dot chain은 Object의 정의된 다른 멤버도 볼 수 있다. 

- 생성한 어떠한 객체.valueOf() -> Object.prototype.valueOf() 동작 flow
  - window()(브라우저?)는 어떠한 객체가 valueOf() method있는지 확인
  - 없으면 constructor valueOf() method확인
  - 생성자의 prototype object의 Object constructor valueOf() method 확인하여 찾으면 호출함.

> Ref: 객체의 method와 property들이 복사되는것이 아니다. chain을 타고 접근한다.(없으면 생성자 없으면 상위객체 없으면 상위객체 생성자...)   
> 임의 객체의 prototype object에 바로 접근하는 공식적인 방법은 없다. `[[prototype]]` ECMAScript에서는 링크는 내부속성으로 정의되있지만 대부분의 모던 브라우저들이 `__proto__` property를 통해 임의 객체로 접근하도록 구현하였다. ex) `어떤객체.__proto__.__proto__` -> ECMAScript 2015부터는 Object.getPrototypeOf(obj) method통해 객체의 prototype object에 바로 접근할 수 있다.

### prototype property: inherit members location

왜 일부는 상속되고 일부는 상속되지 않는건가? 그건 sub-namespace인 prototype property에 정의되어 있어서이다. Object.이 아니라 Object.prototype.이 올바른 접근. prototype property도 Object이며, prototype chain을 통해 상속하고자하는 property와 method를 담아두는 bucket(바구니)로 사용되는 Object이다.

그래서 Object.prototype.watch(), Object.prototype.valueOf() 등은 생성자를 통해 새로 생성되는 instance는 물론 Object.prototype을 상속받는 객체라면 임의의 객체에서 접근할 수 있다.

Object의 생성자에서만 사용할수 있는 멤버들 prototype의 property나 method가 아니므로 접근이 불가하다. 이상하면 [Function() 생성자 확인](https://developer.mozilla.org/ko/docs/Web/JavaScript/Reference/Global_Objects/Function)

> Warn Important: this가 현재 객체의 prototype object일거라고 오해한다. 하지만 `__proto__` property로 접근 가능한 내장 객체라는걸 기억하자. prototype property는 상속 시키려는 member들이 정의된 Object를 가르킨다.

### Create()

Object.create()사용 시 주어진 객체를 prototype object삼아 새로운 object을 생성한다. 

```javascript
var anyObj = Object.create(someObj);

anyObj.__proto__;   //someObj출력
```

### [constructor](https://developer.mozilla.org/ko/docs/Web/JavaScript/Reference/Global_Objects/Object/constructor) property

모든 생성자 함수는 constructor property를 지닌 object를 prototype object로 가지고 있다. constructor property는 원본 생성자 함수 자신을 가르킨다. anyObj.prototype property 또는 아무 constructor method의 prototype property는 생성된 객체의 constructor의 모든 instance를 사용할 수 있다. 

constructor도 함수의 일종이므로 괄호를 붙이면 사용이 가능하고, new 키워드를 통해 실행하면 함수를 instance를 생성하기 위한 constructor로 사용할 수 있다.

```javascript
var someObj = new useCreateMethodObject.constructor(......values);
//자주 쓰이지 않으나, 실행 도중 명시적인 생성자 함수를 예측할 수 없는
// 상황에서 인스턴트 생성같은 경우 쓰면 좋다.

//인스턴스 생성자의 이름이 필요한 경우
instanceName.constructor.name

anyObj.constructor.name //?????
```

> Ref: constructor.name은 변경이 가능하다(상속, 바인딩, 전처리, 트랜스파일러등에 의해 변조가된대) 복잡한 로직에서는 [instanceof연산자](https://developer.mozilla.org/ko/docs/Web/JavaScript/Reference/Operators/instanceof)가 필요하다.

### Prototype 수정

prototype에 method를 추가하면 해당 생성자로 생성된 모든 객체에 사용이 가능하다.

prototype object는 모든 instance에서 공유하기 때문에 정의 즉시 갱신 과정 없이 접근이 가능하다.(위험한거아냐?)

좋은 방법은 아니니 property를 추가할 때 아래와 같이 사용하자

```javascript
OriginObject.prototype.productMade = 'made in Korea'
//를 바꾸서 쓸 수 있도록
OriginObject.prototype.productMade = this.boiler + this.nation;
//이라고 쓰면 함수 범위 위인 전역을 가르쳐 undefinedundefined만 도출

//member에 상수로 선언하고 변경하지 않는 값으로 사용해도 되지만
//생성될 때 한번만 실행되는 constructor에 선언해도 된다.(한번만 실행해줘)
function Test(a, b, c, d){
    this.a = a;
    this.b = b;
    this.c = c;
    this.d = d;
    ...
}

Test.prototype.a = function() {...};

Test.prototype.b = function() {...};
```

## [MDN:Prototype Inherit](https://developer.mozilla.org/ko/docs/Learn/JavaScript/Objects/Classes_in_JavaScript#%ED%94%84%EB%A1%9C%ED%86%A0%ED%83%80%EC%9E%85_%EC%83%81%EC%86%8D)

ECMAScript 2015 Class는 최신브라우저에서는 잘 작동하지만 IE에서는 작동하지 않으니 하는방법을 알아야한다.

```javascript
//Person(first, last, age, gender, interests) 부모를 상속하여 새로운 속성 만드는법
function Teacher(first, last, age, gender, interests, subject) {
    //call(this <- Teacher자신, ...실제 함수 실행에 필요한 인자들을 전달) 
    // java super();랑 비슷(부모의 값을 쓰기위해)
    Person.call(this, first, last, age, gender, interests);

    //부모가 가지지 않은 subject라는 항목을 사용하기 위해 정의
    this.subject = subject;
}

//매개변수가 없는 생성자 상속
function Brick(){
  //부모속성 안쓸거야 call()쓸필요없음.
  this.width = 10;
  this.height = 20;
  ...
}

//부모속성 받음
function ChildBrick(){
  //Brick.width, Brick.height 상속
  //Brick에 초기화하는 매개변수가 없어서 call()에 넘길필요가 없음.
  Brick.call(this);

  this.opacity = 0.5;
  this.color = 'blue';
}

//최상위 Teacher는 Person의 생성자의 프로토타입 속성이 없다.
//확인법 
//Object.getOwnPropertyNames(Teacher.prototype);
//Object.getOwnPropertyNames(Person.prototype);
//Teacher는 Person의 메서드를 상속받지 못하였음. -> Property Object의 create()를 사용
Teacher.prototype = Object.create(Person.prototype);
//상기코드만 넣으면 constructor속성이 Person으로 나옴
//확인 브라우저 재실행 후 Teacher.prototype.constructor return값 확인 Person()나옴
Teacher.prototype.constructor = Teacher;
//Teacher.prototype.constructor -> Teacher() return 의도한대로 동작
//Teacher는 정상적으로 Person도 상속했고, Teacher()

//prototype 정의
Teacher.prototype.someAction = function(){
  ......동작구현
};

//[MDN 예제](https://github.com/mdn/learning-area/blob/main/javascript/oojs/advanced/oojs-class-inheritance-finished.html)
```

## Prototype & Class

- 임의의 클래스와 인스턴스, 프로토타입의 관계

|---|:---:|---|---|
|-|AnyClass||-|
|.constructor|↑|↓|.prototype|
|-|AnyClass.prototype||-|
|-|.method()||-|
|`.__proto__`|↑|↓|new AnyClass();|
|-|↑|↓|instantiation|
|-|anyClassChild||-|
|-|.method()||-|

- Arr(배열) 클래스와 인스턴스, 그리고 프로토타입의 관계

|---|:---:|---|---|
|-|Array||-|
|.constructor|↑|↓|.prototype|
|-|Array.prototype||-|
|-|.push() .slice .map .each...||-|
|`.__proto__`|↑|↓|new Array();|
|-|↑|↓|instantiation|
|-|anyClassChild||-|
|-|.push() .slice .map .each...||-|

> Array 역시 typeof를 했을 시 'object'타입으로 나오고, 비교 시 Array.isArray()로 배열지 확인해야되는 이유는 prototype을 이용한 prototype object를 가진 Object이기 때문이다. 그렇게 설계된거다. 그냥 그렇게 받아들이면된다.

## Prototype Chain

상속은 prototype chain을 사용한다.

```javascript
let inheritArr = new Array([1,23,4,5,123,...]);

inheritArr.length;
inheritArr.slice();
```

## MDN:Class in JavaScript

### 예제

```javascript
class Car {
  //생성자
  constructor(category, engine, transMission, wheel) {
    this.category = {
      fuel,
      body,
      usage
    };
    this.engine = engine;
    ...
  };

  //멤버 메서드
  break(){
    console.log('stop');
  };
  ...
}
```

> class는 내부적으로 프로토타입 상속으로 변환된다. [syntactic sugar](https://en.wikipedia.org/wiki/Syntactic_sugar)의 일종임

```javascript
class Jenesis extends Car{
  constructor(category, engine, transMission, grade, wheel, price, color....){
      //오우오우
      super(category, engine, transMission, wheel);

      this.grade = grade;
      ......
  }
}
```

> [Github:MDN/es2015-class-inheritance 예제](https://github.com/mdn/learning-area/blob/master/javascript/oojs/advanced/es2015-class-inheritance.html)

### Getter & Setter

```javascript
class Jenesis extends Car{
  constructor(category, engine, transMission, grade, wheel, price, color....){
      //오우오우
      super(category, engine, transMission, wheel);

      this.grade = grade;
      ......
  }

  get price(){
    return this._price;
  }

  set price(newPrice){
    this._price = newPrice;
  }
}

//사용측
const myCar = new Jenesis('sedan', 'v6', 'zf', '380', '20inch', 0, 'grey'....);

myCar._wheel; //20inch
myCar._price = 100;
myCar._price; //100;
```

> [Github:MDN/es2015-getters-setters 예제](https://github.com/mdn/learning-area/blob/master/javascript/oojs/advanced/es2015-getters-setters.html)

## 참조

> [MDN:Object/Prototype](https://developer.mozilla.org/ko/docs/Learn/JavaScript/Objects/Object_prototypes)   
> [MDN:JS/Classes](https://developer.mozilla.org/ko/docs/Web/JavaScript/Reference/Classes)