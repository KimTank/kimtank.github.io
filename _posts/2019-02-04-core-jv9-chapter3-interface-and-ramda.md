---
layout: post
title: "인터페이스와 람다식"
date: 2019-02-04T00:00:00-00:00
categories:
 - Java
tags:
 - interface
 - ramda
 - corejava
 - 카이 호스트만
---

1. 인터페이스는 구현 클래스에서 반드시 구현해야 하는 메서드를 명시함.
2. 인터페이스는 해당 인터페이스를 구현하는 모든 클래스의 슈퍼타입. 따라 구현 클래스의 인스턴스를 인터페이스 타입 변수에 할당 가능
3. 인터페이스는 정적 메서드를 포함가능, 인터페이스 모든 변수는 자동으로 public static final임.
4. 인터페이스는 구현 클래스에서 상속하거나 오버라이드할 수 있는 기본 메서드를 포함할 수 있음.
5. 인터페이스는 구현 클래스에서 호출하거나 오버라이드할 수 없는 비공개 메서드를 포함 할 수 있다.
6. `Comparable`과 `Comparator`인터페이스는 객체 비교에 사용함.
7. 함수형 인터페이스는 단일 추상 메서드를 가진 인터페이스임.
8. 람다 표현식은 나중에 실행할 수 있는 코드 블록임.
9. 람다 표현식은 함수형 인터페이스로 변환됨.
10. 메서드 참조와 생성자 참조는 메서드와 생성자를 호출하지 않고 참조함.
11. 람다 표현식과 지역 클래스는 자신을 감싸는 유효 범위에 있는 사실상 최종 변수에 접근할 수 있음.

## 3.1 인터페이스

인터페이스(`interface`)는 서비스 공급자와 자신의 객체를 이 서비스에 사용하고 싶은 클래스 간의 계약을 기술하는 메커니즘. -> 중개업자 - 접점(두 가지 주제시스템 등이 서로 만나서 영향을 주고받는 영역)

### 3.1.1 인터페이스 선언

`public static double average(IntSequence seq, int n)`

sequence[^dic] 정수 시퀀스에서 처음 n개 값의 평균을 보고하는 서비스가 있다고 가정.

[^dic]: **1.**(일련의) 연속적인 사건들He described **the sequence of events** leading up to the robbery.그가 결국 그 강도 사건으로 귀결된 연속적인 사건들을 기술했다.**2.**(사건행동 등의) 순서The tasks had to be performed in a particular **sequence**.그 작업은 특정한 순서대로 수행되어야 했다.**3.**(영화에서 연속성 있는 하나의 주제정경으로 연결되는) 장면 // 동 - 차례로 배열하다 등.

정수 시퀀스가 취할 수 있는 다양한 형태의 예

- 사용자가 제공한 정수 시퀀스
- 임의의 정수 시퀀스
- 소수 시퀀스
- 정수 배열에 들어 있는 요소의 시퀀스
- 문자열에 들어 있는 코드 포인트의 시퀀스
- 수에 들어 있는 각 숫자의 시퀀스

모든 종류의 시퀀스를 다룰 단일 메커니즘(`single mechanism`) 을 구현해봅시다

정수 시퀀스 사이의 공통점 - 시퀀스를 다루려면 최소 2개 메서드필요

- 다음 요소가 있는지 검사하는 메서드
- 다음 요소를 얻는 메서드

```java
public interface IntSequence {
    boolean hasNext();
    int next();
}
```

- 메서드 구현 필요없음 - 기본궇녀없이 선언만한 메서드 추상( `abstract`) 메서드라고 함.
- 기본구현 가능

> Note = 인터페이스 모든 메서드는 자동 `public`이됨. `hasNext`와 `next`를 `public` 선언 필요 없음. 일부 명시적으로 쓰는 사람도 있다고함.

```java
public static double average(IntSequence seq, int n) {
    //시퀀스와 n을 넣고
    int count = 0;
    double sum = 0;
    //결과를 반환할 count와 sum 선언 및 초기화
    while(seq.hasNext() && count < n) {
        //위조건이 false가 나올때까지 반복
        count++;
        sum += seq.next();
        //sum에 저장
    }
    return count == 0 ? 0 : sum / count;
    //count가 0이면 0을 반환, 아니면 평균값을 반환함.
}
```



