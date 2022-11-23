---
layout: post
title: "JavaScript Destructuring in ES6"
date: 2022-09-07
categories:
- JavaScript
tags:
- JavaScript
- ES6
- ECMAScript6(2015)
- spread
- rest
- destructuring
---

ES6에서 나온 문법들 중에 기존 문법들을 함축할 수 있는 문법들을 보면서 늘 든 생각이지만. 효율적이고 좋다. 알아보면 그렇고 모르면 아니다. 누구에게는 클린코드이고 누구에게는 아니다. 내가 더 알면 알 수 록 좋은것이 지식이다. 공부하자 :D

---

## Destructuring

구조분해할당은 배열이나 객체의 속성을 해체하여 그 값을 개별 변수에 담을 수 있게 하는 JavaScript의 Expression이다.

## Syntax

```javascript
let name, age, rest;
[name, age, ...rest] = ['ty',
    30,
    'sw', 'wd', 'dr', 'mm', 'bm'];

name;   //'ty'
age;    //30
rest;   //['sw', 'wd', 'dr', 'mm', 'bm']

//  ( {...} = {...} )  괄호를 빼면 syntax error ()필수 => 하단 객체에서 이미지 첨부
({name, age, ...rest} = {name: 'bulls', age: 30, univ: 'cs', job: 'mechanic'});
name; // bull
age; // 30
rest; // {univ: 'cs', job: 'mechanic'}
```

> 구조분해할당은 Perl, Python 등 다른 언어 기능

---

## 배열 구조 분해

### 1. 기본 변수 할당

```javascript
let height = [170, 186, 194];
let ['ty', 'poe', 'bulls'];
ty; //170
poe;    //186
bulls;  //194
```

### 2. 선언에서 분리한 할당

```javascript
let dt, nb;
[dt, nb] = ['win10', 'ubuntu20.04'];

dt; //win10
nb; //ubuntu20.04
```

### 3. 기본값

```javascript
[mtb = 150, road = 240] = [64];
mtb;    //64 undefined면 150 할당
road;   //240 undefined이기에 기본값으로 할당
//상기 모형이 약속이다.
const [a=1, b=2];   // syntax Error 구조할당 문법똑바로 써라고 해준다^^
const [a=1, b=2] = ['google'];  //const로 재선언 불가
```

### 4. 변수 값 교환(swap)

```javascript
let good = 'christ';
let evil = 'antichrist'

[good, evil] = [evil, good];
good;   // antichrist
evil;   // christ
//히익
```

