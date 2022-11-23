---
layout: post
title: "JavaScript Object"
date: 2022-09-15
categories:
- JavaScript
tags:
- JavaScript
- Object
- Literal
- Initializer
- Prototype
- Inheritance
- prototype-chain
---

코드스테이츠의 실질적 강의세션 1학년은 끝이났다. 처음에 방만하게 조금 아는내용이라고 다른거랑 병행했던 처음부터, 추후 코드스테이츠의 커리큘럼만 따라오던 나중까지. 내실력과 위치를 더 잘 파악할 수있었다. 늦었다고 수박겉햝기식으로 진도만 주구장창 나가고 쓸줄은 알지만 정확하게 쓸줄은 모르는게 늦었기때문에 어쩔 수 없어 라고 생각했던. 코드스테이츠의 강의를 듣기 전에는 몰랐다. 사실 어떤 교육(평생을 살면서 배우는)이든 떠먹여주는건 없다. 쪽찝게과외라도 결국 내가 이해하거나 외워야한다. 다행이도 프로그램개발에서의 몽키코더는 누구나 될수있다(밥은 안굶을 수 있다.). 하지만 누구나 꿈꾸고 뉴스에 나오는 네카??뭐는 참 어렵다. ㅁㅁ위키만 보더라도 1프로의 개발자와 99프로의 코더가 개발시장에 있다고한다. 나는 어디인지 깨달을때까지 공부한다. 미뤄왔던 객체 가자.

---

## Object

일정의 구조에 데이터들을 저장할 수 있다. key와 value의 pair로 이루어져있다. 복잡한 entity를 저장하는데 사용한다. JavaScript의 거의 모든 객체는 Object의 인스턴스이다. 일반적 객체는 Object.prototype에서 속성과 메서드를 상속하지만, 이러한 속성들은 재정의 될 수 있다. 하지만 Object는 의도적으로 재정의되지 않게 생성되거나, 변경될 수 있다(Object.create(null), Object.setPrototypeOf, 등)

이런 변경사항은 해당 변경의 대상이되는 프로토타입 체인상의 속성과 메서드가 추가로 재정의되지 않으면 프로토타입 체인을 통해 모든 객체에서 쓸 수 있다. 객체의 동작을 재정의하여 확장에는 강력하나, 잠재적 크리티컬 이슈를 제공한다.

Object 생성자는 주어진 값에 대한 객체 래퍼를 생성한다. 값이 null또는 undefined면 빈객체를 생성하여 반환한다. 그렇지 않으면 주어진 값에 해당하는 타입의 객체를 반환한다. 값이 이미 객체인 경우 그 값을 반환한다. 생성자가 아닌 호출이면 Object는 new Object()와 동일하게 동작한다.

## Constructor

### Object() 생성자

Object(): 새 객체를 만든다. 이때 생성된 객체는 주어진 값에 대한 래퍼이다.

### Object Literal

```javascript
//배열은 순서가 있지만 각 인덱스가 어떤 의미인지는 알 수 없다.
const someArray = [101, 102, 3_000, 200, 1...];

//객체는 key와 value로 쌍을 이루어 정보를 한눈에 파악 할 수 있다.
const myInfo = {
    name: 'ty',
    age: 37,
    position: 'tanker',
    hobby: 'crazy things',
    ...
};
```

> 배열도 객체처럼 이중배열로 만들수는 있겠만. 객체가 있는 이상은 비효율적이다.

## Static Method

- .assign(): 하나 이상의 원본 객체들로부터 모든 열거 가능한 속성들을 대상 객체로 복사한다.
- .create(): 지정한 프로토타입의 객체 및 속성을 갖고 있는 새 객체를 생성한다.
- .defineProperty(): 지정한 서술자(descriptor)에서 서술한 속성을 객체에 추가한다.
- .defineProperties(): 지정한 서술자들에게 서술한 속성을 객체에 추가한다.
- .entries(): 지정한 객체 자신의 모든 열거 가능한 문자열 속성들의 [key, value] 쌍으로 구성된 배열을 반환한다.
- .freeze(): 객체를 고정한다. 다른 곳의 코드에서 해당 속성을 삭제하거나 변경할 수 없다.
- .fromEntries(): [key, value]쌍의 iterable로부터 새 객체를 반환한다.(.entries의 반대로 작용)
- .getOwnPropertyDescriptor(): 지정한 속성에 대한 속성 서술자를 반환한다.
- .getOwnPropertyDescriptors(): 객체 자신의 모든 속성 서술자들로 구성된 객체를 반환한다.
- .getOwnPropertyNames(): 객체 자신의 모든 열거가능하거나 불가능한 속성들의 이름으로 구성된 배열을 반환한다.
- .getOwnPropertySymbols(): 지정한 객체 자신의 모든 심볼 속성들로 구성된 배열을 반환한다.
- .getPrototypeOf(): 객체의 프로토타입(내부 `[[Prototype]]` 속성)을 반환한다.
- .is(): 두 값이 같은지를 비교한다. 모든NaN값을 같다고 처리한다.(추상 동등 비교 및 엄격한 동등 비교와 다른점이다.)
- .isExtensible(): 객체의 확장이 가능한지 여부를 확인한다.
- .isFrozen(): 객체가 고정되었는지여부를 확인한다.
- .isSealed(): 객체가 봉인되었는지 여부를 확인한다.
- .keys(): 지정한 객체 자신의 모든 열거 가능한 문자열 속성들의 이름으로 구성된 배열을 반환한다.
- .preventExtensions(): 확장되지 못하게한다.
- .seal(): 다른 코드가 객체의 속성을 삭제하지 못하도록 한다.
- .setPrototypeOf(): 객체의 프로토타입(내부`[[Prototype]]`속성)을 설정한다.
- .values(): 자신의 모든 열거 가능한 문자열 속성에 해당하는 값들로 구성된 배열을 반환한다.

