---
layout: post
title: "JavaScript Callback Function"
date: 2022-09-27
categories:
- JavaScript
tags:
- JavaScript
- Higher order function
- callback function
- Ansynchronous
- Asyncronous call
- Promise
- `then()`
---

괴물을 만났다. api를 어렵겠는데요 하더니 30초만에 짜버린다. 따라갈수 없으니 기초부터 잡고 코드리뷰를 해야겠다. 기초를 일단 보자.

생일을 핑계로 팽팽거리다 현우님한테 실례를 저질렀다. 새벽4시
벌받고있다

전화를 정지시킬까

# JavaScript Callback Function

1. 고차 함수는 전달인자(argument)로 함수를 넘겨줄 수 있다.(callback)
2. 고차 함수는 다른 함수를 리턴할 수 있다.(커링함수)
3. 함수를 리턴하거나, 함수를 전달인자로 받는 함수를 모두 고차함수라고한다.
4. 고차함수(커링, 콜백, ...)

고차함수에 callback함수 전달 -> if(조건(없을수도있음))고차함수 내 콜백함수 (여러번)(if false면 안)호출(invoke)

과거 api가 없을때 [underscore.js](https://underscorejs.org/), [lodash](https://lodash.com/)같은 라이브러리(배열이나 객체를 다루기위한 라이브러리)를 사용했다. 직접 구현해보고 비교하여 효율적인 코드를 배우자.

## 비동기(Asynchronous)

컴퓨터는 큐라던가 스택이라던가 요청처리의 방법이 자료구조에의해 처리되는걸로 배웠었는데, 하나의 작업을 시작하면 다음작업 요청이 대기열에서 기다리고 다음 작업 중 현재 처리되는 작업에는 간섭하지 못하는 **blocking**이 이루어진다고 배운적이 있다.

0번째 작업이 끝나고 다음 1번째 작업이 시작하는 시점이 같은 상황을 **동기적(synchronous)**이라고 한다. 

## 비동기 호출(Asynchronous Call)

- callback
    - 다른 함수의 전달인자(argument)로  넘겨주는 함수
    - 파라메타를 넘겨 받는 함수는 callback함수에 따라 sychronously(즉시실행)할수도 있고, anynchronously(나중에 실행)할수도 있다.
    - 예: iterator, event handler...
    - 함수 실행을 연결하는 것이 아니다. 함수 자체를 연결하는거다.

- 비동기 주요 사례
    - DOM Element event handler: click, keyup... -> DOM 강의
    - 페이지 로딩 DOMContentLoaded... -> DOM 런코 Note
- 타이머
    - 타이머API(setTimeout...) -> Timer API 강의
    - 애니메이션 API(requestAnimationFrame) -> [Web Animations API](https://developer.mozilla.org/en-US/docs/Web/API/Web_Animations_API)
- 서버에 자원 요청 및 응답
    - fetch API -> 서버 요청하기 강의
    - AJAX(XHR) -> [Ajax Getting Started](https://developer.mozilla.org/ko/docs/Web/Guide/AJAX/Getting_Started)

- 예제
```javascript
const printStirng = str => {
    setTimeout(
        () => {
            console.log(str)
        },
        Math.floor(Math.random() * 100) + 1
    )
}

//CBA ACB BCA 등 랜덤하게 실행
const printAll = () => {
    printString('A');
    printString('B');
    printString('C');
}

//콜백을 사용하여 순차적 실행 가능
const stepByStep = (str, callback) => {
    setTimeout(
        () => {
            console.log(str)
            callback()
        },
        Math.floor(Math.random() * 100) + 1
    )
}

//1,2,3 순차적으로 실행
const stepAll = () => {
    stepByStep('1', () => {
        stepByStep('2', () => {
            stepByStep('3', () => {
            })
        })
    })
}

//에러 처리 기법
const eventAnyThing = (callback) => {
    ...

    if(isStable)
        callback(null, stable);
    
    if(isUnstable)
        callback(unstable, null);
}

// usage
eventAnyThing((err, data) => {
    if(err){
        console.log('err');
        return 0;
    }
    return data;
})

//주의 Callback Hell(feat. in the deep depth)
const welcomeToHell = (greetings) => {
    ...
    return (crossTheRiver) => {
        goDeep(greetings, hello('Bael'), () => {
            ...
            goDeep(greetings, hello('Agares'), () => {
                ...
                goDeep(greetings, 'Vassago', () => {
                    ...infinity
                })
            })
        })
    }
}
```

## Promise

콜백지옥(if문지옥과 비슷하자나)을 벗어날 수 있는 callback chain

```javascript
const goToHeaven = (Haaaappppyyyy) => {
    return new Promis((resolve, reject) => {
        setTimeout(
            () => {
                console.log(Haaaappppyyyy);
                resolve()
            },
            Math.floor(Math.random() * 100) + 1
        )
    })
}

const meetTheRapGod = () => {
    goToHeaven('8mile')
    .then(() => {
        return goToHeaven('mockingbird')
    })
    .then(() => {
        return goToHeaven('stan')
    })
    .then(() => {
        return goToHeaven('lose yourself')
    })
    ...
}
//if문지옥을 벗어나기위한 if문 clean코드나 switch문같다?

//하지만 Promise도 잘못사용하면 지옥불에 뛰어드는 천지모르는 바보들과 똑같다 ㅉㅉ
const goToTheLoveAndWar = () => {
    return new Promise((resolve, reject) => {
        setTimeout(() => { resolve('after we will meet 4weeks later')}, 100);
    });
}

const humanWhoWantTrueLove = () => {
    return new Promise((resolve, reject) => {
        setTimeout(() => { resolve('want my endless harf')}, 100);
    });
}

const humanWhoWantMoney = () => {
    return new Promise((resolve, reject) => {
        setTimeout(() => { resolve('want to have partner who earn much money')}, 100);
    });
}

const trashWhoWantForEnjoy = () => {
    return new Promise((resolve, reject) => {
        setTimeout(() => { resolve('trash is just animal')}, 100);
    });
}

...we dont know about our life what happend chaos events...

goToTheLoveAndWar()
.then(meeting => {
    console.log(meeting);

    humanWhoWantTrueLove()
    .then(married => {
        console.log(married);

        humanWhoWantMoney()
        .then(cheating => {
            console.log(cheating);

            trashWhoWantForEnjoy()
                .then((... => {
                console.log(...);

                ...()
                .then(...dont worry ur not the only one.)
            })
        })
    })
})

//사람을 만나는것과 같이 잘못사용하면 안하니만 못하다(못하는게 나을지도 주륵..).

//Primise Chanining 
//  -> 우리가 랩신인 에미넴선생님을 영접하는 그날같이 존경심을 담아 CleanCode를 작성해야한다.
//최신기법(node 버전이 높아야한다.)
const respectForTheEminem = async () => {
    const awesomeRabbit = await goToHeaven('8mile');
    console.log(awesomeRabbit);

    const lovelyHaily = await goToHeaven('mockingbird');
    console.log(lovelyHaily);


    const lolJohn = await goToHeaven('stan');
    console.log(lolJohn);

    const oneShotOneOpportunity = await goToHeaven('lose yourself')
    console.log(oneShotOneOpportunity);
    ...
}
```

> ## Timer API
> 
> - setTimerout(callback, milisecond): 일정 시간 후 함수 실행(1_000 -> 1초)
>   - 매개변수(param): 실행할 함수, 대기 시간
>   - return val: 임의의 타이머 ID
>    
> - clearTimeout(timerId): setTimeout타이머 종료
>   - 매개변수(param): 타이머 ID
>   - return val: none
>    
> - clearInterval(timerId) setInterval(callback, millisecond): setTimeout타이머 종료
>   - 매개변수(param): 실행할 함수, 반복 간격밀리초
>   - return val: 임의 타이머ID
>    
> - clearInterval(timerId): setInterval 타이머 종료
>   - param: 타이머ID
>   - return val: none

> ## 참조  
> [MDN:Event Loop](https://developer.mozilla.org/ko/docs/Web/JavaScript/EventLoop)   
> [Philip Roberts:Help, I'm stuck in an event-loop](https://vimeo.com/96425312)   