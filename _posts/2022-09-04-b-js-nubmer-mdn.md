---
layout: post
title: "JavaScript Number MDN"
date: 2022-09-04
categories:
- JavaScript
tags:
- Javascript
- Number
- MDN-Doc
---
고마운 사람들 결혼식 갔다가 뒷풀이로 주말에도 공부해야지 하는 마음으로 결혼식장에 장비 다챙겨갔다가 고이 가져간 그대로 사용도 안하고 숙취로 집에 들어온 후 눈을 뜨니 일요일 오후였다. ^^ 좋은 뒷풀이였지만 쉬는 날이 가장 공부하기 좋은 기회란걸 무엇보다 잘 알고 있으니, 공부하자!!

# JavaScript Number

## Number
- 37이나 -9.25와 같은 숫자를 표현하고 다룰때 사용하는 [원시 래퍼 객체](https://developer.mozilla.org/ko/docs/Glossary/Primitive#primitive_wrapper_objects_in_javascript)
- 숫자를 다루기위해 상수와 메서드를 내장하고 있다.
- Number() 함수를 사용하여 'number'타입으로 파싱이 가능하다.
- Java와 C#의 double타입처럼 [IEEE 754 64비트 바이너리 배정 밀도](https://en.wikipedia.org/wiki/Floating-point_arithmetic)값이다.
> 분수값을 나타낼 수 있지만 저장할 수 있는 값에는 몇가지 제한이 있다.   
> 소수점 이하 17자리 정도만 유지하며 산술은 [반올림](https://en.wikipedia.org/wiki/Floating-point_arithmetic#Representable_numbers,_conversion_and_rounding)의 대상이 된다.   
> 가장 큰 값은 1.8E308이고, 더 큰 값은 [Infinity](https://developer.mozilla.org/ko/docs/Web/JavaScript/Reference/Global_Objects/Infinity)
- JavaScript 코드에서 37과 같은 숫자 리터럴은 정수가 아니라 보동 소수점 값이다. 별도의 정수형은 없다.
> [BigInt](https://developer.mozilla.org/ko/docs/Web/JavaScript/Reference/Global_Objects/BigInt)타입이 있지만 Number를 대체하도록 설계되지 않았다. 37은 Number일뿐 Bigint가 아니다.(BigInt는 n을 붙여 사용 ex: 10n)
- Number는 0b101, 0o13, 0x0A와 같은 리터럴 형식으로 표현될 수 도 있다. [더알아보기](https://developer.mozilla.org/ko/docs/Web/JavaScript/Reference/Lexical_grammar#numeric_literals)

## Description
Number()함수를 사용하면 문자열이나 다른 값을 Number타입으로 변환한다. 만약 인수를 숫자로 변환할 수 없으면 [NaN](https://developer.mozilla.org/ko/docs/Web/JavaScript/Reference/Global_Objects/NaN)으로 리턴한다.

### 리터럴 구문
```javascript
123;
123.0;//상기와 동일
123 === 123.0; // true
```
### 함수 구문
```javascript
Nubmer('123'); //number타입 123 반환
Number('123') === 123; // true

Number('stringValue'); // NaN
Number(undefined); //NaN
```

## Constructor
- Number()
- Number()생성자는 Number객체를 생성한다.

> [Number()생성자 더알아보기](https://developer.mozilla.org/ko/docs/Web/JavaScript/Reference/Global_Objects/Number/Number)

### Syntax
```javascript
const numberObject = new Number(value);
```

### 매개변수
- value: 만들어질 객체의 숫자 값.

### Number 객체 만들기
```javascript
const numObj = new Number('123'); //numObj === 123 false
const numPrimitiveType = Number('123'); //numPrimitiveType === 123 true;
numObj instanceof Number; //true
numPrimitiveType instanceof Number; // true
```

## [Static properties](https://developer.mozilla.org/ko/docs/Web/JavaScript/Reference/Global_Objects/Number#static_properties)
- .EPSILON: 두개의 표현 가능한 숫자 사이의 최소간격
- .MAX_SAFE_INTEGER: JS에서 안전한 최대 정수(2^53 -1)
- .MAX_VALUE: 표현 가능한 가장 큰 양수
- .MIN_SAFE_INTEGER(-(2^53 -1))
- .NaN: Not a Number 특별한 `값`
- .NEGATIVE_INFINITY: 음의 무한대를 나타내는 특수한 값. 오버플로우 시 반환.
- .POSITIVE_INFINITY: 양의 무한대를 나타내는 특수한 값. 오버플로우시 반환된다.
- [.prototype](https://developer.mozilla.org/ko/docs/Web/JavaScript/Reference/Global_Objects/Number): Number객체에 속성을 추가하게 상속할 수 있도록 구현되어 있는거 같다.

## [Static Method](https://developer.mozilla.org/ko/docs/Web/JavaScript/Reference/Global_Objects/Number#%EC%A0%95%EC%A0%81_%EB%A9%94%EC%86%8C%EB%93%9C)
- .isNaN(): NaN인지 확인
- .isFinite(): 유한수인지 확인
- .isInteger(): 정수인지 확인
- .isSafeInteger(): 안전한 정수(-(2^53 -1)과 2^53-1 사이의 정수)인지 확인
- .parseFloat(string): 전역 객체 parseFloat()과 동일한 값
- `.parseInt(string, [radix])`: 전역 객체 parseInt()와 동일한 값

## [Instance Method](https://developer.mozilla.org/ko/docs/Web/JavaScript/Reference/Global_Objects/Number#%EC%9D%B8%EC%8A%A4%ED%84%B4%EC%8A%A4_%EB%A9%94%EC%86%8C%EB%93%9C)

기본타입 모형: Number.prototype 이후 .메서드()
- .toExponential(fractionDigits): 지수 표기법으로 표기된 문자열을 반환
- .toFixed(digits): 고정 소수점 표기법으로 숫자를 표현하는 문자열을 반환
- `.toLocaleString([locales[, options]])`: 이 숫자를 해당 언어 방식으로 표현된 문자열을 반환(Object.prototype.toLocaleString() 메서드를 재정의)
- .toPrecision(precision): 고정 소수점 또는 지수 표기법으로 지정된 정밀도로 숫자를 표현하는 문자열을 반환
- `.toString([radix])`: 지정한 기수("base")에서 지정한 개체를 표현하는 문자열을 반환(Object.prototype.toString() 메서드를 재정의)
- .valueOf(): 명시된 객체의 원시 값을 반환(Object.prototype.valueOf() 메서드를 재정의)

## Example

### Number 객체를 사용해 숫자형 변수에 할당

```javascript
const biggestNum = Number.MAX_VALUE;
const smallestNum = Number.MIN_VALUE;
const infiniteNum = Number.POSITIVE_INFINITY;
const negInfiniteNum = Number.NEGATIVE_INFINITY;
const noANum = Number.NaN;
```

### Number의 정수 범위

Number객체가 표현할 수 있는 정수의 최소값과 최대값을 보여준다.

```javascript
const biggestInt = Number.MAX_SAFE_INTEGER; //  (2**53 - 1) =>  9007199254740991
const smallestInt = Number.MIN_SAFE_INTEGER; // -(2**53 - 1) => -9007199254740991
```

> [ECMAScript 표준, 6.1.6 The Number Type](https://tc39.github.io/ecma262/#sec-ecmascript-language-types-number-type)

JSON으로 직렬화한 데이터를 읽을 때, 위 범위를 벗어나는 수는 JSON분석기의 Number 형변환 시 손상될 수 있다. 이 때 [String](https://developer.mozilla.org/ko/docs/Web/JavaScript/Reference/Global_Objects/String)을 대신 사용하는 것도 대안이다.   
더 큰 수는 [BigInt](https://developer.mozilla.org/ko/docs/Web/JavaScript/Reference/Global_Objects/BigInt)타입으로 표현할 수 있다.

### Number를 사용해 Date객체 숫자로 변환

Number를 함수로 사용하여 [Date](https://developer.mozilla.org/ko/docs/Web/JavaScript/Reference/Global_Objects/Date) 객체를 숫자 값으로 변환한다.

```javascript
let d = new Date('December 17, 1995 03:24:00');
console.log(Number(d));
// 819199440000가 기록된다.
```

### 숫자형 문자열에서 숫자로 변환
```javascript
Number('123'); // 123
Number('123') === 123; // true
Number('12.3'); // 12.3
Number('12.00'); // 12
Number('123e-1'); // 12.3
Number(''); // 0
Number(null); // 0
Number('0x11'); // 17
Number('0b11'); // 3
Number('0o11'); // 9
Number('foo'); // NaN
Number('100a'); // NaN
Number('-Infinity'); // -Infinity
```

## Specification
[ECMAScript Language Specification # sec-number-objects](https://developer.mozilla.org/ko/docs/Web/JavaScript/Reference/Global_Objects/Number#%EC%98%88%EC%A0%9C)

> ## 주의
> 
> 본 포스팅은 MDN:JavaScript/Number 문서를 내가 알아 보기 쉽도록 정리한 것으로 Last Modified는 2022/08/05이다. 본 포스팅은 따로 업데이트 하지 않는 이상 시간이 지나면 legacy할 수 있다. 가능하다면 항상 최신화가 이루어지는 MDN:DOC을 이용해야한다.
> 
> ## 참조
> [MDN:JavaScript/Number](https://developer.mozilla.org/ko/docs/Web/JavaScript/Reference/Global_Objects/Number#%EC%98%88%EC%A0%9C)