### 3.1.2 인터페이스 구현

`IntSequence`를 구현(`implement`[^dic0])하여 `average`메서드에 사용할 수 있는 클래스를 살펴보자고함.

[^dic0]: **동 - 1.**시행하다to **implement changes/decisions/policies/reforms**변화/결정/정책/개혁을 시행하다**명사****1.**(흔히 옥외 활동에 쓰이는 간단한) 도구agricultural **implements**농기구



```java
public class SquareSequence implements IntSequence {
    //SquareSequence가 IntSequence를 따른다는 의미
    private int i;
    pulbic boolean hasNext() {
        return true;
    }
    public int next() {
        i++;
        return i * i;
    }
}

//-----------
public class Test {
    public static void main(String[] args){
        SquareSequence squares = new SquareSequence();
        double avg = average(squares, 100);
    }
}
//============
//유한 시퀀스(가장 낮은 자릿수부터 시작해 양의 정수를 구성하는 숫자 돌려줌)
// 1의 자리부터 가장 높은 자리까지 양의 정수로 반환해줌.
//ex) new DigitSequence(1792) -> hasNext false반환시까지 2, 9, 7, 1 반환
public class DigitSequence implements IntSequence {
    //인트 시퀀스를 implements한 DigitSequence
    //전역에 number선언
    private int number;
    
    //생성자를 만들며 nubmer를 초기화
    public DigitSequence(int n){
        number = n;
    }
    
    //nubmer값이 0이 아니면 true반환
    public boolean hasNext(){
        return number !=0;
    }
    
    //next 메서드 설명
    public int next(){
        //전역에 있는 nuber를 10으로 나눈 나머지연산
        int result = number % 10;
        
        //number를 10을 나누어 목을 전역에 대입
        number /= 10;
        
       	//나머지 연산을 반환
        return result;
    }
    public int rest(){
        return number;
        //멈추는것인지?
    }
}
```

//정수오버플로는 무시하고

> Caution = 인터페이스를 구현하는 클래스는 인터페이스의 메서드를 반드시 `public`으로 선언해야함. 그렇지 않으면 클래스의 메서드는 기본적으로 패키지 접근이 됨. -> 인터페이스는 공개 접근을 요구하므로 컴파일러가 오류를 보고함.

> Note = `SquareSequence`와 `DigitSequence`클래스는 인터페이스의 모든 메서드를 구현해야됨. 클래스가 인터페이스의 메서드 중 일부만 구현한다면 해당 클래스는 반드시 `abstract`제어자로 선언해야함.



### 3.1.3 인터페이스 타입으로 변환

```java
IntSequence digits = new DigitSequence(1729);
double avg = average(digits, 100);
```

`IntSequence`타입 변수는 `IntSequence`인터페이스를 구현한 어떤 클래스의 객체라도 참조할 수 있음.

??객체의 클래스가 인터페이스를 구현할 때는 이 객체를 해당 인터페이스 타입 변수에 할당할 수 있다. 또 이 객체를 해당 인터페이스를 기대하는 메서드에도 전달 할 수 있음.?????

- `T`타입의 모든 값을 변환 없이 `S`타입의 변수에 할당할 수 있다면 `S`타입은 `T`타입(서브타입(`subtype`))의 슈퍼타입(`supertype`)이다. ex) `IntSequence`인터페이스는 `DigitSequence`클래스의 슈퍼타입임.

> Note = 인터페이스 타입으로 변수를 선언할 수 있지만, 타입이 인터페이스 자체인 객체는 만들 수 없음. 모든 객체는 클래스의 인스턴스임.

### 3.1.4 캐스트와 `instanceof`  연산자

`부모 변수A = new 자식생성자();`

반대의경우 슈퍼타입 -> 서브타입 => 캐스트(`cast`)(강제변환)을 사용

```java
IntSequence sequence = ...;
DigitSequence digits = (DigitSequence)sequence;
//digits.rest() 가능
```

