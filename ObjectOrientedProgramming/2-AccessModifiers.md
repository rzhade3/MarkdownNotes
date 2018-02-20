# Access Modifiers
---

In computer science, because of the abstraction principle, we need to make sure that we can see only as much as we need to. If there is a function that we don't need to see from outside a class, there's no need to make it visible outside there. That's why we use access modifiers.

|   Modifier  | Class | Package | Subclass | World |
|-------------|-------|---------|----------|-------|
|  `public`   |   Y   |    Y    |    Y     |   Y   |
| `protected` |   Y   |    Y    |    Y     |   N   |
| No modifier |   Y   |    Y    |    N     |   N   |
| `private`   |   Y   |    N    |    N     |   N   |

1. `public`

The public modifier makes the method/ variable visible to everything
	* Example:
  	```java
  	class Vehicle {
		public int fuelEconomy;
  	}

	class GasStation {
		public void getFuelEconomy(Vehicle vehicle) {
			return vehicle.fuelEconomy;
		}
	}
	```

Note that in this example, the `GasStation` class can access the fuelEconomy variable in the `Vehicle` class despite not being in the same package or subclass. 

2. `protected`

The protected modifier makes the method or variable visible 
	* Example:
  	```java
  	class Vehicle {
		protected int fuelEconomy;
  	}

	class GasStation {
	}
  	```

3. No modifier

Not having a modifier means that we can see the variable/ method from within the class itself, or any class inside the package
	* Example:
  	```java
	package coolBeans;

  	class Vehicle {
		int fuelEconomy;
  	}
  	```

  	```java
	package coolBeans;
	
	class GasStation {
		public int getFuelEconomy(Vehicle vehicle) {
			return vehicle.fuelEconomy;
		}
  	}
  	```

4. `private`

	The private modifier is the most restricting of the access modifiers. Variables/ functions can only be referenced within the class it is currently within
	* Example:
  	```java
  	class Vehicle {
		private int fuelEconomy;

		public int getFuelEconomy() {
			return this.fuelEconomy;
		}
  	}
  	```

	The above is a pretty standard way to access instance variables in a class. Instead of making variables public, if we want to access the value somewhere else, we use "getter" and "setter" methods.

Remember, in computer science, the more specific you make the access modifiers, the better. Use public sparingly, and only if it must be used. 
