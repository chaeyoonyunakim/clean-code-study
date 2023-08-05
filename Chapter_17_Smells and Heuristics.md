# Chapter 17 : [Smells](https://en.wikipedia.org/wiki/Code_smell) and [Heuristics](<https://en.wikipedia.org/wiki/Heuristic_(computer_science)>)

날짜: 2023년 7월 30일 → 2023년 8월 5일

## General

### G1: *****Multiple Languages in One Source File***** 한 소스 파일에 여러 언어를 사용

- 여러 언어 혼합으로 혼란스러움 또는 부주의함 발생 가능
- 이상적인 시나리오는 소스 파일 당 하나의 언어 사용
- 실제 상황에서는 여러 언어 사용 필요, 추가 언어의 수와 범위를 최소화하는 노력 필요

### G2: *****Obvious Behavior Is Unimplemented***** 당연한 동작이 구현되지 않음

- Following “The Principle of Least Surprise”
    - 코드가 읽는 이를 놀라게 해서는 안된다. == 읽었을때 당연한 기능을 해야 한다.

### G3: *****Incorrect Behavior at the Boundaries***** 경계 에러

- 모든 boundary condition, 모든 corner case, 모든 quirk와 exception는 알고리즘을 혼란스럽게 할 수 있음
- 직관에 의존하지 마세요. 모든 경계 조건을 찾아 테스트를 작성하세요.

### G4: *****Overridden Safeties***** 안전 장치 해제

- 특정 컴파일러 경고를 끄는 것(또는 모든 경고를 끄는 것)은 빌드를 성공적으로 수행하는 데 도움이 될 수 있지만, 끝없는 디버깅 세션의 위험성이 있음
- 실패하는 테스트를 끄고 나중에 통과시킬 것이라고 스스로에게 말하는 것은 신용카드가 무료 돈인 것처럼 가정하는 것만큼이나 나쁨

### G5: *****Duplication***** 중복

DRY principle (Don’t Repeat Yourself).

“Once, and only once.”

아주 중요!

최근 15년 간 나온 디자인 패턴은 대다수가 중복 제거를 위한 방법이다. 이를 활용해 어디서든 중복을 발견하면 없애라.

- Codd 정규 형식은 데이터베이스 스키마에서 중복을 제거하는 전략임
- 객체 지향 프로그래밍 자체도 모듈을 조직화하고 중복을 제거하는 전략임
- 구조적 프로그래밍 또한 중복을 제거하는 전략임

### G6: *****Code at Wrong Level of Abstraction* 추상화 수준이 잘못된 코드**

- 고수준의 일반 개념과 저수준의 세부 개념을 분리하는 추상화하는 것이 중요함
- 모든 저수준 개념이 파생 클래스에, 모든 고수준 개념이 기본 클래스에 있어야 함
- 예를 들어, 세부 구현에만 관련된 상수, 변수, 유틸리티 함수는 기본 클래스에 존재해서는 안 됨. 기본 클래스는 그들에 대해 아무것도 알아서는 안 됨

### G7: *****Base Classes Depending on Their Derivatives***** 기본 클래스가 그들의 파생 클래스에 의존하는 경우

- 개념을 기본 클래스와 파생 클래스로 분할하는 가장 일반적인 이유는 고수준의 기본 클래스 개념이 저수준의 파생 클래스 개념에 독립적이기 위함임
- 아니면 클래스끼리 너무 강한 결합

### G8: TMI

- 잘 정의된 모듈은 매우 작은 인터페이스를 가지고 있어서 적은 양으로 많은 것을 할 수 있음
- 잘 정의된 인터페이스는 의존할 수 있는 함수가 많지 않아서 결합도가 낮음. 잘 정의되지 않은 인터페이스는 호출해야 하는 많은 함수를 제공하여 결합도가 높음
- 클래스가 가진 메서드가 적을수록 좋음. 함수가 알고 있는 변수가 적을수록 좋음. 클래스가 가진 인스턴스 변수가 적을수록 좋음
- 데이터를 숨겨라. 유틸리티 함수를 숨겨라. 상수와 임시 변수를 숨겨라. 많은 메서드나 많은 인스턴스 변수를 가진 클래스를 만들지 마라
- 하위 클래스를 위해 많은 protected 변수와 함수를 만들지 마라. 인터페이스를 매우 깔끔하고 작게 유지하는데 집중하라. 정보를 제한하여 결합도를 낮게 유지하라.

