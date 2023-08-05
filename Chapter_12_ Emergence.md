# Chapter 12. Emergence

## Emergence란?

the process of becoming visible after being concealed

A design is “simple” if it follows 4 rules (in order of importance)

1. Runs all the tests
2. Contains no duplication
3. Expresses the intent of the programmer
4. Minimises the number of classes and methods

## **Runs all the tests**

- A design must produce a system that acts as intended.
- Making the system testable pushes us towards a design where our classes are small and single-purpose (SRP), and are not as tightly coupled with DI, interfaces, and abstractions.
- Writing tests leads to better design.

## Contains no duplication

### **Refactoring**

- Incrementally refactor. For every few lines of code, pause and reflect on the new design. Did we just degrade it? Run tests to demonstrate that we haven’t broken anything.
- There are different types of duplication: lines of code that look exactly the same, implementation

```
struct ItemList {
    private var items: [Int] = []
    func size() -> Int {
        return items.count
    }
    func isEmpty() -> Bool {
        return 0 == size()
    }
}
```

- talks about the “Template Method” which looks like just using extensions

```
struct VacationPolicy {
    func alterForLegalMinimums() // this should be protected
}
extension VacationPolicy {
    func accrueVacation() {
        calculateBaseVacationHours()
        alterForLegalMinimums()
        applyToPayroll()
    }
    private func calculateBaseVacationHours() { }
    private func alterForLegalMinimums() { }
}
struct USVacationPolicy: VacationPolicy {
    func alterForLegalMinimums() { }
}
struct EUVacationPolicy: VacationPolicy {
    func alterForLegalMinimums() { }
}
```

## Expresses the intent of the programmer

- Code should clearly express the intent of its author. The clearer the author can make the code, the less time others will have to spend understanding it.
- You can do this by: choosing good names, keep function classes small, using standard nomenclatures, well written unit tests (someone reading the tests should be able to get a quick understanding of what a class is all about), and the most important way is to try. Too often we get the code working and then move on. Take a little pride in your workmanship, and spend time cleaning it up.

## **Minimal Classes and Methods**

- In an effort to make our classes and methods small, we might create too many tiny classes and methods. So we should keep our functions and class count small.
- Goal should be to keep our overall system small while we are also keeping our functions and classes small.
- Remember this is the lowest priority of Simple Design.