## Instance Property

- .prototype.constructor: 프로토타입을 생성하는 함수를 지정한다.
- `.prototype.__proto__`: 객체가 인스턴스화될때 프로토타입으로 사용된 객체를 가르킨다.

## Instance Message

- `.prototype.__defineGetter__()`: 엑세스(get)할 때 실행되어 값을 반환하는 함수와 지정한 속성을 연결한다.
- `.prototype.__defineSetter__()`: 설정(set)할 떄 실행되어 해당 속성을 수정하는 함수와 지정한 속성을 연결한다.
- `.prototype.__lookupGetter__()`: `__defineGetter__()`메서드에 의해 지정된 송성과 연결된 함수를 반환한다.
- `.prototype.__lookupSetter__()`: `__defineSetter__()`메서드에 의해 지정된 속성과 연결된 함수를 반환한다.
- .prototype.hasOwnProperty(): 지정한 속성이 해당 객체에 직접 포함되어 있고 프로토타입 체인을 통해 상속되지 않는지 여부를 불리언값으로 반환한다.
- .prototype.isPrototypeOf(): 호출한 객체가 지정한 객체의 프로토타입 체인에 있는지 여부를 불리언 값으로 반환한다.
- .prototype.propertyIsEnumerable(): ECMAScript `[[Enumerable]]`속성이 설정되었는지 여부를 불리언 값으로 반환한다.
- .prototype.toLocaleString(): toString()을 호출한다.
- .prototype.toString(): 객체의 문자열 표현을 반환한다.
- .prototype.valueOf(): 원시값을 반환한다.

## Access Object

```javascript
const someObj = {
  a: ...,
  b: ...,
  c: ...,
  ...
}

//2가지 방법, 점구문, 대괄호구문
someObj.a;  //...value
someObj["b"]; //...value
```

객체에 입력된 모든 key는 문자열로 바뀐다.

## Object modify

```javascript
const anyObj = {
  a: ...,
  b: ...,
  c: ...
  ...
}

anyObj.a = ....;
anyObj['b'] = ....;
```
## Complex

```javascript
//리스트에 뿌려줄 정보를 배열에 담을 수 있다.
const clxArr = [
    {category: 'cycle', price: 2_500_000},
    {category: 'mtb', price: 5_000_000},
    {category: 'component', price: 8_900_000},
    {category: 'wheel', price: 20_000_000},
    ...
];

//배열내 계층구조를 만들 수 있다.
const clxObj = {
  brand: 'Specialized',
  category: 'Cycle Cross',
  modelName: ['S-work', 'cx-7000', 'cx-6000d', ...],
  specPrice: {
    duraAceDi2: 17_000_000,
    redETap: 20_000_000,
    ultegraDi2: 14_000_000,
    forceETap: 16_000_000,
    ...  
  }
  warranty: 1
  ...
}

//다양한 정보를 커스텀하게 담을 수 있다.
```

## Object Prototype

Object.prototype 메서드 동작 변경은 기존 내용의 앞이나 뒤에 확장할 내용을 래핑하여 코드를 주입하는걸 고려해야한다. 만들어놓고 돌려보지 않은 코드는 기본 제공코드 또는 다른사람의 확장이 실행되기 전 사전 조건부로 사용자 정의 코드를 실행한다.

함수가 호출되면 호출에 대한 매개변수가 유사배열 arguments 객체에 보관된다. someFunction(a, b, c)호출 시 본문 내의 arguments 객체에 (a, b, c) 3개의 유사배열 요소가 포함된다.

