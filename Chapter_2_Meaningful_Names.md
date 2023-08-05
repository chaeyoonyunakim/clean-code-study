# Chapter 2. Meaningful Names

## Introduction

Names are everywhere in software. → So we’d better do it well.

## Use Intention-Revealing Names

- It should tell you why it exists
- What it does
- How it is used
- If the name requires a comment → the name does not reveal its intent

![Screenshot 2023-04-28 at 13.42.37.png](Chapter%202%20Meaningful%20Names%20e6451ce800554788ac81dc7f5175c096/Screenshot_2023-04-28_at_13.42.37.png)

The problem isn’t the **simplicity** of the code but the **implicity** of the code

You need to be able to tell what the code does as soon as you read the code.

## Avoid Disinformation

![Screenshot 2023-04-28 at 14.04.16.png](Chapter%202%20Meaningful%20Names%20e6451ce800554788ac81dc7f5175c096/Screenshot_2023-04-28_at_14.04.16.png)

You should avoid the names that give clues or incorrect meanings.

• Do not refer to a grouping of accounts as an **accountList** unless it’s actually a **List**, because the word **List** means something specific to programmers (List data type).

• Using these two names **XYZControllerForEfficientHandlingOfStrings** and **XYZControllerForEfficientStorageOfStrings** in one module is also be dis-information where they are very similar and vary in a small thing and this may lead to inconsistent spellings and mistakes.

• Avoid using the lower-case of **L** or the upper-case of **O** as variable names, because they look like the constants **one** and **zero**, respectively.

## Make Meaningful Distinctions:

If you want to distinguish or differentiate between names you should use names that have meaning, so,

- Don’t use number series naming (a1, a2, a3…) because these are non-informative
- Noise words are another meaningless distinction. Imagine that you have Product class. If you have another called ProductInfo or ProductData, then you differentiated the names but, without having mean. Info and Data are indistinct noise words like a, an, and the.
- Another example of noise words is if you have two classes Customer and CustomerObject, Which one will you use to represent the customer’s payment history? You can’t know from those names because the distinction here has no meaning.

## Use Pronounceable Names

Should use names consisting of pronounceable words. Try to pronounce DtaRcrd102, genymdhms, and modymdhms, you can’t. But you can pronounce Customer, generationTimeStamp, or modificationTimeStamp.

![Untitled](Chapter%202%20Meaningful%20Names%20e6451ce800554788ac81dc7f5175c096/Untitled.png)

## Use Searchable Names

Single-letter names and numeric constants are difficult to search for in your code, so avoid them because they are unsearchable names.

Single-letter names can ONLY be used as local variables inside short methods.

The name's length should correspond to the size of its scope.

## **Don’t Be Cute/Don’t Use Offensive Words**

Don’t use funny names or any sort of slang while naming your items.Don’t use culture dependent jokes.Again , focus on the clarity. Say what you mean , Mean what you say.

```
deleteAllItems()
```

vs

```
whack()
```

vs

```
kill()
```

vs

```
eatMyShorts()
```

vs

```
abort()
```

## **Pick One Word per Concept**

Use the same concept across the codebase.

```
FetchValue() vs GetValue() vs RetrieveValue()
```

If you are using fetchValue() to return a value of something, use the same concept; instead of using fetchValue() in all the code, using getValue(), retrieveValue() will confuse the reader.

```
dataFetcher() vs dataGetter()
```

If all three methods do the same thing, don’t mix and match across the code base. Instead, stick to one.

```
FeatureManager vs FeatureController
```

Stick to either Manager or Controller. Again, consistency across the codebase for the same thing.

## **Don’t Pun**

This is exactly opposite of previous rule.Avoid using the same word for two different purposes.Using the same term for two different ideas is essentially pun.For example, say you have two classes having the same add() method.In one class, it performs addition of two values, in another, it inserts an element into a list.So, choose wisely; in the second class use insert() or append() instead of add().

## **Solution Domain Names vs Problem Domain Names**

The clean code philosophy suggests using solution domain names such as the name of algorithms or the name of design patterns whenever needed, and use a problem domain name as the second choice. For example, accountVisitor means a lot to a programmer who is familiar with the Visitor design pattern.A “JobQueue” definitely make more sense to a programmer.

## **Add Meaningful Context as a Last Resort**

While there are a few names which are meaningful themselves, most are not.Instead, you have to place names in context for your reader by enclosing the min well-named classes, functions, or namespaces.If not possible, prefixing the names may be necessary as a last resort.For example, the member variable named “state” inside the address class shows what it contains.But the same “state” may be misleading if used to store “Name of The State” without context.So, in this scenario, name it something like “addressState” or “StateName.”The “state” may make more sense in a context where you are coding about addresses when named “addrState.”

## **Avoid Encoding**

Don”t try to reinvent the wheel and define your own encoding for things that were already defined and standardised. The last thing that you want to have is your own custom language.Because of this, try to use prefix like “I” for interfaces or “Base” suffix for abstract classes.Don”t use “C” prefix for class implementation or “m_” for variables.If you end up with a custom encoding, take a step back and try to see why you have ended up in this situation.Based on that response, you should make a decision.

## **Avoid Mental Mapping**

Let’s start with an example:

```
r
t
p
```

Even if we are developers, we don’t want to learn and memorise that “r” means full url of Dacia server from Romania,“t” is the same url but without protocol information and “p” represent the query parameters that we need to send to the server to be able to login.Even if mental mapping is bad, there are some names that are standard in our days.For example, when we see an “i” or “j” we know from the first moment that we are talking about an iteration.

## **Class and Method naming**

There are two simple rules that can help us a lot when we need to find a good name to our class or methods:

- A class name should have a noun or noun phrase
- A method name should have a verb of a verb phraseTry to avoid naming classes with prefixes/suffixes like “Service”, “Factory”, “Processor”, “Data”, “Info”.These class names are overused (especially when we don”t find better names).

## **Use names from Solution and Problem domain name**

Don”t use names that are out of context and are not from that specific domain. It is more natural for someone that works in automotive industry to use “engine” and not “power source”. You should use the specific domain names and not developers naming, that can be wrong.This can be a cause of misunderstanding between clients and developers.

## **Don’t Add Gratuitous Context**

It is pretty easy to add context to things that are already clear. For example in a class called “Car” you don’t need to name the colour field of the class “carColour” or “colourCar”. You are already in the car class and all information from this class is related to “Car”.