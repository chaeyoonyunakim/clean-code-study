# 점진적인 개선

**To write clean code, you must first write dirty code *and then clean it*.**

Most freshman programmers (like most grade-schoolers) don’t follow this advice particularly well. They believe that the primary goal is to get the program working. Once it’s “working,” they move on to the next task, **leaving the “working” program** in whatever state they finally got it to “work.” Most seasoned programmers know that this is **professional suicide**.

### Example with args

### 1차 초안

- it works 하지만 messy

```java
private boolean parse() throws ParseException { 
    if (schema.length() == 0 && args.length == 0)
      return true; 
    parseSchema(); 
    try {
      parseArguments();
    } catch (ArgsException e) {
    }
    return valid;
  }
  
  private boolean parseSchema() throws ParseException { 
    for (String element : schema.split(",")) {
      if (element.length() > 0) {
        String trimmedElement = element.trim(); 
        parseSchemaElement(trimmedElement);
      } 
    }
    return true; 
  }
  
  private void parseSchemaElement(String element) throws ParseException { 
    char elementId = element.charAt(0);
    String elementTail = element.substring(1); 
    validateSchemaElementId(elementId);
    if (isBooleanSchemaElement(elementTail)) 
      parseBooleanSchemaElement(elementId);
    else if (isStringSchemaElement(elementTail)) 
      parseStringSchemaElement(elementId);
    else if (isIntegerSchemaElement(elementTail)) 
      parseIntegerSchemaElement(elementId);
    else
      throw new ParseException(String.format("Argument: %c has invalid format: %s.", 
        elementId, elementTail), 0);
    } 
  }
```

### 2차

- boolean 유형에 대해서만 리팩토링 진행, 당장은 괜찮으나 Arg 유형이 다양해질수록 엉망이 될 가능성 존재
- 여기서 기능 추가를 멈추고 리팩토링을 해야한다.

### 3차

- 프로그램을 망치는 가장 좋은 방법 중 하나는 개선이라는 이름 아래 구조를 크게 바꾸는 행위. **점진적인** 개선이 중요!
- The problem is that it’s very hard to get the program working the same way it worked before the “improvement.” : **refinement에서 가장 중요한 것은 test**
- test를 통과하면 변경 후에도 시스템이 변경 전과 똑같이 돌아간다고 할 수 있다!

```java
private class ArgumentMarshaler { 
  private boolean booleanValue = false;

  public void setBoolean(boolean value) { 
    booleanValue = value;
  }
  
  public boolean getBoolean() {return booleanValue;} 
}

private class BooleanArgumentMarshaler extends ArgumentMarshaler { }
private class StringArgumentMarshaler extends ArgumentMarshaler { }
private class IntegerArgumentMarshaler extends ArgumentMarshaler { }
```

## Conclusion

오래된 나쁜 코드: As code rots, the modules insinuate themselves into each other, creating lots of hidden and tangled dependencies. Finding and breaking old dependencies is a long and arduous task.

새로운 나쁜 코드: On the other hand, keeping code clean is relatively easy. If you made a mess in a module in the morning, it is easy to clean it up in the afternoon. Better yet, if you made a mess five minutes ago, it’s very easy to clean it up right now.

그러므로 코드는 언제나 최대한 깔끔하고 단순하게 정리하자. 절대로 썩어가게 방치하면 안 된다.
