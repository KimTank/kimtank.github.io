---
layout: post
title: "JavaScript String"
date: 2022-09-06
categories:
- JavaScript
tags:
- JavaScript
- String
- Syntax
- Indices
- Length
- Method
- Template-Literals
- Undefined
- Math
- random
---

문자열은 사람이 읽을 수 있는 언어를 나타내주는 중요한 정보이다. 실제로는 character, 문자의 모음으로 실질적으로는 메모리에는 결국 0과 1로 저장되겠지만, 유저가 읽고 받아들이려면 문자열이 없어서는 곤란하다.

# JavaScript String

문자의 모음, Strings of characters

## Syntax

```javascript
//(쌍)따옴표로 쌓여져있는 글자
let name = 'ty';
let nickName = "tank";
//let love = "cat is most lovely animal'; 해당구문은 error
```

## Indices & Length

- Indices: 지수, Numerical index
- Length: 길이

```javascript
let a = 'hello dumdum';
a[3];   // l
a[a.length] // index = length - 1 => a[a.length] overflow => undefined

a.length // 12 index => 0~11 ================> caution.1

//=================================> caution.2
let name = 'TaeYoon';
name = 'TAEYOON';
//=================================> caution.2 end

let number = 10;
let stringValue = 'ten';

let additionResult = number + stringValue; // 10ten
typeof additionResult;  // 'string
// number와 string을 JavaScript는 따로 처리하지 못하니, string으로 변환한다.
```

> ## caution
> 1. [C언어 배열의 범위를 넘어설때](https://blog.naver.com/PostView.nhn?isHttpsRedirect=true&blogId=tipsware&logNo=221054714926&categoryNo=50&parentCategoryNo=0&viewDate=&currentPage=1&postListTopCurrentPage=1&from=search)   
> 2. 상위 TaeYoon, TAEYOON은 전혀 다른 문자열이다. 메모리주소가 다르다. 한번에 한문자만 수동으로 업데이트할 수 없다. TAEYOON은 새 메모리를 가지는 새 문자열로 name변수에 덮어쓴다.

## String Methods

thing.method(...args);

string객체 내 내장된 instance는 length밖에 없지만, 구현되어있는 method()는 종류가 많으니, 가능하다면 MDN문서에서 확인하자.

- .toUpperCase(): 대문자로 변환
- .toLowerCase(): 소문자로 변환
- .trim(): 앞과 뒤의 공백을 날려준다. 어떻게 들어올지 모르는 유저의 입력값을 정제할때 사용.
- .indexOf(arg): 문자열에 주어진 인수가 나타내는 문자열 index와 그 자릿수를 반환
- .slice(0...): 문자열의 인수 부분을 잘라내서 **새로운 문자열**로 반환해 준다.

```javascript
let value = 'badboy is gone';
value.slice(6);     // ' is gone' => 6번째 부터
value.slice(0, 6);  // 'badboy' => 0~6전까지
value.slice(-4);    // 'gone' => 음수일 경우 뒤에서 1부터 4까지
```

> ### 중요
> .slice(0...)는 원래 문자열에 영향을 끼치지 않는다. mutable, immutable

- .replace(arg1, arg2): **정규표현식을 사용하여 제어할 수 있다.**, arg1은 기존 변경전 문자열또는 문자, arg2는 변경할 문자열또는 문자. 처음으로 매칭되는 값만 변경된다.(반복문을 사용하면 다 변경할수 있을거같다. .replaceAll(arg1, arg2)가 있긴하지만 브라우저별로 호환여부가 다르다. chrome 호환 안됨)
- .repeat('number type'): 반복하여 붙인다. 'abc'.repeat(3); => 'abcabcabc'. 새로운 문자열이 만들어지고 원본은 변하지 않는다.

## Template Literals

### Syntax

```javascript
let number = 10;
let unit = 'km';

console.log(`${number}${unit} left`); // 10km left
//동적으로 변경할 수 있다.
// ` back tick character
// ${3 * 4} 산술연산 가능
```

## Null & Undefined

둘다 단일한 값으로 비슷하지만 같은건 아니다.

### null

실제 JavaScript의 값이다. 일부러 값을 지정하지 않는 것. 아무것도 없는 상태. 다른 언어와는 다르게 JavaScript에서는 자주보는 값이 아니다. 직접 변수에 지정하는 값으로 쓰인다.

### undefined

정의된 값이 없는 값이다. "뭔값인지 모르겠어요^^". null이랑은 다르다. 아무것도 없는 상태(null) 자체가 아님. 가장 많이 쓰인다. 자연적으로 많이 쓰이게된다(일반 다른언어의 null처럼)

## Math Object

수학연산 모음을 모아놓은 객체이다.

- .PI: 원주율 3.141592653589793...
- .round(4.6): 반올림 결과값 5
- .abs(-465): 절대값 결과값 465
- .pow(2,3): 2의 3승 지수 결과값 8
- .floor(1.99999...): 내림 결과값 1
- .ceil(2.1): 올림 결과값 3
- .random(): 0~0.99999999999...  사이의 무언가
```javascript
//JavaScript의 Math.random();은 자연수를 반환하지 않는다.
//JS만의 자연수 반환 과정
const step1 = Math.random();
const step2 = step * 10;
const step3 = Math.floor(step2);

const step4 = step3 + 1;

const finalStep = Math.floor(Math.random() * 10) + 1;

//만들어 놓으면 쓰기 좋겠네(전역에 모듈화해서 심어놓고 슉슉)
const getRandom = () => Math.floor(Math.random() * 10) + 1;
```

> ## 참고
> [MDN:JS/String](https://developer.mozilla.org/ko/docs/Web/JavaScript/Reference/Global_Objects/String)   
> [MDN:JS/Template Literals](https://developer.mozilla.org/ko/docs/Web/JavaScript/Reference/Template_literals)   
> [MDN:JS/null](https://developer.mozilla.org/ko/docs/Web/JavaScript/Reference/Operators/null)   
> [MDN:JS/undefined](https://developer.mozilla.org/ko/docs/Web/JavaScript/Reference/Global_Objects/undefined)   
> [MDN:JS/Math](https://developer.mozilla.org/ko/docs/Web/JavaScript/Reference/Global_Objects/Math)