- 객체는 실제 클래스나 그 슈퍼타입으로만 캐스트 가능, 잘못 캐스트시 컴파일 시간오류나 클래스 캐스예외(`ClassCastException`)뜸.

  ```java
  String digitString = (String) sequence;
  //작동불능 -> IntSequence는 String의 슈퍼타입이 아님
  RandomSequence randoms = (RandomSequence) sequence;
  //가능성이 있으나, 불가능하면 클래스 캐스트 예외 던짐.
  ```

- 그러지 않기 위해 먼저 객체가 원하는 타입인지 `instanceof`연산자로 검사해야됨.

- `object instanceof Type` `object`가 `Type`을 슈퍼타입으로 둔 클래스의 인스턴스일 때 `true`를 반환함.

  =>> 객체의 실제클래스가 `Type`이거나 `Type`을 확장 또는 구현한 서브타입일 때 `true`

- ```java
  if(sequence instanceof DigitSequence) {
      DigitSequence digits = (DigitSequence) sequence;
      //...
  }
  ```

  > Note = `instanceof`연산자는 `null`에 안전함(`obj`가 `null`이면 `obj instanceof Type` 표현식은 `false`임.). 결국 `null`은 어떤 타입의 객체도 참조할 수 없음.



### 3.1.5 인터페이스 확장

인터페이스는 또 다른 인터페이스를 확장(`extand`)해서 원래 있던 메서드 외의 추가 메서드를 요구하거나 제공할 수 있음

```java
//예외가 일어날때 리소스를 닫는 중요한 인터페이스임.
public interface Closeable{
    void close();
}
//---
public interface Channel extends Closeable {
    boolean isOpen();
}
//채널 인터페이스를 구현하는 클래스(자식)은 도 메서드를 모두 구현해야됨. -> 두 인터페이스 타입 중 어느 것으로든 해당 클래스의 객체를 변환할 수 있음.
```



### 3.1.6 여러 인터페이스 구현

클래스는 인터페이스를 몇 개든 구현할 수 있음. -> 다중상속의 개념

```java
public Class AAA implement AA0, AA1, AA2 {
    ...
}
//AAA클래스는 AA0, AA1, AA2를 슈퍼타입으로 둔다.
```



### 3.1.7 상수

인터페이스에 정의한 변수는 자동으로 public static final이 됨. 이 상수들은 전체이름으로 참조할 수 있고, 클래스가 인터페이스를 구현하면 한정어(`qualifier`)를 생략하고 쓸 수 있음. 일반적 표현 아니고 열거(`enumeration`)를 사용하는 것이 더 좋음.

> Note = 인터페이스 안에는 인스턴스 변수를 둘 수 없음. 인터페이스는 객체의 상태가 아니라 동작(behavior)을 명시함.



## 3.2 인터페이스의 정적 메서드, 기본 메서드, 비공개 메서드

자바 8 이전에는 인터페이스 모든 메서드가 추상 메서드여야 했음. 메서드의 바디가 없어야 했음.

자바 9에서는 실제 구현이 있는 메서드 세종류(정적, 기본, 비공개) 인터페이스에 추가할 수 있음[^dic2]

[^dic1]: 자바 8부터는 정적 메서드와 기본 메서드를 인터페이스에 넣을 수 있고, 자바 9부터는 비공개 메서드를 인터페이스에 넣을 수 있음.

### 3.2.1 정적 메서드

팩토리 메서드는 인터페이스와 잘 맞음. `IntSequence`인터페이스에는 주어진 정수의 숫자 시퀀스를 만들어 내는 정적 메서드인 `digitsOf`둘 수 있음.

`IntSequence digits = IntSequence.digitsof(1729);`

위 메서드는 `IntSequence`인터페이스를 구현한 클래스의 인스턴스를 돌려주나, 호출자는 이 인스턴스가 어느 클래스의 인스턴스인지 신경쓸 필요 없음.

```java
public interface intSequence {
    //...
    static IntSequence digitsOf(int n){
        return new DigitSequence(n);
    }
}
```

> Note = 이전(?)에는 보통 정적 메서드를 동반 클래스(`companion class`)에 두었음. 자바`API`에서 `Collection/Collections`나 `Path/Paths`같은 인터페이스와 유틸리티 클래스의 쌍을 볼 수 있음. <= 하지만 이 분할이 필요없다고 한다.