### G9: *****Dead Code*****

- 죽은 코드는 실행되지 않는 코드임.
- 사용하지 않는 코드의 문제점은 시간이 지남에 따라 냄새가 나기 시작한다는 것임. 그것이 오래될수록 냄새는 강하고 신랄해짐. 이는 사용하지 않는 코드가 디자인이 변경될 때 완전히 업데이트되지 않기 때문임.

### G10: *****Vertical Separation***** 수직 분리

- 변수와 함수는 그들이 사용되는 곳 근처에 정의되어야 함. 지역 변수는 첫 사용 바로 위에서 선언되어야 하며 수직 범위가 작아야 함.
- private 함수는 첫 사용 바로 아래에 정의되어야 함. private 함수는 전체 클래스의 범위에 속하지만, 호출과 정의 사이의 수직 거리를 제한하려고 함
- private 함수를 찾는 것은 첫 사용부터 아래로 스캔하는 것만으로 가능해야 함

### G11: *****Inconsistency***** 일관성 부족

- 특정한 방식으로 어떤 것을 수행한다면, 유사한 모든 것을 같은 방식으로 수행해야 함.

### G12: *****Clutter***** 잡동사니

- 아무도 사용하지 않고 호출하지 않는 함수, 정보를 제공하지 않는 주석 등은 삭제해라

### G13: *****Artificial Coupling***** 인위적 결합

- 무관한 개념을 인위적으로 결합하지 마라.

### G14: *****Feature Envy***** 기능 욕심

- 클래스 메서드는 자기 클래스의 변수와 함수에만 관심을 가져야 함

### G15: *****Selector Arguments***** 선택자 인수

- 함수의 인수에 선택자(Flag 등) 넣지 마라
- 함수가 여러 일을 하는 것이 됨

### G16. *****Obscured Intent***** 모호한 의도

- 코드를 짤 때는 의도를 최대한 분명히 밝혀라
- 행을 바꾸지 않고 표현한 수식, 헝가리식 표기법, 매직 번호 등 ❌

### G17: *****Misplaced Responsibility***** 잘못된 위치

- 코드 위치는 독자가 여기있겠구나! 싶은 곳에 배치하는것이 좋음.
- 때로는 개발자에게 편한 곳에 배치하기도 함

### G18: *****Inappropriate Static***** 부적절한 static 함수

- 재정의할 가능성이 존재하는 함수를 static으로 정의하지 마라

### G19: *****Use Explanatory Variables***** 서술적 변수를 사용하라

- 계산을 여러 단계로 나누고 중간 값으로 서술적인 변수 이름을 사용해서 가독성을 높여라

### G20: *****Function Names Should Say What They Do* 함수 이름은 그들이 하는 일을 말해야 한다**

- 함수가 무엇을 하는지 알기 위해 함수의 구현(또는 문서)을 봐야 한다면, 더 나은 이름을 찾거나 더 나은 이름을 가진 함수에 기능을 배치할 수 있도록 기능을 재배치해야 함.

### G21: *****Understand the Algorithm***** 알고리즘을 이해하라

- 실행 가능한 코드를 만들고 구현 완료를 선언하기 전에 함수가 동작하는 방식을 완전하게 이해해야 함

### G22: *****Make Logical Dependencies Physical***** 논리적 의존성은 물리적으로 드러내라

- 한 모듈이 다른 모듈에 의존하다면 물리적인 의존성도 있어야 함.

### G23: *****Prefer Polymorphism to If/Else or Switch/Case***** If/Else 혹은 Switch/Case 문보다 다형성을 사용하라

