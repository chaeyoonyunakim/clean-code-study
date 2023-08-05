# Boundaries

경계(Boundary)란?

프로젝트를 진행하다 보면 오픈 소스, 다른 부서가 만들어 놓은 API, 모듈 등 외부 코드를 사용하는 경우, **외부 코드를 내 코드에서 호출하는 부분**

practices and techniques to keep the boundaries of our software clean.

## Write test to learn the behaviour of third-party API

- 외부코드를 이해하기도 어렵고 내 코드에 적용하기도 힘들때…
- Instead of experimenting and trying out the new stuff in our production code, we could write some tests to explore our understanding of the third-party code.
- Learning tests verify that the third-party packages we are using work the way we expect them to

## Learning tests are better than free

- Learning tests verify that the third-party packages we are using work the way we expect them to. Once integrated, there are no guarantees that the third-party code will stay compatible with our needs. 😮

## ****Using Code That Does Not Yet Exist****

- 아직 개발되지 않은 모듈이 필요할 때, 이를 기다리기 전에 원하는 기능을 먼저 정의, mock function
- 경계를 잘 설정해놓으면 외부 모듈의 내부 로직을 이해하지 않고도 사용가능
- 외부 모듈이 개발된 다음 테스트 케이스를 생성해 우리가 API를 올바르게 사용하는지 테스트할 수도 있다.

## ****Clean Boundaries****

- Good software designs accommodate change without huge investments and rework. 좋은 소프트웨어 디자인은 변경이 생길 경우 많은 재작업 없이 변경을 반영할 수 있는 디자인이다.
- Code at the boundaries needs clear separation and tests that define expectations. 경계에 위치하는 코드는 깔끔히 분리한다.
- Avoid letting too much of our code know about the third-party particulars. 직접 호출하는 코드를 가능한 줄여 경계를 관리하자.
- Wrap third-party API in our own defined interface.