### 3.2.2 기본 메서드

인터페이스에 있는 어느 메서드에서든 기본(`default`)구현을 작성 가능. 기본 메서드는 방드시 ` default`제어자 붙여야함.

```java
public interface IntSequence{
    default boolean hasNext(){
        return true;
    }
    int next();
}
```

구현하는 클래스측에서는 `hasNext`메서드를 오버라이드하거나 기본 구현을 상속하는 방법 중 하나를 선택가능

> Note = 기본 메서드 덕에 자바 `API`의 `Collection/AbstractCollection`이나 `WindowListener/WindowAdapter`처럼 인터페이스와 해당 인터페이스의 메서드를 대부분 또는 모두 구현한 동반 클래스를 제공했던 고전적 패턴에 종지부를 찍을 수 있었음. 요새는 바로 구현함. <== 좋아졌단 말인듯

- 기본 메서드 주 용도 -> 인터페이스를 진화(`interface evolution`)

- `Collection`인터페이스를 예를 들어 설명 => ???

  `public class Bag implement Collection`

  - 이전 처럼 기본메서드가 없을 시 `Bag`클래스는 새로 추가된 메서드를 구현하지 않으므로 컴파일이 되지 않음. -> 인터페이스에 기본 메서드가 아닌 메서드를 추가하면 소스 수준에 호환(`source-compatible`)
  - 클래스를 다시 컴파일 하지 않고 `Bag`클래스가 포함된 기존 `JAR`파일을 그대로 사용한다고 하면, 빠진 메서드가 있는데도 여전히 클래스를 제대로 로드함. 프로그램에서 여전히 `Bag`인스턴스를 생성할 수 있고, 문제도 없음(인터페이스에 메서드를 추가하는 것은 바이너리 수준에 호환(`binary-compatible`)). 하지만 프로그램에서 `Bag`인스턴스로 메서드 호출 시 `AbstractmethodError`발생함.
  - 메서드 `default`선언시 이 문제 해결가능. `Bag`클래스 제대로 컴파일됨. `Bag`클래스를 다시 컴파일하지 않고 로드한 후 `Bag`인스턴스로 `stream`메서드를 호출하면 `Collection.stream`메서드가 호출됨.



### 3.2.3 기본 메서드의 충돌 해결

클래스가 인터페이스를 두 개 구현한다 가정. 한 인터페이스에는 기본 메서드있고, 다른 인터페이스에는 이 메서드와 이름, 매개변수 타입이 같은 메서드(기본이든 아니든)가 있다면 반드시 충돌을 해결해야함.

```java
public interface Person{
    String getName();
    default int getId(){
        return 0;
    }
}
//====
public interface Identified{
    default int getid(){
        return Math.abs(hashCode());
    }
}
```

`hashCode`메서드가 객체에서 파생한 정수를 반환함.

```java
public class Employee implements Person, Identified{
    //해결법
    public int getId(){
        return Identified.super.getId();
    }
    //...
}
```

`Employee`클래스는 `Person`인터페이스의 `getId`메서드와 `Identified`인터페이스의 `getId`메서드를 상속받음. 문제는 자바 컴파일러가 한가지를 선택하지 못함. -> 오류 보고함.

해결법 -> `Employee`클래스에 `getId`메서드를 추가한 후 고유 `ID`체계를 구현하거나, 출돌한 메서드 중 하나에 위임해야됨.

> Note = `super`키워드로 슈퍼타입의 메서드를 호출할 수 있음. 위 예제에서는 둘 중 어느 슈퍼타입을 원하는지 명시해야됨. 슈퍼클래스의 메서드를 호출하는 문법과 일관성이 있다는 것은 4장에서 설명함.

`Identified`인터페이스에서 `getId`를 기본 메서드로 구현하지 않는다고 하면

```java
interface Identified{
    int getId();
}
```

