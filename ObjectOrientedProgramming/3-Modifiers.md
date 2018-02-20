# Modifiers
---
Modifiers are keywords that define some aspect of 

`public static final int variableName`

There are four main types of modifiers


### Access Modifier
[See here](AccessModifiers.md)

### Static Vs Non Static
Static modifiers mean that we can access the variable or the method without instantiating an object first. The most common example of this is with the main method

```java
public static void main(String[] args) {
	
}
```
We can call this method without instantiating an object first, as there is a static in the name of the method. 

Methods and variables can be static, which means that they are shared among all instances of the class.

* Common Uses
	1. Main method
	2. Sharing a variable between multiple objects

### Final Vs Non Final
Sometimes we might want to make a variable or function _immutable_, or unchanging. For example, if we have a certain variable that we know should _not_ change in the course of the program, or elsewhere, we can flag it with the __final__ keyword, e.g.

```java
final int maxHealth = 100;
```

It can also be used for methods and classes. A final method cannot be overriden or hidden by subclasses, e.g.

```java
public final int findArea { return side * side; }
```

And a final class cannot be subclassed.

### Variable Type

### Return Type
A return type for a function defines what type of variable the function will return. This can be any variable type. 