> 일반 다른 언어에서 swap을 하고 싶으면 임시 변수를 따로 두어야한다.   
> [로우레벨 언어 XOR교체 트릭(XOR연산을이용한 처리과정)...Wikipedia](https://en.wikipedia.org/wiki/XOR_swap_algorithm)

### 5. 함수가 반환한 배열 분석

```javascript
const getBike = () => ['mtb', 'road', 'minivelo'];

let [mine, yours, lovely] = getBike();
mine;   //mtb
yours;  //road
lovely; //minivelo
```

### 6. 일부 반환 값 무시

```javascript
let [mine, , lovely] = getBike();
mine;   //mtb
lovely; //minivelo

let [,,] = getBike();   //모두무시

let [mine, ...yours] = getBike();
mine;   //mtb
yours;  //[road, minivelo]
```

### 7. 변수에 배열의 나머지를 할당

```javascript
let [mine, ...others] = ['AbsRing', 'goldenRing', 'silverRing', 'copperRing'];
mine;   //AbsRing
others; //['goldenRing', 'silverRing', 'copperRing']

//[a, b, ...c,] = [1,2,3,4,5]; syntaxError 발생 spread뒤 쉼표 금지
```

### [8. 정규 표현식과 일치하는 값 해제](https://developer.mozilla.org/ko/docs/Web/JavaScript/Reference/Operators/Destructuring_assignment#%EC%A0%95%EA%B7%9C_%ED%91%9C%ED%98%84%EC%8B%9D%EA%B3%BC_%EC%9D%BC%EC%B9%98%ED%95%98%EB%8A%94_%EA%B0%92_%ED%95%B4%EC%B2%B4%ED%95%98%EA%B8%B0)

---

## 객체 구조 분해 

### 1. 기본 할당

```javascript
let person = {name: 'ty', age: 30};
const {name, age} = person;

name;   //ty
age;    //30
```

### 2. 선언 없는 할당

```javascript
({name, age}) = {name: 'ty', age: 30};
```

> ![MDN](/assets/img/220909-destructuring-object-caution.png)

### 3. 새로운 변수 이름으로 할당

배열과는 달리 속성을 해체하여 객체의 원래 속성명과는 다른 이름의 변수에 할당이 가능하다.

```javascript
let {name: shortName, age: ageBeforeSevenYear} = person;
shortName;  //ty
ageBeforeSevenYear; // 30
```

### 4. 기본값

```javascript
let {state = 'normal', feel = 'stable'} = {state: 'upset'};
state;  //upset
feel;   //stable
```

### 5. 기본값 갖는 새로운 이름의 변수에 할당

```javascript
let {me: state = 'normal', you: feel = 'stable'} = {me: 'happy'};
state;  //happy
feel;   //stable
```

### 6. 함수 매개변수의 기본값 설정

```javascript
//MDN 예제 읽어볼것.

//ES5
function drawChart(options) {
  options = options === undefined ? {} : options;
  var size = options.size === undefined ? 'big' : options.size;
  var cords = options.cords === undefined ? { x: 0, y: 0 } : options.cords;
  var radius = options.radius === undefined ? 25 : options.radius;
  console.log(size, cords, radius);
  // 이제 드디어 차트 그리기 수행
}

//ES2015 MDN
function drawChart({size = 'big', cords = { x: 0, y: 0 }, radius = 25} = {}) {
  console.log(size, cords, radius);
  // 차트 그리기 수행
}

//사용은 동일
drawChart({
  cords: { x: 18, y: 30 },
  radius: 30
});
//매우 축약하였다. 물론 알면 보이고 안보이면 모르는건 현실
```

> ES2015의 파라메타의 내를 보면 빈객체를 할당하였는데, 없어도 상관없지만, 객체를 전달하지 않았을때도 사용가능하려면 객체를 할당하여 하는것을 더 유용하다고한다.   만약 객체임을 검증하는 코드를 심어서 오류를 던지거나, 이전에 이미 객체일때 동작하도록 verify 후 인자로 전달한다면 사실 크게 상관은 없을 것 같으나, MDN에서는 이방법을 더 유용하다고 표현하였다.   어디까지 에러로 볼 것인가는 기획과 개발, 유저의 입장에서 다 다를 것이지만. 그정도 구분은 명확하게 설계하여 들어간다면 이와같은 문제가 유용할 수도? 아닐수도 있을거라 생각한다.

### 7. 중첩된 객체 및 배열의 구조분해

```javascript
//MDN예제 읽어보면 어디서 분해해왔는지 알 수 있다.
var metadata = {
    title: "Scratchpad",
    translations: [
       {
        locale: "de",
        localization_tags: [ ],
        last_edit: "2014-04-14T08:43:37",
        url: "/de/docs/Tools/Scratchpad",
        title: "JavaScript-Umgebung"
       }
    ],
    url: "/en-US/docs/Tools/Scratchpad"
};

var { title: englishTitle, translations: [{ title: localeTitle }] } = metadata;

console.log(englishTitle); // "Scratchpad"
console.log(localeTitle);  // "JavaScript-Umgebung"
```

### 8. for of 반복문과 구조 분해

```javascript
//MDN 읽어보세요
for (var {name: n, family: { father: f } } of people) {
  console.log("Name: " + n + ", Father: " + f);
}

// "Name: Mike Smith, Father: Harry Smith"
// "Name: Tom Jones, Father: Richard Jones"
```

### 9. 함수 매개변수로 전달된 객체에서 필드 해체

```javascript
//MDN 예제 읽어서 어떻게 접근했는지 이해해야한다.
function userId({id}) {
  return id;
}

function whois({displayName: displayName, fullName: {firstName: name}}){
  console.log(displayName + " is " + name);
}

var user = {
  id: 42,
  displayName: "jdoe",
  fullName: {
      firstName: "John",
      lastName: "Doe"
  }
};

console.log("userId: " + userId(user)); // "userId: 42"
whois(user); // "jdoe is John"
```

### 10. 계산된 속성 이름과 구조 분해

```javascript
let key = 'id';
let { [key]: gID } = {id: 'suuor'};

gID;    //suuor
```

### 11. 객체 구조분해에서 Rest

```javascript
//MDN 대체 이정도까지의 문법을 무조건 써야하는 이유는 왜 안나와있지
let {a, b, ...rest} = {a: 10, b: 20, c: 30, d: 40}
a; // 10
b; // 20
rest; // { c: 30, d: 40 }
```

### 12. 속성 이름이 유효한 JavaScript 식별자명이 아닌 경우

```javascript
//쓰지 말라고하는 변수명을 쓸수있단 말을 하고있는거 같은데, 대체할 유효한 식별자명을 제공해라고한다.
const foo = { 'fizz-buzz': true };
const { 'fizz-buzz': fizzBuzz } = foo;

console.log(fizzBuzz); // "true"
```

---

> 유용한 것도 많았지만, 너무 복잡하고 지킬것이 많다. 사실 이전 프로젝트에서 람다와 안드로이드 최신기법이었던 jetpack을 적용하지 않았던 이유는 필요성이었다. 이런방식으로 코딩되어있는 코드를 해독하고 연구해야된다면 맞다. 무조건 알아야되고, 익숙해져야하는것이 필수다. 하지만 이런 문법들을 무조건 써야한다면 잘모르겠다. 회사라는건 나혼자 일하는 곳이라면 몰라도 여러사람이 일하는 곳인데, 이런 규약들을 다 적용해서 어디까지 쓰겠다는 약속을 하지 않으면, 누군가는 남들이 읽지 못하는 코드를 짜고 있을 것이다. 이전에 일을 가르쳐주던 팀장이 하던 말들이 이해되기 시작한다. 최신기술에 민감해야되는건 맞지만, 상용화되어 안정적으로 돌아가야될 서비스에 무턱대고 적용하고 쓰기에는 조금 위험한게 아닐까?

## 참조

> [MDN:JS/Destructuring](https://developer.mozilla.org/ko/docs/Web/JavaScript/Reference/Operators/Destructuring_assignment#%EA%B0%9D%EC%B2%B4_%EA%B5%AC%EC%A1%B0_%EB%B6%84%ED%95%B4)