`Employee`클래스가 `Person`인터페이스의 기본 메서드를 상속받을수있는가? -> 설명이 어려워 그대로 적습니다. -> 언뜻보면 가능할거같기도함. 하지만 `Identified.getId`가 수행할 동작을 `Person.getId`메서드가 실제로 하는지 컴파일러가 어떻게 아는가? ex) `Person.getId`는 사람의 `ID`번호가 아니느 프로이트의 이드(`Freudian id`)레벨을 반환할 수 있음.[^dic2]     <===???????????????????

[^dic2]: 이드(`id`)는 프로이트 자아, 초자아와 더불어 정신을 구성하는 이론적 요소로 정신분석학 용어. -> 태어나면서부터 존재하는 본능적 충동의 원천을 의미함. 하... 설명이 참 어렵네요 결국 본문에서 필자는 어느 인터페이스의 `getId`인지 알지 못한다는 임다.

====> 해결책 : 자바 설계자들 안전성과 일관성 따르기로함. 두 인터페이스가 어떻게 충돌하는지는 중요하지 않음. 적어도 한 인터페이스에서 구현을 제공하면 컴파일러는 오류를 보고함. 모호성을 해결하는 일은 프로그래머의 책임임  <-- 응 그렇게 쓰지말라고 명시적으로 말해주는거같습니다.

> Note = 두 인터페이스 모두 공유 메서드의 기본 구현을 제공하지 않으면 충돌이 일어나지 않는다. 이 경우 구현 클래스에 메서드를 구현하거나 메서드를 구현하지 않고 클래스를 `abstract` 로 선언하면됨.

> Note = 클래스가 슈퍼클래스를 확장하고 인터페이스를 구현해서 두 인터페이스가 모두 같은 메서드를 상속받을 때 규칙이 더 간단함. 슈퍼클래스의 메서드만 중요하고 인터페이스의 기본 메서드는 무시됨. <== 이게 인터페이스간 충돌보다 일반적이라고 합니다. 말이참 어렵네요

### 3.2.4 비공개 메서드

9부터 인터페이스에 비공개 메서드를 만들 수 있음. 비공개 메서드는 `static`이나 인스턴스 메서드는 될 수 있지만, `default`메서드는(오버라이드가 가능) 될 수 없음. 비공개 메서드는 인터페이스 자체에 있는 메서드에서만 쓸 수 있으므로, 인터페이스 안에 있는 다른 메서드의 헬퍼 메서드로만 사용할 수 있음.

```java
//IntSequence 인터페이스가 다음메서드를 제공한다고 가정
static of(int a)
static of(int a, int b)
static of(int a, int b, int c)

//이 메서드들은 헬퍼메서드 호출가능
private static IntSequence makeFiniteSequence(int... values){
    //...
}
```



## 3.3 인터페이스의 예

인터페이스는 클래스가 구현하기로 약속한 메서드의 집합. 예로는 자바 API중 자주 사용하는 4가지 보자.

### 3.3.1 Comparable 인터페이스

 객체의 배열을 정렬한다고 봤을 때, 정렬 알고리즘은 요소를 비교해서 순서가 어긋나 있으면 재배치하는 일을 반복함. 비교하는 규칙은 클래스마다 다르고, 정렬 알고리즘은 클래스가 제공하는 메서드를 호출할 수 있어야 함. 모든 클래스가 호출될 메서드를 무엇으로 할지 합의하면 정렬 알고리즘은 정렬을 수행할 수 있음.

 어떤 클래스의 객체를 정렬하려면 해당 클래스가 `Comparable`인터페이스를 구현해야함. 이 인터페이스의 기술적 중한 점 -> 정렬을 수행할 때 문자열 대 문자열, 직원 대 직원 식으로 비교함. `Comparable`인터페이스는 타입 매개변수를 받는다.

```java
public interface Comparable<T> {
    int compare to(T other);
}
```

ex) `String`클래스는 `Comparable<String>`을 구현함 `String`의 `compareTo`메서드는 다음 시그니처를 가짐

```java
int compareTo(String other)
```

> Note = `Comparable`이나 `ArrayList`처럼 타입 매개변수를 받는 타입은 제네릭(`generic`)타입.

