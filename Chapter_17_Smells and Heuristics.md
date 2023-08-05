# Chapter 17 : [Smells](https://en.wikipedia.org/wiki/Code_smell) and [Heuristics](<https://en.wikipedia.org/wiki/Heuristic_(computer_science)>)

날짜: 2023년 7월 30일 → 2023년 8월 5일

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
