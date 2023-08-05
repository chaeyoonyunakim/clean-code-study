# Unit Tests

유닛 테스트(unit test)는 컴퓨터 프로그래밍에서 소스 코드의 특정 모듈이 의도된 대로 정확히 작동하는지 검증하는 절차다. 즉, 모든 함수와 메소드에 대한 테스트 케이스(Test case)를 작성하는 절차를 말한다.

## ****The Three Laws of TDD****

**First Law.** You may not write production code until you have written a failing unit test.

**Second Law.** You may not write more of a unit test than is sufficient to fail, and not compiling is failing.

**Third Law.** You may not write more production code than is sufficient to pass the currently failing test.

∴ we will write dozens of tests every day, hundreds of tests every month, and thousands of tests every year. If we work this way, those tests will cover virtually all of our production code

## Keeping Tests Clean

bad example:

테스트 코드는 대충 짤 수 있게 허락함 ⇒ 테스트 코드 읽기가 어려워짐 ⇒ 코드를 수정할수록 실패하는 테스트가 많아져 개발 시간이 점점 길어짐 ⇒ 테스트를 없애버림 ⇒ 코드가 썩기 시작함 … 

∴ 나쁜 테스트는 테스트가 없는 셈이나 마찬가지

## What makes a clean test?

Readability, readability, and readability.

엄청 효율적일 필요는 없음, 가독성이 짱!

## One assert per test

결론이 하나라서 이해하기가 편하다.

하지만 테스트케이스가 많다면? 👇

## One concept per test

Perhaps a better rule is that we want to test a single concept in each test function.

So probably the best rule is that you **should minimize the number of asserts per concept** and **test just one concept per test function**.

## F.I.R.S.T 법칙

**F**ast : 테스트는 빨라야 한다.

**I**ndependent : 각 테스트는 서로 의존하면 안 된다.

**R**epeatable : 어떤 환경에서든 반복가능해야 한다. local, QA, Staging, 운영 환경 어디서든

**S**elf-validating : The tests should have a boolean output.

**T**imely : The tests need to be written in a timely fashion. 단위 테스트는 테스트하려는 실제 코드를 구현하기 직전에 구현한다.

## **결론**

- 테스트 코드는 실제 코드만큼이나 프로젝트 건강에 중요하다. 어쩌면 실제 코드보다 더 중요할지도 모르겠다.
- 테스트 코드는 실제 코드의 유연성, 유지보수성, 재사용성을 보존하고 강화하기 때문이다. 그러므로 테스트 코드는 지속적으로 깨끗하게 관리하자.
- 표현력을 높이고 간결하게 정리하자. 테스트 API를 구현해 도메인 특화 언어(Domain Specific Language, DSL)를 만들자. 그러면 그만큼 테스트 코드를 짜기가 쉬워진다.

> 테스트 코드가 방치되어 망가지면 실제 코드도 망가진다. 테스트 코드를 깨끗하게 유지하자.
>