`x.compareTo(y)`를 호출하면 `compareTo`메서드는 `x`와 `y`중 어느 것이 앞에 오는지 나타내는 정수값을 반환함. 반환값이 양수(1일 필요 X)면 `x`가 `y`다음에 옴. 반환값이 음수(-1이면 필요 X)면 `y`가 `x`다음에 옴. `x`와 `y`가 같으면 0.

어떤 정수든 반환 값이 될 수 있음. 이런 유연성으로 인해 정수간 차이를 반환할 수 있음. 정수간 차이가 정수 오버플로를 일으키지 않는 한 이 방법이 편함.

```java
public class Employee implements Comparable<Employee>{
   //...
    public int compareTo(Employee other){
        return getId() - other.getId();//ID가 항상 0이면 제대로 작동함.
    }
}
```

> Caution = 두 정수의 차이를 반환하는 방법이 늘 제대로 작동하는 것은 아님. 부호가 서로 반대인 피연산자들의 값이 크면 두 정수의 차이가 오버플로 될 수 있음. 이때는 모든 정수에 올바르게 작동하는 `Integer.compare`메서드를 사용하나, 정수들이 음수가 아니거나 절대값이 `Integer.MAX_VALUE` / 2 보다 작다면 차이를 반환해도 제대로 작동함.

부동소수점값 비교 시 그대로 차이를 반환하면 안됨. 그 대신 정적 메서드 `Double`, `compare`를 사용해야함. 이 메서드 -> `+-무한대`와 `NaN(Not a Number)` 제대로 작동

```java
public class Employee implements Comparable<Employee>{
   //...
    public int compareTo(Employee other){
        return Double.compare(salary, other.salary);//ID가 항상 0이면 제대로 작동함.
    }
}
```

직원들을 급여순으로 정렬하는 방법.

> Note = `compare`메서드가 `other.salary`에 접근하는 것은 규칙에 맞음. 자바의 메서드는 자신이 속한 클래스의 모든 객체에 있는 비공개 기능에 접근가능

`String`클래스는 자바 라이브러리에 들어 있는 100개 이상의 다른 클래스와 마찬가지로 `Comparable`인터페이스를 구현함. `Arrays.sort`메서드는 `Comparable`객체로 구성된 배열을 정렬함.

```java
String[] friends = {"P", "A", "M"};
Arrays.sort(friends);
```

> Note = `Array.sort`메서드는 컴파일 시간에 인수가 `Comparable`객체의 배열인지 검사하지 않음. 대신 `Comparable`인터페이스를 구현하지 않은 클래스 요소를 만나면 예외를 던짐.



### 3.3.2 Comparator 인터페이스

문자열을 사전 순서가 아니라 길이가 증가하는 순서로 비교한다고 하면, `String`클래스는 `compareTo`메서드를 두  가지 방법으로 구현하지 못함. -> `String`클래스는 우리가 소유한 클래스가 아니므로 수정불가.

 위 상황에 맞는 `Arrays.sort`메서드의 두 번째 버전 -> 이 버전은 배열과 비교자(`comparator)`를 매개변수로 받음(비교자는 `Comparator` 인터페이스를 구현하는 클래스의 인스턴스임.)

```java
public interface Comparator<T>{
    int compare(T first, T second);
}
//문자열을 길이로 비교하려면 Comparator<String>을 구현하는 클래스를 정의해야 함.
class LengthComparator implements Comparator<String>{
    public int compare(String first, String second){
        return first.length() - second.length();
    }
}
//실제 비교 수행시 이클래스의 인스턴스를 만들어야함.

public void main(String[] args){
    Comparator<String> comp = new LengthComparator();
    if(com.compare(words[i], words[j] > 0))//...
}
```

위 호출을 `words[i].compareTo(words[j])`와 비교하면 `compare`메서드는 문자열 자체가 아니라 비교자 객체로 호출됨.

> Note = `LengthComparator`객체에는 상태가 없지만 여전히 인스턴스를 만들어야 한다. `compare`메서드는 정적 메서드가 아니므로 호출하려면 인스턴스가 필요함.

배열을 정렬하려면 `LengthComparator`객체를 `Arrays.sort`메서드에 전달해야함.

```java
String[] friends = {"p", "pp", "m"};
Arrays.sort(friends, new LengthComparator());
```



### 3.3.3 Runnable 인터페이스

 모든 프로세서가 멀티코어 장착하고 있다면, 모든 코어를 작업 중인 상태로 유지하고 싶을 것임. 아마 특정 작업을 별도의 스레드에서 수행하거나 실행용 스레드 풀에 넣으려고 할 것임. 작업을 정의하려면 `Runnable`인터페이스를 구현해야함. `Runnable`인터페이스에는 메서드가 한개만 있음.

```java
class HelloTask implements Runnable{
    pulic void(){
        for(int i=0; i<1000; i++){
            System.out.println("Hello, World!");
        }
    }
}
```

이 태스크를 새 스레드에서 실행하려면 `Runnable`로 스레드를 생성하고 시작해야함.

```java
Runnable task = new HelloTask();
Thread thread = new Thread(task);
thread.start();
```

이제 `run`메서드는 별도의 스레드에서 실행되므로 현재 스레드는 다른 작업을 계속할 수 있다.

### 3.3.4 사용자 인터페이스 콜백

`GUI(Graphical User Interface)`를 이용할 때는 동작에 대한 수행할 액션을 지정하는데 -> 콜백(`callback`)이라고 한다. 자바 기반`GUI`라이브러리에서는 콜백에 인터페이스를 사용함. ex) `JavaFX`에서는 이벤트를 보고할 때 다음 인터페이스 사용함.