- 대부분의 사람들이 switch 문을 사용하는 이유는 쉬워서, 상황에 가장 적합한 해결책이기 때문은 아님. 스위치를 사용하기 전에 다형성을 고려하라.

### G24: *****Follow Standard Conventions***** 표준 표기법

- 인스턴스 변수 선언 위치, 이름을 정하는 방법, 괄호를 넣는 위치 등에 대한 표준을 따라야 함.

### G25: *****Replace Magic Numbers with Named Constants***** 매직 숫자는 명명된 상수로 교체하라

코드에서 숫자를 직접 사용하지 말라. 직관적인 것은 그냥 써도 됨.

```java
double milesWalked = feetWalked/5280.0;
int dailyPay = hourlyRate * 8;
double circumference = radius * Math.PI * 2;
```

### G26: *****Be Precise***** 정확하라

- 코드에서 무언가를 결정할 때는 정확하게 결정한다.
- 예외처리도 정확하게

### G27: *****Structure over Convention***** 관례보다 구조를 사용하라

- 스위치/케이스 문을 매번 동일한 방식으로 구현하도록 하는 것은 어렵지만 base class를 만들면 클래스가 모든 추상 메서드를 구현하도록 강제함.

### G28: *****Encapsulate Conditionals***** 조건을 캡슐화

```java
if (timer.haseExpired() && !timer.isRecurrent())

if (shouldBeDeleted(timer)) // better
```

### G29: *****Avoid Negative Conditionals*** 부정 조건은 피하라

```java
if (!buffer.shouldNotCompact())

if (buffer.shouldCompact()) // better
```

### G30: *****Functions Should Do One Thing***** 함수는 한 가지 일만 한다.

// Don’t

```java
public void pay(){
	for (Employee e : employees) {
    	if (e.isPaypay()) {
        	Money pay = e.calculatePay();
            e.deliverPay(pay);
        }
    }
}
```

// Do

```java
public void pay(){
	for (Employee e : employees)
    	payIfNecessary(e);
}

private void payIfNecessary(Employee e) {
	if(e.isPayday()){
    	calculateAndDeliverPay(e)
    }
}

private void calculateAndDeliverPay(Employee e) {
	Money pay = e.calculatePay();
    e.deliverPay(pay);
}
```

### G31: *****Hidden Temporal Couplings***** 숨겨진 순서

- 함수 인수를 적절히 배치해 함수가 호출되는 순서를 명백히 드러내라

### G32: *****Don’t Be Arbitrary* 임의로 하지 마라**

- 코드 구조를 잡을 때는 왜 그런 구조로 짰는지에 대해 생각하고, 그 이유를 코드에 나타내라.

### G33: *****Encapsulate Boundary Conditions***** 경계 조건을 캡슐화하라

- 경계 조건은 빼먹거나 놓치기 쉽기 때문에 코드 여기저기에서 처리하지 않고 한 곳에서 별도로 처리한다.

### G34: *****Functions Should Descend Only One Level of Abstraction***** 함수는 추상화 수준을 한 단계만 내려가야 한다

- 함수 내 모든 문장은 추상화 수준이 동일해야 함.
- 그 추상화 수준은 함수 이름이 의미하는 작업보다 한 단계만 낮아야 함.

### G35: *****Keep Configurable Data at High Levels***** 설정 정보는 최상위 레벨에

- 추상화 최상위 단계에 두어야 할 기본값 상수나 설정 관련 상수를 저차원 함수에 숨기지 마라

### G36: *****Avoid Transitive Navigation***** 추이적 탐색을 피하기

- 데메테르의 법칙: 일반적으로 한 모듈은 주변 모듈을 모를수록 좋다. "내성적인 코드 작성"

## Names

### N1: Choose Descriptive Names

- Desciptive Name: 코드 가독성 높여 이해도 상승, 읽는 사람이 코드의 목적과 기능을 추론가능하다.