hook을 통해 프로토타입을 수정하고자 할 때는 해당 함수에서 apply()를 호출하면서 this와 arguments객체를 현재 동작에 전달한다. Node.prototype, Function.prototype 등 모든 프로토타입에 적용가능하다.

```javascript
var current = Object.prototype.valueOf;
//내가 지정한 -prop-value 범분야에 사용
//항상 동일한 프로토타입 체인에 있지 않기 떄문에, Object.prototype을 수정할거다.
Object.prototype.valueOf = function() {
  if(this.hasProperty('-prop-value'))
    return this['-prop-value']
} else {
  /* 내가 만든 객체는 아니다.
  가능한 원래의 동작재현하여 기본동작으로 돌아갈거다.
  apply메서드는 다른 언어에서 super처럼 작용한다.
  valueOf()가 arguments를 가지고 있지 않더라도, 다른 hook이 있을게 */
}
```

JavaScript에는 명확한 하위 클래스 객체가 없다. 프로토타입은 특정 기능의 기본클래스객체를 만드는데 좋다.

```javascript
//사람객체(대문자) 이름넣으면 말할수있다 참
var Person = function (name) {
  this.name = name;
  this.canTalk = true;
}

//객체의 프로토타입 환영해 말할 수 있으면 콘솔 안녕 나는 이름이야
Person.prototype.greet = function () {
  if (this.canTalk) {
    console.log('Hi, I am ' + this.name);
  }
};

//고용인은 name을 전달하여 뭘하는 도중에 제목을 넣으셨네
var Employee = function (name, title) {
  Person.call(this, name);
  this.title = title;
};

//고용인의 프로토타입에 Object.create()함수로 사람프로토타입=========================================
Employee.prototype = Object.create(Person.prototype);
Employee.prototype.constructor = Employee; 
// Object.prototype.constructor를 Employee로 설정하지 않으면
// Person (parent)의 prototype.constructor를 사용합니다.
// 이를 피하기 위해 prototype.constructor를 Employee (child)로 설정합니다.

//고용인 환영해 말할수있으면 콘솔 안녕 이름이야, 직업
Employee.prototype.greet = function () {
  if (this.canTalk) {
    console.log('Hi, I am ' + this.name + ', the ' + this.title);
  }
};

//고객 불러 이름
var Customer = function (name) {
  Person.call(this, name);
};

//고객 프로토타입 사람 생성자
Customer.prototype = Object.create(Person.prototype);
Customer.prototype.constructor = Customer; // Object.prototype.constructor를 Customer로 설정하지 않으면
// Person (parent)의 prototype.constructor를 사용합니다.
// 이를 피하기 위해 prototype.constructor를 Customer (child)로 설정합니다.

//마임 사람 불러 이름 말못해
var Mime = function (name) {
  Person.call(this, name);
  this.canTalk = false;
};

//마임 만들어 사람을 이용해서 하지만 말못해
Mime.prototype = Object.create(Person.prototype);
Mime.prototype.constructor = Mime;
// Object.prototype.constructor를 Mime로 설정하지 않으면
// Person (parent)의 prototype.constructor를 사용합니다.
// 이를 피하기 위해 prototype.constructor를 Mime (child)로 설정합니다.

//밥은 고용인이고 직업은 빌더야
var bob = new Employee('Bob', 'Builder');

//조는 손님이야
var joe = new Customer('Joe');

//알지는 난해한색이고 직업은 핸디맨?이야
var rg = new Employee('Red Green', 'Handyman');

//마이크는 고객이야
var mike = new Customer('Mike');

//마임은 말못해
var mime = new Mime('Mime');

//밥환영해
bob.greet();
// Hi, I am Bob, the Builder

//조 환영해
joe.greet();
// Hi, I am Joe

//알지 환영해
rg.greet();
// Hi, I am Red Green, the Handyman

//마이크 환영해
mike.greet();
// Hi, I am Mike


//마임 말못해
mime.greet();
```

## 참조

> [MDN:JS/Operator/Object_initializer](https://developer.mozilla.org/ko/docs/Web/JavaScript/Reference/Operators/Object_initializer)   
> [MDN:JS/Functions/arguments](https://developer.mozilla.org/ko/docs/Web/JavaScript/Reference/Functions/arguments)   
> [MDN:Prototype](https://developer.mozilla.org/en-US/docs/Glossary/Prototype)   
> [MDN:JS/Inheritance & the prototype chain](https://developer.mozilla.org/ko/docs/Web/JavaScript/Inheritance_and_the_prototype_chain)   
> [MDN:JS/Global_Object/Object](https://developer.mozilla.org/ko/docs/Web/JavaScript/Reference/Global_Objects/Object)   