```java
public interface EventHandler<T>{
    void handle(T event);
}

//EventHandler도 제네릭 인터페이스 여기서 T는 보고할 이벤트 타입(ex 버튼클릭에 해당하는 ActionEvent), 수행할 액션 지정시 EventHandler<T> 인터페이스 구현해야함.

class CancelAction implements EventHandler<ActionEvent> {
    public void handle(ActionEvent event) {
        System.out.println("Oh noes!");
    }
}

//메인에서 객체생성해서 버튼 추가
Button cancelButton = new Button("Cancel");
cancelButton.setOnAction(new CancelAction());
```

> ==> 본 교재에서의 콜백예제에 대해서는 `JavaFX` -> `Swing GUI`툴킷으로 표현하였음.
>
> 간단하게 생각하여 안드로이드의 `listener`의 경우 1가지 동작만 가능하게 한 `callback`으로 볼수있음.

### 

## 3.4 람다 표현식

람다 표현식(`lambda expression`)은 나중에 한번이상 싱행할 수 있게 전달하는 코드 블록임.

- `Arrays.sort`에 비교 메서드 전달
- 별도의 스레드에서 태스크 실행
- 버튼을 클릭했을 때 일어날 액션 지정

이전 설명한 부분들이 이런 코드블록을 지정할때 좋은 상황들

하지만 자바는 객체지향언어이고, 함수타입이 없음. 대신 객체(특정 인터페이스를 구현하는 클래스의 인스턴스)로 함수를 표현함.

### 3.4.1 람다 표현식 문법

문자열을 길이로 정렬하려고 한 문자열이 다른 문자열보다 짧은지 검사하는 코드를 전달하는 `Comparator`인터페이스의 경우는

```java
first.length() - second.length()
```

와 같이 계산함.

`first`와 `second` 둘다 문자열이다. 자바는 타입결한이 강한 언어이므로 타입도 명시해야됨.

```java
(String first, String second) -> first.length() - second.length()
```

람다식은 쉽게 말해 코드 블록으로, 해당 코드에 전달해야 하는 변수의 명세(`specification`)까지 갖춘것.

람다 표현식의 바디에서 표현식 하나로는 표현할 수 없는 계산을 수행한다면 메서드를 쓸 때 처럼 작성하면 됨.

{}로 감싸고 명시적인 `return`문을 사용함.

```java
(String first, String second) -> {
    int difference = first.length() - second.length();
    if(difference < 0) return -1;
    else if (difference > 0) return 1;
    else return 0;
}
```

람다 표현식에 매개변수가 없으면 매개변수가 없는 메서드처럼 빈 괄호를 붙여야함.

```java
Runnable task = () -> {for(int i = 0; i<1000; i++) do}
```

람다 표현식의 매개변수 타입을 추론할 수 있다면 다음과 같이 매개변수 타입을 생략할 수 있음.