### N2: Choose Naems at the Appropriate Level of Abstraction

- 적절한 추상화 수준에서 이름을 선택: 코드를 명확하게 하고 유지보수성를 쉽게 한다. 개발자는 구현별 이름을 지양하고 대신 작업 중인 클래스 또는 기능의 상위 개념이나 목적을 반영하는 이름을 선택하여 적응성과 지속적인 개선을 보장해야 한다.

### N3: Use Standard Nomenclature Where Possible

- 표준 명명법과 규칙을 사용: 프로젝트와 관련된 확립된 패턴과 일반적으로 사용되는 용어를 통합하여 코드를 더 쉽게 접근하고 이해할 수 있도록 만들자.

### N4: Unambiguous Names

- 모호한 용어를 피하자: 함수나 변수에 대한 명확하고 명확한 설명을 제공하는 이름을 선택하고 코드 가독성과 이해를 향상시키기 위해 필요할 때는 더 길지만 설명적인 이름을 선택하는게 좋다.

### N5: Use Long Names for Long Scopes

- 이름의 길이는 범위의 길이와 일치하게 하자: 짧은 이름은 작은 범위에 사용할 수 있지만 코드의 명확성과 이해를 유지하기 위해 더 길고 설명적인 이름을 더 큰 범위에 사용해야 합니다.

### N6: Avoid Encodings

- 인코딩을 사용하지 말자: m* 또는 f와 같은 접두사 및 vis*와 같은 프로젝트/서브시스템 인코딩은 중복이다.

### N7: Names Should Describe Side-Effects

- 이름은 side-effect을 설명해야 한다: 단순한 동사 형태를 피하자. 함수, 변수 또는 클래스의 특성과 동작을 완전히 설명해야 한다. e.g., ObjectOutputStream을 만들거나 반환하는 함수에는 "getOos" 대신 "createOrReturnOos"와 같이 기능의 모든 측면을 정확하게 반영하는 이름을 사용하는게 좋다.

## Tests

### T1: Insufficient Tests

- 코드에 오류 또는 부정확성을 발생시킬 수 있는 모든 가능한 시나리오 및 조건을 포함한다. 탐색되지 않은 조건이나 검증되지 않은 계산이 있는 한 충분하지 않습니다.

### T2: Use a Coverage Tool!

- 탐지 도구를 활용: 대부분의 IDE가 시각적 지표를 제공한다. 테스트가 불충분한 모듈, 클래스 및 기능을 식별할 수 있다.

### T3: Don't Skip Trivial Tests

- 사소한 테스트를 건너뛰지 말자: 관련 문서 작성하는 것보다 코드 작성이 더 쉽다.

### T4: An Ignored Test Is a Question about an Ambiguity

- unclear requirements로 behavioral detail이 불명확할 수 있다. 해당 테스트는 주석 처리를 하거나 @Ignore표기하면 컴파일 할 때 관련된 요소인지 아닌지 판별하기 수월하다.

### T5: Test Boundary Conditions

- 경계 조건: 알고리즘의 중간은 바르게 이해하지만 경계를 잘못 판단할 수 있으니 주의하자.

### T6: Exhaustively Test Near Bugs

- 버그 하나를 발견하면 해당 부분에 대한 철저한 테스트를 수행해야 옆에 있는 다른 버그를 잡아내기 쉽다.

### T7: Patterns of Failure Are Revealing

- 테스트 보고서에 녹색(통과) 부분과 빨간색(실패) 부분의 패턴을 찾으면 해결책으로 쉽게 이어질 수도 있다.

### T8: Test Coverage Can Be Revealing

- 테스트가 실행되지 않는 코드를 보면 테스트가 실패하는 이유를 알 수도 있습니다.

### T9: Tests Should Be Fast

- 상황이 바빠질 때 오래 걸리는 테스트들은 생략되기 쉬우니 테스트 해야 할 일을 빨리하자.

# 결론

"Clean code is not written by following a set of rules. Professionalism and craftsmanship come from values that drive disciplines."
