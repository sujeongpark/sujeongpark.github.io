---
layout: post
title: "TDD란 무엇일까?"
author: "subling"
---

# TDD (Test Driven Development) - 테스트 주도 개발
회사에서 교육시간에 TDD를 배우게 되었다. 과연 TDD(Test-Driven development)란 무엇일까?<br><br>
> <em>프로그램을 작성하기 전에 테스트 먼저 하라!<br> Test the program before you write it.</em><br><br>
\- 켄트 벡(Kent Beck)

<br><br>
## TDD의 정의
TDD는 "업무 코드를 작성하기 전에 테스트 코드를 먼저 만드는 것"이라고 할 수 있다. 즉 코드를 검증하는 테스트 코드를 먼저
만든 다음에 실제 작성해야 하는 프로그램 코드 작성에 들어가는 것이다. TDD를 사용하면 명시적인 코드로 개발 종료조건을 정해놓게 된다.
따라서 <b>테스트 케이스 작성으로 구현을 시작하는 것</b>, 그것이 바로 TDD라 할 수 있다.
<br><br><br><br>

## TDD의 목표
> <em>잘 동작하는 깔끔한 코드<br>Clean code that works</em><br><br>
\- 론 제프리(Ron Jeffries)

<br>
TDD에서는 정상적으로 동작하는 코드만이 목표가 아니라 작성된 코드가 명확한 의미를 전달할 수 있도록 작성되어야 한다고 말한다.
따라서 "제대로 동작함(works)"뿐 아니라 "깔끔함(Clean)"까지 동등한 수준의 개발 목표로 삼는다.
<br><br><br><br>

## TDD Cycle
![](https://s3.amazonaws.com/ckl-website-static/wp-content/uploads/2017/03/TDD-e1492712699769-300x300.png)<br>
TDD는 <b>테스트 코드 작성 -> 코드 구현 -> 리팩토링</b> 순으로 이루어진다.<br>
- 처음에는 실패하는 테스트를 만든다. 이것이 의미하는 바는 테스트 케이스(코드)를 작성하는 것이다. 
- 이후 단계에서 이전 단계에서 작성한 테스트 케이스를 통과하는 코드를 구현한다.
- 마지막으로 코드에서 중복이나 불필요한 것을 제거하는 등의 리팩토링 과정을 거친다.
<br><br><br>

### 예시를 한번 들어보자.
- <b>Design</b><br>
두 숫자를 더한 값을 리턴하는 add 메소드를 구현해보자.<br><br>

- <b>Test(Fail)</b><br>
```
public class Calculator {
    public int add(int a, int b) {
        return 0;
    }

    public static void main(String[] args) {
        Calculator calc = new Calculator();
        System.out.println( calc.sum(10, 20) == 30);
        System.out.println( calc.sum(1, 2) == 3);
        System.out.println( calc.sum(-10, 20) == 10);
        System.out.println( calc.sum(0, 0) == 0);
    }
}
```
실행결과
```
false
false
false
true
```
add 메소드는 컴파일 에러만 나지 않도록 해놓고, 내부는 비어둔 상태이다. 즉 add 메소드를 먼저 구현하지 않고, 테스트 코드를 먼저 만들어놓았다.
테스트 코드에 해당하는 테스트 케이스를 모두 만족하면, add 메소드가 정상적으로 작성되었다고 판단할 것이다.
<br><br>

- <b>Implement</b><br>
```
public class Calculator {
    public int add(int a, int b) {
        return a+b;
    }
    ...
}
```
add 메소드를 구현한다. 두 개의 인자를 넘겨받아 서로 더하여 값을 리턴해준다. 
<br><br>

- <b>Test(Pass)</b><br>
```
public class Calculator {
    public int add(int a, int b) {
        return a+b;
    }
    
    public static void main(String[] args) {
        Calculator calc = new Calculator();
        System.out.println( calc.sum(10, 20) == 30);
        System.out.println( calc.sum(1, 2) == 3);
        System.out.println( calc.sum(-10, 20) == 10);
        System.out.println( calc.sum(0, 0) == 0);
    }
}
```
실행결과
```
true
true
true
true
```
모두 <code>true</code>가 출력된다. 이로써 미리 작성한 테스트 케이스를 모두 통과하는 코드를 구현하였다. 앞에서 명시적인 코드로 정해놓은 개발 종료조건을 달성한 것이다. 이후에는 코드를 리팩토링하는 과정을 걸치게 된다. 예시로 작성한 add 메소드는 간단하기에 리팩토링 단계를 거치지 않아도 괜찮지만 만약, 코드가 길고 복잡해질수록 리팩토링 과정이 중요해지게 된다.<br><br>

만약 이후에, <code>add 메소드에 두 개보다 적거나 많은 인자를 받게 된다면 어떻게 해야할까?</code> 혹은 <code>넘겨받은 인자가 int 타입이 아니면 어떻게 해야할까?</code> 등 새로운 문제를 발견한다면 다시 Design 단계부터 시작해 테스트 코드를 작성하고, 작성한 테스트 케이스를 모두 통과하는 코드를 구현하는 과정이 계속 반복될 것이다.
<br><br><br><br>

## 글을 끝마치며...
<hr>
이렇게 TDD에 대해 알게 되었다. 앞으로는 코드를 작성할 때 테스트 코드를 먼저 작성하고 코드를 구현하는 습관을 들여야할 것 같다.
<br><br>

## 참고
> [테스트 주도 개발](https://repo.yona.io/doortts/blog/issue/2)<br>
[TDD on mobile dev, a matter of timing](https://cheesecakelabs.com/blog/tdd-mobile-dev-matter-timing/) (TDD Cycle 이미지 출처)<br>
