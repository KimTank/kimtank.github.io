---
layout: post
title: "즐거운 소수"
date: 2022-08-24T00:00:00-00:00
categories:
- WebFront
tags:
- JavaScript
- codestates
- algorythm
---
// 소수 : 수학에서 1과 그수 자신 이외의 자연수로는 나눌 수 없는, 1보다 큰 자연수 
// 1. 1보다 커야 한다.
// 2. 2를 제외한 짝수는 소수가 아니다. (2는 소수)
// 3. 3부터 자기 자신(num) 전까지 for문으로 반복해서 나누어 떨어지는 경우가 있으면 소수가 아니다.

function isPrime(num) {
// 1이면 소수가 아니다.
  if (num === 1) {
    return false;
  }
  // 짝수는 소수가 아니지만, 2는 소수다.
  if (num === 2) {
    return true;
  }
  // 짝수는 소수가 아니다.
  if (num % 2 === 0) {
    return false;
  }
  // 1부터 자기 자신(num) 전까지 for문으로 반복하면서 나누어 떨어지는 경우가 있으면 소수가 아님
  for (let i = 3; i < num; i++) {
    if (num % i === 0) {
      return false;
    }
  }
  // 이외에는 나머지는 다 소수다.
  return true;


  // 소수 : 수학에서 1과 그수 자신 이외의 자연수로는 나눌 수 없는, 1보다 큰 자연수 
// 1. 1보다 커야 한다.
// 2. 2를 제외한 짝수는 소수가 아니다. (2는 소수)
// 3. 3부터 자기 자신(num) 전까지 for문으로 반복해서 나누어 떨어지는 경우가 있으면 소수가 아니다.
function isPrime(num) {
  // 1. 1보다 커야 한다.
  if (num === 1) {
    return false;
  }
  // 2-1. 2는 소수다.
  if (num === 2) {
    return true;
  }

  // 2-2. 2를 제외한 짝수는 소수가 아니다.
  if (num % 2 === 0) {
    return false;
  }

  // 3. 3부터 num의 제곱근까지만 반복해도 나누어 떨어지는 수가 있으면 소수가 아니다.
    // num이 36일 경우 36을 구하는 방법(약수의 곱)
  // 1 * 36, 2 * 18, 3 * 12, 4 * 9, 6 * 6, 9 * 4, 12 * 3, 18 * 2, 36 * 1
  // 36의 제곱근(6)끼리의 곱을 기준으로 좌우 대칭을 이룬다. 
  // 즉, 제곱근보다 작은 수 중에 약수가 없다면, 큰 수 중에도 약수가 있을 수 없다.
  for (let i = 3; i <= parseInt(Math.sqrt(num)); i++) {
    // num이 17일 때, parseInt(Math.sqrt(17))은 4
    if (num % i === 0) {
      // 17 % 3 === 2
      // 17 % 4 === 1 => 제곱근보다 작은 수 중에 약수(나누어 떨어지는 수)가 없으므로, 17은 소수이다.
      return false;
    }
  }
  return true;
}



// 17번 문제는 수를 받아서 그게 소수인지 여부만 확인
// 18번 문제는 수를 받아서 그거보다 작은 수를 다 탐색 -> 소수인지 확인해서 누적한 문자열로 반환
// 18 => '2-3-5-7-11-13-17'
function listPrimes(num) {
  // 2는 이미 소수인 걸 알고 있기 때문에 '2'를 할당한 변수 만들기
  let result = '2';
  // 첫번째 반복문 : 3부터 num까지 수를 모두 탐색
  for(let prime = 3; prime <= num; prime+=2) {
    let isPrime = true;
    // 숫자를 다확인할 필요가 없다. 소수인지 확인하려면 제곱근기준으로 앞까지만 확인하면 된다!
    let sqrt = parseInt(Math.sqrt(prime))
    for (let i = 3; i < sqrt; i+=2) {
      // 만약 prime을 i로 나눴을 때 나누어 떨어지면, 그건 소수가 아니다.
      // 제곱근이 3 이하인 홀수
      // 9보다 작은 홀수는 제곱근이 3보다 작다.
      if(prime % i === 0) {
        // prime 9일 때, 9의 제곱근 3
        // 9 % 3 === 0 => 9는 소수가 아니다.
        // 11 % 3 === 2
        // 9부터 16까지 제곱근이 4미만인 수  //16의 제곱근이 4// 16보다 작은 수의 제곱근은 4보다 작다.
        // 13 % 3 === 1
        // 15 % 3 === 0;
        // 17 % 3 === 2;
        isPrime = false;
        break;
      }
    } 
    if(isPrime === true) {
      result = result + `-${prime}`
      // result = `${result}-${prime}`
    }
  }
  return result;
}




> 
> ### 참고_Mozilla.org_
> - [`for...of`](https://developer.mozilla.org/ko/docs/Web/JavaScript/Reference/Statements/for...of)
> - [`forEach`](https://developer.mozilla.org/ko/docs/Web/JavaScript/Reference/Global_Objects/Array/forEach)
> - [`rest parametes`](https://developer.mozilla.org/ko/docs/Web/JavaScript/Reference/Functions/rest_parameters)
> - [`instanceof`](https://developer.mozilla.org/ko/docs/Web/JavaScript/Reference/Operators/instanceof)
> - [`addition assignment`](https://developer.mozilla.org/ko/docs/Web/JavaScript/Reference/Operators/Addition_assignment)
> 