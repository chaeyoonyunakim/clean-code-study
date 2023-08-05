# Chapter 7. Error Handling

## Intro

Error handling is important, but if it obscures logic, it's wrong.

오류 처리는 반드시 프로그램에 필요한 요소이다.

프로그램은 반드시 실패할 여지가 있기 때문이고 그 처리를 책임지는 건 오로지 프로그래머다.

오류 처리와 깨끗한 코드는 서로 연관성이 깊다.

여기저기 흩어진 오류 처리는 코드가 무슨 일을 하는지 알기 어렵게 한다.

이런 오류 처리로 인해 프로그램 논리를 이해하기 어려워 진다면 좋은 코드라고 보기 어렵다.

---

## Principle 1. 오류 코드보다 e**xceptions**를 사용하라

Return code **대신 Exceptions를 사용하라**

오류 코드를 사용하고 그 오류 코드에 맞게 상황을 처리하도록 구현한다면 너무 구조가 복잡하다 (호출한 즉시 오류를 처리해야 하기 때문이다)

그러므로 다음과 같이 예외를 사용하도록 짜라.

```
public void sendShutDown(){
        try{
            tryToShutDown();
        }catch (Exception e){
            e.printStackTrace();
        }
}
```

이렇게 하면 예외를 처리하는 함수와 예외가 발생할 수 있는 함수가 명확히 구별된다.

즉 개념을 독립적으로 보고 이해할 수 있다.

---

## Principle 2. Try-Catch-Finally 먼저 쓰기

예외가 발생할 수 있는 코드를 짤 땐 try-catch-finally 문을 작성하고 시작하는 것이 좋다.

그러면 어디서 예외가 일어나는지 명확해지고 예외가 날 수 있는 부분과 예외가 나지 않는 부분을 구별하도록 쉽게 짤 수 있다. 그리고 이렇게 함으로써 코드의 "Scope 정의"가 가능해진다.

즉, try 블록에 어디까지 넣어야 하는지 명확해진다.

---

## Principle 3. **Unchecked Exceptions를 사용하라**

자바에선 확인된 예외(Checked Exception)이 있다.

Checked Exception이 없는 언어도 많다 → C#과 C++, 파이썬, 루비 등

Checked Exception이 없어도 안정화 된 어플리케이션을 충분히 개발 할 수 있다.

오히려 Checked Exception은 OCP(Open Closed Principle)을 위반한다.

왜냐하면 상위 함수에서 하위 함수로 이뤄진 구조에서 하위 함수에서 추가로 예외가 발생할 수 있는 코드가 추가되면 예외 핸들러를 찾을 때까지 모든 함수가 throw Exception을 해야한다.

즉 확인된 예외 때문에 연쇄적인 수정이 발생한다.

때로는 중요한 라이브러리 작성 때문에 모든 Checked Exception을 잡아내야 하는 경우가 있지만 그렇지 않은 경우라면 사용하지 말자.

---

## Principle 4. **Exceptions로 문맥을 제공하라**

예외를 던질 땐 충분한 전후 상황에 대한 정보를 담아서 전달하라.

그러면 오류를 발생한 원인과 위치를 찾기 쉬워진다.

---

## Principle 5. **정상적인 상황을 정의하라(Default값을 설정하라)**

애플리케이션에서 오류를 정의할 때 오류를 형편없이 분류하면 안된다.

다음과 같이 외부 라이브러리를 사용하는 상황에서 모든 예외를 분류 없이 다 잡아내면 오류를 형편없이 분류한 사례다.

```
// 외부 라이브러리
ACMEPort port = new ACMEPort(12);

try{
	port.open();
}catch(DeviceResponseException e){
	reportPortError(e);
}catch(ATM1212UnlockedException e){
	reportPortError(e);
}catch(GMXError e){
	reportPortError(e);
}
```

이 경우 외부 라이브러리를 새로운 클래스로 감싸서 프로그램 의존성도 크게 줄이고 나중에 다른 라이브러리를 써도 문제없이 쓸 수 있도록 하는게 좋다.

다음과 같이 감쌀 수 있다.

```
public class LocalPort{
    private ACMEPort innerPort;

    public LocalPort(int portNumber){
    	innerPort = new ACMEPort(portNumber);
    }

    public void open(){
        try{
            innerPort.open();
        }catch(DeviceResponseException e){
           ...
        }catch(ATM1212UnlockException e){
            ...
        }
    }

}
```

---

## Principle 6. null을 리턴하지 마라

> null을 반환하는 코드는 일거리를 초래할 뿐 아니라 호출자에게 문제를 떠넘긴다.
> 

null을 반환한다면 책에서 말하는 대로 null검사를 해야하는 코드가 강제되며, 만약 빠뜨린다면 실수를 범하게 되는 것이다. JAVA 8 이후로는 Optional을 이용해 NullPointerException을 방지할 수 있다.

- 예외에 의미를 제공하라 - 예외를 던질 때는 전후 상황을 충분히 덧붙인다.
- 정상 흐름을 정의하라 - 예외를 처리할 상황 자체가 발생하지 않도록 코드를 구현해라.

```
public void registerItem(Item item){
        if(item != null){
            ItemRegistry registry = persistenceStory.getItemRegistry();
        }
}
```

이 함수에서 null을 체크하는게 문제다. null을 반환하지마라.

메소드에서 null을 반환하고픈 유혹이 든다면 예외를 던지거나 특수 사례 객체를 반환하라.

자바에서는 Collections.emptyList()가 있어서 빈 리스트를 반환하는 방법이 있다. 이 방법을 사용하면 코드가 깔끔해진다.

---

## Principle 7. null을 전달하지 마라

- null을 리턴하는 것도 나쁘지만 null을 메서드로 넘기는 것은 더 나쁘다.
- null을 메서드의 파라미터로 넣어야 하는 API를 사용하는 경우가 아니면 null을 메서드로 넘기지 마라.
- 일반적으로 대다수의 프로그래밍 언어들은 파라미터로 들어온 null에 대해 적절한 방법을 제공하지 못한다.
- 가장 이성적인 해법은 null을 파라미터로 받지 못하게 하는 것이다. (애초에 전달하지말자)