```java
Comparator<String> comp
 = (first, second) -> first.length() - second.lenth();
//(String first, String second)와 같음.
//람다 표현식을 문자열 비교자(Comparator<String>)에 할당하므로, 컴파일러는 first와 second가 문자열이라고 추론할 수 있다.
```

메서드에 매개변수가 한개만 있고, 이 매개변수의 타입을 추론할 수 있다면 괄호도 생략할 수 있다.

```java
EventHandler<ActionEvent> listener = event ->
    System.out.println("Oh noes!");
//(event) -> 또는 (ActionEvent event) -> 대신 사용할 수 있다.
```

람다 표현식의 결과 타입은 명시하지 않음. 하지만 컴파일러는 람다 표현식 바디에서 결과 타입을 추론한 후 기대하는 타입과 일치하는지 검사함.

```java
(String first, String second) -> first.length() - second.length()
```

이 표현식은 기대하는 결과가 `int`타입(또는 `Integer`, `long`, `double`같은 호환 타입)인 문맥에 사용할 수 있음.



### 3.4.2 함수형 인터페이스

람다식은 액션을 표현하는(ex `Runnable`, `Comparator`) 인터페이스와 호환됨.

람다 표현식은 단일 추상 메서드(`single abstract method`)를 가진 인터페이스(즉, 추상 메서드가 한 개만 있는 인터페이스)자리에 사용할 수 있음. 이런 인터페이스를 함수형 인터페이스(`functional interface`)라고 함.[^참조]

[^참조]: 오해하지 마세요. 인터페이스에 기본 메서드나 정적 메서드(자바 8), 비공개 메서드(자바 9)가 여러 개 있다고 해도 추상 메서드가 한개만 있다면 함수형 인터페이스임.

함수형 인터페이스 `Arrays.sort` 이 메서드는 두번째 매개변수 `Comparator`의 인스턴스를 요구함.(`Comparator` 인터페이스에는 메서드가 하나만 있음.) 이 매개변수에 다음과 같은 람다 전달해보자

```java
Arrays.sort(words, (first, second) -> first.length() - second.length());
```

내부에서 `Arrays.sort` 메서드의 두 번째 매개변수는 `Comparator<String>`을 구현한 클래스으이 객체를 받음. 이 객체로 `compare`메서드를 호출하면 람다 표현식의 바디가 실행됨. 이런 객체와 클래스를 관리하는 일은 순전히구현체의 몫이며 고도로 최적화 되있음 -> 명시적 표현보다는 암묵적으로 짜여진거같다는 느낌같습니다. 스마트하게

함수 리터럴을 지원하는 거의 모든 프로그래밍 언어에서`(String, String) -> int`처럼 함수 타입을 선언하고, 이 함수 타입으로 변수를 선언한 후 함수를 변수에 저장해 호출할 수 있음. 하지만 자바에서는 이 중 하나만 람다 표현식으로 할수 있음. 바로 람다 표현식을 함수형 인터페이스 타입 변수에 저장해 해당 인터페이스의 인스턴스로 변환하는 것.

> Note = 자바 `Object`타입은 모든 클래스의 슈퍼타입이지만, 람다 표현식은 `Object`타입 변수에 저장할 수 없음. `Object`는 함수형 인터페이스가 아니라 클래스임.

자바 `API`에는 수많은 함수형 인터페이스가 있음. 그 중 하나가 `Predicate`인터페이스임.

```java
public interface Predicate<T>{
    boolean test(T t);
    //이외의 default 메서드와 static 메서드
}
```

`ArrayList`클래스에는 매개변수로 `Predicate`를 받는 `removeIf`메서드가 있음. `Predicate`는 람다 표현식을 전달받을 용도로 특별히 설계함. ex) 다음 문장 배열 리스트에서 `null`값을 모두 제거함.

```java
list.removeIf(e -> e == null);
```



to be continue..



## 3.5 메스드 참조와 생성자 참조

## 3.6 람다 표현식 처리

## 3.7 람다 표현식과 변수 유효 범위

## 3.8 고차 함수

## 3.9 지역 클래스와 익명 클래스