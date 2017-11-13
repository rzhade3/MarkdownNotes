# Classes and Objects
---

Object Oriented programming is an important paradigm in which we use objects, which are units of code with common variables and functions, 
* We often deal with things in the real world that are markedly similar to one another, so it makes sense to keep some blueprint
	* For example, what if we had to keep track of a bunch of users in a game? Making new variables and functions for each one would be time consuming and might introduce inconsistencies. 

### Classes
Classes are the most basic unit of OOP. It is essentially a blueprint for an object
* ___Classes are not instantiated! When a class is instantiated, it is an object__
* Classes will contain methods and variables 
* Code
```java
class Vehicle {
	private int numWheels = 0;
	public void setSpeed() {
		//The methods go in here
	}
}
```

### Objects
When we want to work with a class, we need to _instantiate_ it first
* Definition:
	* Objects are simply instantiated classes
		* E.g. If you bought a new bicycle, you have a new bicycle _object_ of type (_class_) bicycle
* Code:
```java
Vehicle newVehicle = new Vehicle();
```

### Constructor
What if we want to create an object with some initial conditions? Simple: __Use a constructor__
* Definition:
	* A constructor is a method that instantiates an object, using the parameters passed in
		* This looks similar to an instance method, but has no explicit return type
	* A class can have multiple constructors, with different constructors (see [polymorphism](#polymorphism))
* Code:
```java
class Vehicle {
	private int numWheels;
	private int topSpeed;

	public Vehicle(int numWheels) {
		this.numWheels = numWheels;
	}
}
```
* Note the use of the ```this``` keyword. This keyword refers to the object that it is currently in

### Inheritance
Sometimes we might find that many classes share some common features
* Motorcycles and cars both have wheels and are types of vehicles, but might have some different quantities or features
Inheritance is an easy way to change some aspects of a class while maintaining whatever we need
* Terminology:
	1. __subclass__: The "child" class. In this example, the motorcycles and the cars are _subclasses_ of the vehicles
	2. __superclass__: The "parent" class. In this example, "vehicle" is a _superclass_ of both the motorcycle and cars class
* Code:
```java
class Vehicle {
	private int numWheels;
	private int topSpeed;

	public Vehicle(int numWheels) {
		this.numWheels = numWheels;
	}
}

class Motorcycle extends Vehicle {
	public Motorcycle(int topSpeed) {
		super(2);
		this.topSpeed = topSpeed;
	}
}

class Car extends Vehicle {
	public Car(int topSpeed) {
		super(4);
		this.topSpeed = topSpeed;
	}
}
```
* Note the use of the super() method to pass the parameter to the superclass's constructor

### Polymorphism
* Definition:
	* A fancy term for what we did in the last section
* Types
	1. _Ad hoc polymorphism:_ Also known as function overloading. Making a method behave differently depending on the parameters that are passed in
		* Code
		```java
		public int add(int x, int y) {
			return x + y;
		}

		public int add(String x, String y) {
			return x + " " + y;
		}
		```
	2. _Parametric Polymorphism:_ Somewhat more complicated. Basically it is writing a method to take in generic arguments so that it can function uniformly regardless of the parameter type
		* Code
		```java
		class Node {
			T elem;
			public Node(T elem, Node next) {
				this.elem = elem;
			}
		}
		```
		* Note the use of the T argument type in the above code. This is known as a "generic" in Java, and handles parametric polymorphism
	3. _Subtyping:_ A class, and all of its subclasses, can be passed into a method and work properly
		* Code
		```java
		class Vehicle {
			// Code goes here
		}

		class Motorcycle extends Vehicle {
			// Code goes here
		}

		class Car extends Vehicle {
			// Code goes here
		}

		public void getSpeed(Vehicle vehicle) {
			return vehicle.topSpeed;
		}
		```
		* The above code will work with vehicles, motorcycles and cars as all three are subclasses of vehicle
