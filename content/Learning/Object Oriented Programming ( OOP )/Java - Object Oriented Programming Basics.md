---
id: Java - Object Oriented Programming Basics
aliases: Object Oriented Prgramming Basics in Java
tags:
  - java
  - basics
  - oop
author: S.Sunhaloo
date: 2025-09-05
status: Completed
---

## List of Contents

- [[#Creation of Parent Class]]
	- [[#Implementing The Parent Class]]
	- [[#Create Instance of Parent Class]]
- [[#Creation of Methods Of Objects Of Parent Class]]
	- [[#Instance / Class Variables]]
	- [[#Creation Of Some Method For Parent Class]]
		- [[#Methods Related To Parent Class]]
- [[#Creation of Subclass]]
	- [[#Create Instance of Child Subclass]]
	- [[#Method Overriding]]
- [[#Polymorphism?]]
- [[#Encapsulation]]
- [[#Abstraction]]
- [[#Multiple Inheritance - Interfaces]]
- [[#Composition]]
- [[#Aggregation]]
- [[#Split Files]]

---

> [!INFO]
> Please refer to the first note / file with the name '[[Introduction to Object Oriented Programming]]'.
>
> These are my notes about *theoretical* aspect of Object Oriented Programming. There I talked about the `Vehicle` class.
>
> I am going to try to *implement* that same **parent** `Vehicle` class as example here also.
>
> Let's get **practical**!

> [!NOTE]
> Do refer to the Python version of this very note. Because I showed how to actually go about the steps that we need to take **before** actually writing any code.
>
> - The note / file is called '[[Python - Object Oriented Programming Basics]]'

> [!NOTE]
> For the moment instead of breaking it into multiple files. I am going to stick to a **single file** setup for the moment.

# Creation of Parent Class

## Implementing The Parent Class

```java
// Our 'Vehicle' class definition
class Vehicle {
  // Declare variables so that we can hold attributes of object 'Vehicle'
  String brand;
  String model;
  double price;
  String colour;
  int health;
  int engineNum;
  int chassisNum;
  int engineCapacity;

  // Constructor to assign those variables to the object
  public Vehicle(
      String brand,
      String model,
      double price,
      String colour,
      int health,
      int engineNum,
      int chassisNum,
      int engineCapacity) {
    // Intialise the attributes for an object
    this.brand = brand;
    this.model = model;
    this.price = price;
    this.colour = colour;
    this.health = health;
    this.engineNum = engineNum;
    this.chassisNum = chassisNum;
    this.engineCapacity = engineCapacity;
  }
}
```

> [!WARNING] `public`, `protected`, `private` And 'package-private'!
> As you know, we are working with a "*real*" Object Oriented Programming Language.
>
> This means that we need to **declare** our variables and also think about how we are going to *situate* our variables.
>
> - Do we want it to be **fully** `public`?
> 	- Meaning that *anybody* will be able to **set** or **change** it values
> 	- Yes, it can be *changed* from **anywhere**!
> - Do we want it to be '*package-private*'
> 	- Is it in the **same** "*default package*" whereby we can allow for **setting** of values
> 	- Is it in a **different** *package* ( _i.e **different** folder containing the code_ )
> - Do we want it to be `protected`
> 	- Meaning that the object's attribute will be able to **change** it if they are in the **same** *package* or *subclass*
> - Do we want it to be `private`
> 	- Meaning that the code *inside* **that class** will only be able to *changed* / *modified*
> 	- Subclasses and "*same package*" classes **cannot** even *modify* it

> As you can see... In this case, I opted to use the '*package-private*' data types.

## Create Instance of Parent Class

Let us now go ahead an create our first **object** for the **parent** class of `Vehicle`.

> [!NOTE]
> Therefore, this is what I am going to write in my `main` function of the `Main` class!

```java
// Our main class
public class Main {
  // Our main function
  public static void main(String[] args) {
    // Create first object of the parent class of `Vehicle`
    Vehicle vehicle1 = new Vehicle("Mazda", "RX-7 FD", 500000, "Canary Yellow", 65, 1, 1, 1300);
  }
}
```

### Displaying Information About Object In `Main` Class's `main` Function

- Update the `main` function as follows:

```java
// Our main class
public class Main {
  // Our main function
  public static void main(String[] args) {
    // Create first object of the parent class of `Vehicle`
    Vehicle vehicle1 = new Vehicle("Mazda", "RX-7 FD", 500000, "Canary Yellow", 65, 1, 1, 1300);

    // Display each attributes for the vehicle object created
    System.out.println("Vehicle 1's Brand: " + vehicle1.brand);
    System.out.println("Vehicle 1's Model: " + vehicle1.model);
    System.out.println("Vehicle 1's Price: " + vehicle1.price);
    System.out.println("Vehicle 1's Colour: " + vehicle1.colour);
    System.out.println("Vehicle 1's Health: " + vehicle1.health);
    System.out.println("Vehicle 1's Engine Number: " + vehicle1.engineNum);
    System.out.println("Vehicle 1's Chassis Number: " + vehicle1.chassisNum);
    System.out.println("Vehicle 1's Engine Capacity: " + vehicle1.engineCapacity);
  }
}
```

- Therefore, running our `main.py` file we should be able to display all the **attributes** of `vehicle1`

```console
Vehicle 1's Brand: Mazda
Vehicle 1's Model: RX-7 FD
Vehicle 1's Price: 500000.0
Vehicle 1's Colour: Canary Yellow
Vehicle 1's Health: 65
Vehicle 1's Engine Number: 1
Vehicle 1's Chassis Number: 1
Vehicle 1's Engine Capacity: 1300
```

> [!SUCCESS]
> As you can see, our object `vehicle1` has been successfully created with its proper attributes!

# Creation of Methods Of Objects Of Parent Class

## Instance / Class Variables

Before we create any **methods** for objects so that we can apply some *functionality* to them. I am first going to add some **class attributes** to every object of `Vehicle` being created.

```java
// Our 'Vehicle' class definition
class Vehicle {
  // Declare variables so that we can hold attributes of object 'Vehicle'
  String brand;
  String model;
  double price;
  String colour;
  int health;
  int engineNum;
  int chassisNum;
  int engineCapacity;

  // Declare class's instance variable here
  int fuelLevel;
  boolean isRunning;
  boolean locked;

  // Constructor to assign those variables to the object
  public Vehicle(
      String brand,
      String model,
      double price,
      String colour,
      int health,
      int engineNum,
      int chassisNum,
      int engineCapacity) {
    // Intialise the attributes for an object
    this.brand = brand;
    this.model = model;
    this.price = price;
    this.colour = colour;
    this.health = health;
    this.engineNum = engineNum;
    this.chassisNum = chassisNum;
    this.engineCapacity = engineCapacity;

    // Set the values for the class variables
    this.fuelLevel = 50;
    this.isRunning = false;
    this.locked = true;
  }
}
```

As you can see we have added `fuelLevel`, `isRunning` and the `locked` **class variables** that are going to be *initialised* for **any** `Vehicle` object created.

- Check `Vehicle` object **class attributes** from `main` inside `Main`

```java
// Our main class
public class Main {
  // Our main function
  public static void main(String[] args) {
    // Create first object of the parent class of `Vehicle`
    Vehicle vehicle1 = new Vehicle("Mazda", "RX-7 FD", 500000, "Canary Yellow", 65, 1, 1 1300);

    // Display each attributes for the vehicle object created
    System.out.println("Vehicle 1's Brand: " + vehicle1.brand);
    System.out.println("Vehicle 1's Model: " + vehicle1.model);
    System.out.println("Vehicle 1's Price: " + vehicle1.price);
    System.out.println("Vehicle 1's Colour: " + vehicle1.colour);
    System.out.println("Vehicle 1's Health: " + vehicle1.health);
    System.out.println("Vehicle 1's Engine Number: " + vehicle1.engineNum);
    System.out.println("Vehicle 1's Chassis Number: " + vehicle1.chassisNum);
    System.out.println("Vehicle 1's Engine Capacity: " + vehicle1.engineCapacity);

    // Display the class variables of `Vehicle` object
    System.out.println("\nVehicle 1's Fuel Level: " + vehicle1.fuelLevel + " <--");
    System.out.println("Vehicle 1's Engine Running?: " + vehicle1.isRunning + " <--");
    System.out.println("Vehicle 1's Doors Locked?: " + vehicle1.locked + " <--");
  }
}
```

- Therefore this is the output that we should expect to see:

```console
Vehicle 1's Brand: Mazda
Vehicle 1's Model: RX-7 FD
Vehicle 1's Price: 500000.0
Vehicle 1's Colour: Canary Yellow
Vehicle 1's Health: 65
Vehicle 1's Engine Number: 1
Vehicle 1's Chassis Number: 1
Vehicle 1's Engine Capacity: 1300

Vehicle 1's Fuel Level: 50 <--
Vehicle 1's Engine Running?: false <--
Vehicle 1's Doors Locked?: true <--
```

> [!SUCCESS]
> We have now been able to **create** *instance variables* and been able to **display** these variables!

## Creation Of Some Method For Parent Class

Therefore, let's go ahead and create some **methods** that's going to work with our `Vehicle` objects.

### Static Methods

> [!INFO]
> Head over to '[[Python - Object Oriented Programming Basics#Static Methods | Python - Object Oriented Programming Basics]]' if you want that little *introduction* that I gave for **static methods**!

#### Static Method To Display Horizontal Rule

```java
// Static method that is going to display a simple horizontal rule
public static void displayRule(int num_of_char) {
	System.out.printf("\n\t");

	// Iterate through the number of characters
	for (int i = 0; i < num_of_char; i++) {
	  System.out.printf("-");
	}

	System.out.printf("\n\n");
}
```

- Usage:

```java
// Our main class
public class Main {

  // Our main function
  public static void main(String[] args) {
    // Create first object of the parent class of `Vehicle`
    Vehicle vehicle1 = new Vehicle("Mazda", "RX-7 FD", 500000, "Canary Yellow", 65, 1, 1, 1300);

    // Use the static method `displayRule` WITHOUT creating any objects
    Vehicle.displayRule(50);
  }
}
```

- Therefore, this is going to output something along lines of this:

> *Get It! "Along The Lines..."*

```console
        --------------------------------------------------
```

> [!NOTE]
> If you want to know when you are going to have to use a `static` method or a method related to the **object** of a class.
>
 > Head over to the '[[Python - Object Oriented Programming Basics#Static Methods | Python - Object Oriented Programming Basics]]' '*Static Methods*' heading!

### Methods Related To Parent Class

#### Display All Information About Vehicle

```java
  // Method that will be able to display the information about vehicle
  public void displayInfo() {
    displayRule(35);
    System.out.println("\t\tVehicle Information");
    displayRule(35);

    // Display the individual attributes
    System.out.println("\t\tBrand: " + brand);
    System.out.println("\t\tModel: " + model);
    System.out.println("\t\tPrice: " + price);
    System.out.println("\t\tColour: " + colour);
    System.out.println("\t\tHealth: " + health);
    System.out.println("\t\tEngine Number: " + engineNum);
    System.out.println("\t\tChassis Number: " + chassisNum);
    System.out.println("\t\tEngine Capacity: " + engineCapacity);

    displayRule(35);
  }
```

- Usage:

```java
// Our main class
public class Main {

  // Our main function
  public static void main(String[] args) {
    // Create first object of the parent class of `Vehicle`
    Vehicle vehicle1 = new Vehicle("Mazda", "RX-7 FD", 500000, "Canary Yellow", 65, 1, 1, 1300);

    // Display all the information about `vehicle1`
    vehicle1.displayInfo();
  }
}
```

- This is the output after running the above function:

```console
        -----------------------------------

                Vehicle Information

        -----------------------------------

                Brand: Mazda
                Model: RX-7 FD
                Price: 500000.0
                Colour: Canary Yellow
                Health: 65
                Engine Number: 1
                Chassis Number: 1
                Engine Capacity: 1300

        -----------------------------------
```

> [!WARNING]
> This is <strong> <span style="color: red;"> not</span> </strong> a '**getter**' function!
>
> This just **displays** / **presents** data to the user about the attributes of the vehicle instead of <span style="color: orange;"> returning</span> a specific *value* of an **attribute** using the `return` keyword.
>
 > Again, `void` $\Rightarrow$ **no** `return` $\Rightarrow$ **NOT** a *Getter*!

#### Lock and Unlock Vehicle

- Method to **lock** the *vehicle*:

```java
// Method that is going to be able to lock the vehicle
public void lock() {
	// Check if the vehicle has already been locked
	if (locked) {
	  // Output appropriate message
	  System.out.println("\n\t<< Vehicle Has Already Been Locked!!!  > \n");
	
	  // If the vehicle has not yet been locked ==> lock the doors
	} else {
	  locked = true;
	
	  // Output appropriate message
	  System.out.println("\n\t<< Vehicle Has Now Been Locked!!!  > \n");
	}
}
```

- Method to _**un**lock_ the *vehicle*:

```java
// Method that is going to be able to unlock the vehicle
public void unlock() {
  // Check if the vehicle has already been unlocked
  if (!locked) {
    // Output appropriate message
    System.out.println("\n\t<< Vehicle Has Already Been Unlocked!!!  > \n");

    // If the vehicle has not yet been unlocked ==> unlock the doors
  } else {
    locked = false;

    // Output appropriate message
    System.out.println("\n\t<< Vehicle Has Now Been Unlocked!!!  > \n");
  }
}
```

- Show usage of **both** `unlock` and `lock`:

```java
// Our main class
public class Main {

  // Our main function
  public static void main(String[] args) {
    // Create first object of the parent class of `Vehicle`
    Vehicle vehicle1 = new Vehicle("Mazda", "RX-7 FD", 500000, "Canary Yellow", 65, 1, 1, 1300);

    // Get the current lock status of the `vehicle1`
    System.out.println("Current Lock Status Of Vehicle: " + vehicle1.locked);

    // Call the method to unlock the vehicle
    vehicle1.unlock();

    // get the current lock status after unlocking vehicle
    System.out.println("Current Lock Status Of Vehicle: " + vehicle1.locked);

    // Call the method to lock the vehicle
    vehicle1.lock();

    // Get the current lock status after locking vehicle
    System.out.println("Current Lock Status Of Vehicle: " + vehicle1.locked);
  }
}
```

- Therefore, this is the output that we are going to get:

```console
Current Lock Status Of Vehicle: true

        << Vehicle Has Now Been Unlocked!!!  > 

Current Lock Status Of Vehicle: false

        << Vehicle Has Now Been Locked!!!  > 

Current Lock Status Of Vehicle: true
```

#### Start and Stop Engine

- Method to **start** the *engine*:

```java
// Method that is going to be able to start the engines of the vehicle
public void startEngine() {
	// Check if the vehicle's engine has already been running
	if (isRunning) {
	  // Output appropriate message
	  System.out.println("\n\t<< Vehicle's Engines Has Already Been Running!!!  > \n");
	
	  // If the vehicle's engine has not yet been running ==> start the engines
	} else {
	  isRunning = true;
	
	  // Output appropriate message
	  System.out.println("\n\t<< Vehicle's Engines Was Started And Now Running!!!  > \n");
	}
}
```

- Method to **stop** the *engine*:

```java
// Method that is going to be able to stop the engines of the vehicle
public void stopEngine() {
	// Check if the vehicle's engine has already been "off"
	if (!isRunning) {
	  // Output appropriate message
	  System.out.println("\n\t<< Vehicle's Engines Has Already Been 'Off'!!!  > \n");
	
	  // If the vehicle's engine has been running ==> stop the engines
	} else {
	  isRunning = false;
	
	  // Output appropriate message
	  System.out.println("\n\t<< Vehicle's Engines Was Stopped!!!  > \n");
	}
}
```

- Show usage of **both** `startEngines` and `stopEngines`:

```java
// Our main class
public class Main {

	// Our main function
	public static void main(String[] args) {
		// Create first object of the parent class of `Vehicle`
		Vehicle vehicle1 = new Vehicle("Mazda", "RX-7 FD", 500000, "Canary Yellow", 65, 1, 1, 1300);
		
		// Get the current engine running status of the `vehicle1`
		System.out.println("Current Engine Running Status Of Vehicle: " + vehicle1.isRunning);
		
		// Call the method to start the engines the vehicle
		vehicle1.startEngine();
		
		// Get the current engine running status after starting engines vehicle
		System.out.println("Current Engine Running Status Of Vehicle: " + vehicle1.isRunning);
		
		// Call the method to stop the engines the vehicle
		vehicle1.stopEngine();
		
		// Get the current engine running status of the `vehicle1` after shutdown
		System.out.println("Current Engine Running Status Of Vehicle: " + vehicle1.isRunning);
	}
}
```

- Therefore this is the output that we get:

```console
Current Engine Running Status Of Vehicle: false

        << Vehicle's Engines Was Started And Now Running!!!  > 

Current Engine Running Status Of Vehicle: true

        << Vehicle's Engines Was Stopped!!!  > 

Current Engine Running Status Of Vehicle: false
```

#### Drive and Brake Vehicle

- Method to **drive** the *vehicle*:

```java
  // Method that is going to allow the vehicle to drive
  public void drive(Scanner scanner) {
    // First check if the vehicle has fuel to start with
    if (fuelLevel == 0) {
      // Output appropriate message
      System.out.println("\n\t<< Please Refuel Vehicle!!!  > \n");

      // Return the to "main" function
      return;
    }

    // If the vehicle's engines are not running
    if (!isRunning) {
      // Output appropriate message
      System.out.println("\n\t<< Engines Has Not Yet Been Started - Fuel Level Good!!!  > \n");

      // Ask the user if he / she wants to start the engines
      System.out.print("Do You Want To Start The Engines[y/n]: ");
      // NOTE: as `.next()` takes in a string... Use `.charAt(0)` to get character
      char user_input = scanner.next().charAt(0);

      // If the user does NOT want to start the engines
      if (Character.toLowerCase(user_input) != 'y') {
        // Return the to "main" function
        return;
      }

      // Change the current running status
      isRunning = true;
    }

    // Check if we have a minimum level of fuel to be able to drive the car
    if (fuelLevel < 10) {
      // Output appropriate message
      System.out.println("\n\t<< The Vehicle Need To Be Refueled!!!  > \n");
    }

    // If the vehicle has fuel and engines has already been started
    System.out.println("\n\t== The Vehicle Is Being Driven!!! ==\n");

    // Decrease the fuel level by '5' but don't let it go below '0'
    fuelLevel = Math.max(0, fuelLevel - 5);
  }
```

- Method to "_**brake**_" the *vehicle*:

```java
  // Method that is going to allow the vehicle to brake
  public void brake() {
    // Display a simple message that will show vehicle is braking
    System.out.println("\n\t== The Vehicle Is Slowing Down / Braking! ==\n");
  }
```

- Show usage of **both** `drive` and `brake`:

> Yes! I did *import* the `java.util.Scanner` package!

```java
// Our main class
public class Main {

  // Our main function
  public static void main(String[] args) {
    // Declare scanner that will read user input from 'stdin'
    Scanner scanner = new Scanner(System.in);

    // Create first object of the parent class of `Vehicle`
    Vehicle vehicle1 = new Vehicle("Mazda", "RX-7 FD", 500000, "Canary Yellow", 65, 1, 1, 1300);

    // Display the current fuel level of `vehicle1`
    System.out.println("\nCurrent Fuel Level ( Before Driving ): " + vehicle1.fuelLevel);

    // Call the method to start the engines
    vehicle1.startEngines();

    // Call the method to drive the vehicle
    vehicle1.drive(scanner);

    // Call the method to brake the vehicle
    vehicle1.brake();

    // Call the method to stop the engines
    vehicle1.stopEngines();

    // Display the current fuel level after driving
    System.out.println("\nCurrent Fuel Level ( After Driving ): " + vehicle1.fuelLevel);

    // close the scanner object
    scanner.close();
  }
}
```

- Therefore this is the output that we get:

```console
Current Fuel Level ( Before Driving ): 50

        << Vehicle's Engines Was Started And Now Running!!!  > 


        == The Vehicle Is Being Driven!!! ==


        == The Vehicle Is Slowing Down / Braking! ==


        << Vehicle's Engines Was Stopped!!!  > 


Current Fuel Level ( After Driving ): 45
```

#### Refuel Vehicle

```java
  // Method that is going to allow us to refuel the vehicle
  public void refuel() {
    // Check if the tank if already full for vehicle
    if (fuelLevel == 100) {
      // Output appropriate message
      System.out.println("\n\t<< Vehicle's Fuel Tank Already Full!!!  > \n");

      // if the fuel level for vehicle is less than '100'
    } else if (fuelLevel < 100) {
      // Output appropriate message
      System.out.println("\n\t== Refuelling The Vehicle ==\n");

      // Increase the fuel level by '10' but don't let it go above 100
      fuelLevel = Math.min(fuelLevel + 10, 100);

    }
  }
```

- Usage:

```java
// Our main class
public class Main {

  // Our main function
  public static void main(String[] args) {
    // Create first object of the parent class of `Vehicle`
    Vehicle vehicle1 = new Vehicle("Mazda", "RX-7 FD", 500000, "Canary Yellow", 65, 1, 1, 1300);

    // Change the fuel level of `vehicle1`
    vehicle1.fuelLevel = 20;

    // Display the current fuel level of `vehicle1`
    System.out.println("\nCurrent Fuel Level ( Before Driving ): " + vehicle1.fuelLevel);

    // Iterate through the loop 3 times
    for (int i = 0; i < 3; i++) {
      // Call the method to refuel the vehicle
      vehicle1.refuel();
    }

    // Display the current fuel level after driving
    System.out.println("\nCurrent Fuel Level ( After Driving ): " + vehicle1.fuelLevel);
  }
}
```

- Therefore this is the output that we get:

```console
Current Fuel Level ( Before Driving ): 20

        == Refuelling The Vehicle ==


        == Refuelling The Vehicle ==


        == Refuelling The Vehicle ==


Current Fuel Level ( After Driving ): 50
```

#### Methods For Repairing Vehicle

##### Method Overloading ( Repair Vehicle )

- **General** Service Method:

```java
  // Method that is going to handle general repairs
  public void repair() {
    // Check if the vehicle is already repaired
    if (health > = 70) {
      // Output appropriate message
      System.out.println("\n\t<< Vehicle's Already Repaired!!!  > \n");

      // Check if the vehicle need repairing
    } else {
      // Increase the health level by '10' but don't let it go above 100
      health = Math.min(health + 10, 100);

      // Output appropriate message
      System.out.println("\n\t== Repairing The Vehicle ==\n");
    }
  }
```

- **General** Service Usage:

```java
// Our main class
public class Main {

  // Our main function
  public static void main(String[] args) {
    // Create first object of the parent class of `Vehicle`
    Vehicle vehicle1 = new Vehicle("Mazda", "RX-7 FD", 500000, "Canary Yellow", 65, 1, 1, 1300);

    // Change the health level of `vehicle1`
    vehicle1.health = 50;

    // Display the current health level of `vehicle1`
    System.out.println("\nCurrent Health Level ( Before Repairing ): " + vehicle1.health);

    // Iterate through the loop 3 times
    for (int i = 0; i < 3; i++) {
      // Call the method to repair the vehicle
      vehicle1.repair();
    }

    // Display the current health level after driving
    System.out.println("\nCurrent Health Level ( After Health ): " + vehicle1.health);
  }
```

- **General** Service Output:

```console
Current Health Level ( Before Repairing ): 50

        == Repairing The Vehicle ==


        == Repairing The Vehicle ==


        << Vehicle's Already Repaired!!!  > 


Current Health Level ( After Health ): 70
```

- **Specific** Service Method:

```java
  // Method to that is going to handle specific repairs
  public void repair(String partName, int estimatedCost) {
    // Output appropriate message
    System.out.println("\n\t== Part Name: " + partName + " | Estimated Cost: " + estimatedCost + " ==\n");
  }
```

- **Specific** Service Usage:

```java
// Our main class
public class Main {

  // Our main function
  public static void main(String[] args) {
    // Create first object of the parent class of `Vehicle`
    Vehicle vehicle1 = new Vehicle("Mazda", "RX-7 FD", 500000, "Canary Yellow", 65, 1, 1, 1300);

    // Change the health level of `vehicle1`
    vehicle1.health = 50;

    // Display the current health level of `vehicle1`
    System.out.println("\nCurrent Health Level ( Before Repairing ): " + vehicle1.health);

    // Iterate through the loop 3 times
    for (int i = 0; i < 3; i++) {
      // Call the method to repair the vehicle
      vehicle1.repair("Gear Lever", 700);
    }

    // Display the current health level after driving
    System.out.println("\nCurrent Health Level ( After Health ): " + vehicle1.health);
  }
}
```

- **Specific** Service Output:

```console
Current Health Level ( Before Repairing ): 50

        == Part Name: Gear Lever | Estimated Cost: 700 ==


        == Part Name: Gear Lever | Estimated Cost: 700 ==


        == Part Name: Gear Lever | Estimated Cost: 700 ==


Current Health Level ( After Health ): 50
```

---

# Creation of Subclass

## Implementing The Child Subclass

```java
class Car extends Vehicle {
  // Declare variables so that we can hold attributes of object 'Car'
  int numOfDoors;

  // Declare class's instance variable here
  String trunkStatus;

  // Constructor to assign those variables to the object 'Car'
  public Car(
      String brand,
      String model,
      double price,
      String colour,
      int health,
      int engineNum,
      int chassisNum,
      int engineCapacity,
      int numOfDoors) {

    // Set the vehicle's attributes to the 'Vehicle' class
    super(brand, model, price, colour, health, engineNum, chassisNum, engineCapacity);

    // Initialise specific attributes for the 'Car' class
    this.numOfDoors = numOfDoors;

    // Class instance variable for 'Car' object
    this.trunkStatus = "closed";
  }

  // Specific method for 'Car' class to open the object's trunk
  public void openTrunk() {
    // Check if the car's trunk has already been opened
    if (trunkStatus.equals("opened")) {
      // Output appropriate message
      System.out.println("\n\t<< Car's Trunk Has Already Been Opened!!! >>\n");

      // If the car's trunked has not yet been opened ==> open the trunk
    } else {
      trunkStatus = "opened";

      // Output appropriate message
      System.out.println("\n\t<< Car's Trunk Has Been Opened!!! >>\n");
    }
  }

  // Specific method for 'Car' class to close the object's trunk
  public void closeTrunk() {
    // Check if the car's trunk has already been closed
    if (trunkStatus.equals("closed")) {
      // Output appropriate message
      System.out.println("\n\t<< Car's Trunk Has Already Been Closed!!! >>\n");

      // If the car's trunked has not yet been closed ==> close the trunk
    } else {
      trunkStatus = "closed";

      // Output appropriate message
      System.out.println("\n\t<< Car's Trunk Has Been Closed!!! >>\n");
    }
  }
}
```

Given that we already know how to create **methods** for a `class`.

I simply add the **methods** for the `Car` *subclass* in the code block above instead of making a separate heading in this note for it.

> [!NOTE] Relationships
> 
> In terms of theory, this is an '**IS-A**' relationship!
> 
> Whereby we say that: "*`Car` is a `Vehicle`*".

## Create Instance Of Child Subclass

Let us now go ahead and create our first **object** of the **child** class of `Car`.

```java
// Our main class
public class Main {
  // Our main function
  public static void main(String[] args) {
    // Create first object of the cihld class of `Car`
    Car car1 = new Car("Nissan", "R32 GTR", 600000, "Black", 55, 1, 1, 2568, 2);
  }
}
```

### Calling Some Methods On Child Object

```java
// Our main class
public class Main {
  // Our main function
  public static void main(String[] args) {
    // Declare scanner that will read user input from 'stdin'
    Scanner scanner = new Scanner(System.in);

    // Create first object of the parent class of `Vehicle`
    Vehicle vehicle1 = new Vehicle("Mazda", "RX-7 FD", 500000, "Canary Yellow", 65, 1, 1, 1300);

    // Create first object of the child class of `Car`
    Car car1 = new Car("Nissan", "R32 GTR", 600000, "Black", 55, 1, 1, 2568, 2);

    // Call parent methods of 'Vehicle' class on the 'Car' child class
    car1.displayInfo();

    Vehicle.displayRule(55);

    car1.unlock();
    car1.startEngines();
    car1.drive(scanner);

    Vehicle.displayRule(55);

    car1.brake();
    car1.stopEngines();

    for (int i = 0; i < 3; i++) {
      car1.refuel();
    }

    Vehicle.displayRule(55);

    car1.startEngines();
    car1.drive(scanner);

    Vehicle.displayRule(55);

    car1.brake();
    car1.stopEngines();

    Vehicle.displayRule(55);

    car1.unlock();

    // call 'Car' child class specific methods
    car1.openTrunk();

    for (int i = 0; i < 2; i++) {
      car1.closeTrunk();
    }

    car1.lock();

    Vehicle.displayRule(55);

    // close the scanner object
    scanner.close();
  }
}
```

- This is the output after running the above *updated* `main` function:

```console
	-----------------------------------

		Vehicle Information

	-----------------------------------

		Brand: Nissan
		Model: R32 GTR
		Price: 600000.0
		Colour: Black
		Health: 55
		Engine Number: 1
		Chassis Number: 1
		Engine Capacity: 2568

	-----------------------------------


	-------------------------------------------------------


	<< Vehicle Has Now Been Unlocked!!! >>


	<< Vehicle's Engines Was Started And Now Running!!! >>


	== The Vehicle Is Being Driven!!! ==


	-------------------------------------------------------


	== The Vehicle Is Slowing Down / Braking! ==


	<< Vehicle's Engines Was Stopped!!! >>


	== Refuelling The Vehicle ==


	== Refuelling The Vehicle ==


	== Refuelling The Vehicle ==


	-------------------------------------------------------


	<< Vehicle's Engines Was Started And Now Running!!! >>


	== The Vehicle Is Being Driven!!! ==


	-------------------------------------------------------


	== The Vehicle Is Slowing Down / Braking! ==


	<< Vehicle's Engines Was Stopped!!! >>


	-------------------------------------------------------


	<< Vehicle Has Already Been Unlocked!!! >>


	<< Car's Trunk Has Been Opened!!! >>


	<< Car's Trunk Has Been Closed!!! >>


	<< Car's Trunk Has Already Been Closed!!! >>


	<< Vehicle Has Now Been Locked!!! >>


	-------------------------------------------------------
```

## Method Overriding

### Drive and Brake

- Method to **drive** the *car*:

```java
  /*
   * INFO: Overridden `drive` method for the 'Car' subclass.
   * WARNING: The importance of `@Override`.
   * This is an optional "decorator" in Java, but it is better to include it!
   * In our case, we could do WITHOUT it simply because the method name and
   * parameters match.
   * However, if we made a typo like `Drive`, it wouldn't apply our
   * changes when calling `<carObjectInstanceName>.drive()`, and would
   * run the Vehicle's `drive` method instead!
   */
  @Override
  public void drive(Scanner scanner) {
    // Check if the trunk is open or now
    if (this.trunkStatus.equals("opened")) {
      // Output appropriate message
      System.out.println("\n\t<< Cannot Drive: Trunk Is Open!!! >>\n");

      // Return to the "main" function
      return;
    }

    // 'Car' objects drive in 'Sport' mode only
    System.out.println("\n\t== Car Drive Mode: Sport ==\n");

    // Get the current fuel level of the 'Car' object
    int fuelBeforeDrive = this.fuelLevel;

    // NOTE: Call the actual implementation from Vehicle's `drive` method
    // Therefore, in this way; we can still get the implementation of `drive`
    // WITHOUT needing to re-write everything again!
    // WARNING: We added the line below here because:
    // 1. We need to check if the trunk is open first
    // 2. We need to make sure that the we override the fuel level
    // ( given 'Sport' mode... We should remove more fuel )
    super.drive(scanner);

    // Update the fuel level in addition to the Vehicle's `drive` method fuel burn
    // This means that consume fuel in `super().drive()` and also Car's `drive`
    // method
    if (this.fuelLevel < fuelBeforeDrive) {
      this.fuelLevel = Math.max(0, this.fuelLevel - 2);
    }
  }
```

- Method to "_**brake**_" the *car*:

```java
  // INFO: Overriden `brake` method for the 'Car' subclass
  @Override
  public void brake() {
    // NOTE: Call the actual implementation from Vehicle's `brake` method
    super.brake();

    // 'Car' objects has ABS engaged ==> display it
    System.out.println("\t== ABS Engaged: Controlled Braking ==\n");
  }
```

- Show usage of **both** `drive` and `brake`:

```java
// Our main class
public class Main {
  // Our main function
  public static void main(String[] args) {
    // Declare scanner that will read user input from 'stdin'
    Scanner scanner = new Scanner(System.in);

    // Create first object of the child class of `Car`
    Car car1 = new Car("Nissan", "R32 GTR", 600000, "Black", 55, 1, 1, 2568, 2);

    // Display the current fuel level of `car1`
    System.out.println("\nCurrent Fuel Level ( Before Driving ): " + car1.fuelLevel);

    // Call the method to start the engines
    car1.startEngines();

    // Call the method to drive the vehicle
    car1.drive(scanner);

    // Call the method to brake the vehicle
    car1.brake();

    // Call the method to stop the engines
    car1.stopEngines();

    // Display the current fuel level after driving
    System.out.println("\nCurrent Fuel Level ( After Driving ): " + car1.fuelLevel);

    // close the scanner object
    scanner.close();
  }
}
```

- Therefore this is the output that we get:

```console
Current Fuel Level ( Before Driving ): 50

	<< Vehicle's Engines Was Started And Now Running!!! >>


	== Car Drive Mode: Sport ==


	== The Vehicle Is Being Driven!!! ==


	== The Vehicle Is Slowing Down / Braking! ==

	== ABS Engaged: Controlled Braking ==


	<< Vehicle's Engines Was Stopped!!! >>


Current Fuel Level ( After Driving ): 43
```

> [!SUCCESS]
> We can definitely see that instead of getting a fuel level of '45' **after** driving. We instead get a fuel level of '43' which is $50 - 7 = 43$!

#### The Override Keyword

Compared to [[Python - Object Oriented Programming Basics | Python]]'s `@override` **decorator**, which by the way, needs to be imported from the 'typing' module.

Our `@Override` *decorator* in Java does play a **significant** role!

The thing about the `@Override` decorator in Java its that it pretty special in terms that it can *verify* a **subclass**'s method to becoming an "*overridden*" method.

> Basically the `@Override` *decorator* is a **compiler check**!

Let's take our `brake` method as example to show this. In our `Car` **subclass**, we wrote this ( *method signature / definition* ):

```java
  @Override
  public void brake() { ... }
```

Therefore, we were **able** to *compile* and *run* the program **without** any issues.

Let's say that instead of `brake` we change the function name to `braking`; something like this:

```java
  @Override
  public void braking() { ... }
```

Well, only changing the name of the method in our `Car` subclass, you are going to see *this* when you try compiling... You should see this **error**:

```console
Main.java:342: error: braking() in Car does not override or implement a method from a supertype
  @Override
  ^
1 error
make: *** [Makefile:4: compile] Error 1
```

> Yeah I know that my `Main.java` file is getting pretty huge ( *that's what she said* )!

#### The Super Function

The `super` **keyword** in this case is pretty self-explanatory. Where it allows one to **use** the *implementation* and *logic* written in the **parent** class and simply call it inside the **child** class.

This means that we **don't** have to *re-write* anything found in the original, parent class method.

> [!NOTE]
> Now, I am not telling you that you "*need*" to use the `super.methodName()` statement.
> 
> If you want to **completely** *re-write* the function in its entirety... <span style="color: lime">You Could</span>!

> [!WARNING]
> The `@Override` *decorator* and `super` *keyword* are just **tools**.
> 
> Therefore, they are **not** a *requirement* for the "*showing*" 'Inheritance' in both Java and [[Python - Object Oriented Programming Basics | Python]].

# Polymorphism?

From what we already know in our little adventure in '[[Introduction to Object Oriented Programming#Polymorphism | Introduction to Object Oriented Programming]]'.

Polymorphism is basically '**Method Overloading**' and '**Method Overriding**'.

Hence, can we say that we already know about '*Polymorphism*' itself?

> The answer is **no**!

Method Overloading and Method overriding is just the "*tool*" that **allows** for *Polymorphism* but it does **not**, *by itself*, show the overall concept well.

> Let's take a little example and then you should be able to understand what I am trying to say.

```java
// Our main class
public class Main {
  // Our main function
  public static void main(String[] args) {
    // Create an array list to hold objects of different classes
    List<Vehicle> garage = new ArrayList<>();

    // Create object of the child class of `Vehicle` and add to `garage` array-list
    garage.add(new Vehicle("Mazda", "RX-7 FD", 500000, "Canary Yellow", 65, 1, 1, 1300));
    // Create object of the child class of `Car` and add to `garage` array-list
    garage.add(new Car("Nissan", "R32 GTR", 600000, "Black", 55, 1, 1, 2568, 2));

    // INFO: Polymorphism in action
    // Treat all the objects, inside the list, as a genaric vehicle
    for (Vehicle vehicle : garage) {
      // Call the `brake` method on these "vehicles"
      vehicle.brake();

      // display horizontal rule using static method
      Vehicle.displayRule(50);
    }
  }
}
```

> Yes! I did *import* the `java.util.List` and `java.util.ArrayList` package(s)!

As you can see in the above example, we created a `list` that contains an *instance* of **both** our `Vehicle` and `Car` class respectively.

Then we simply called the `brake` *method* on **both** of them and therefore, we get the following output:

```console

	-- The Vehicle Is Slowing Down / Braking! --


	 -------------------------------------------------- 


	-- The Vehicle Is Slowing Down / Braking! --

	-- ABS Engaged: Controlled Braking --


	 -------------------------------------------------- 
```

> [!BUG]
> The output is different right, instead of `=` you see `-`.
> 
> Given that I use the [dataview](https://github.com/blacksmithgu/obsidian-dataview) plugin ( *which I plan to remove one day and use Obsidian Bases* ) the `=` is a reserved work for code blocks.
> 
> This is the reason as to why I change it from `=` to `-`.
> 
> > The original output did **line-up** with the code!

> [!INFO] What's so special about that?
> 
> Its the idea of "*One interface, many implementation*!"
> 
> Where, in our case, the **interface** is the *function* / *method* and the *objects* are the different **implementations**!
> 
> Thus, in my own words:
> 
> > "its the idea of overall idea of a single function be able to do / act differently on different objects / classes that it can work on"

# Encapsulation

> Refer to the note '[[Introduction to Object Oriented Programming#Encapsulation | ]]' for more information.

As the word implies; we are going to "*encapsulate*" our **data** and hence, **hide** our data from other `class`es so that only a **selected** few can modify them.

> This is what we mean by "*data hiding*"!

Therefore, to avoid data being manipulated **without** our *consent*. We therefore, provide `public` methods like '**getters**' and '**setters**' that can work on these data *in a specific manner*.

Let's modify the above `main` function so that it looks like this:

```java
// Our main class
public class Main {
  // Our main function
  public static void main(String[] args) {
    // Create an array list to hold objects of different classes
    List<Vehicle> garage = new ArrayList<>();

    // Create object of the child class of `Vehicle` and add to `garage` array-list
    garage.add(new Vehicle("Mazda", "RX-7 FD", 500000, "Canary Yellow", 65, 1, 1, 1300));
    // Create object of the child class of `Car` and add to `garage` array-list
    garage.add(new Car("Nissan", "R32 GTR", 600000, "Black", 55, 1, 1, 2568, 2));

    // Showing "Encapsulation" ( before implementation )

    // Display the fuel level of the 'Car' object before changing
    System.out.println("( Before Encapsulation ) Fuel Level Before Change: " + garage.get(0).fuelLevel);

    // Change the fuel level ( directly ) for our 'Car' object
    garage.get(0).fuelLevel = 100;

    // Display the fuel level of the 'Car' object after changing
    System.out.println("( Before Encapsulation ) Fuel Level After Change: " + garage.get(0).fuelLevel);
  }
}
```

- The output of the above `main` function is going look like this:

```console
( Before Encapsulation ) Fuel Level Before Change: 50
( Before Encapsulation ) Fuel Level After Change: 100
```

As you can see we can simply change the `fuelLevel` [[#Instance / Class Variables | class instance variable]] was **able** to be *modified* **without** any issues inside the `Main` class!

> Well, we are now going to try to stop that from happening!

## Hiding The Fuel Level

We are now going to modify the `fuelLevel` class **instance** variable so that we need to use '*getters*' and '*setters*' to be able to **get** and **update** the value.

- Modify the variable definition of `fuelLevel` to be `private`:

```java
  // Declare class's instance variable here
  boolean isRunning;
  boolean locked;

  // Update the fuel level to be a private class / instance variable
  private int fuelLevel;

  // Constructor to assign those variables to the object
```

### Comparing

Running the above code found inside the `main` function again, we should get an error:

```console
Main.java:330: error: fuelLevel has private access in Vehicle
    int fuelBeforeDrive = this.fuelLevel;
                              ^
Main.java:344: error: fuelLevel has private access in Vehicle
    if (this.fuelLevel < fuelBeforeDrive) {
            ^
Main.java:345: error: fuelLevel has private access in Vehicle
      this.fuelLevel = Math.max(0, this.fuelLevel - 2);
          ^
Main.java:345: error: fuelLevel has private access in Vehicle
      this.fuelLevel = Math.max(0, this.fuelLevel - 2);
                                       ^
Main.java:375: error: fuelLevel has private access in Vehicle
    System.out.println("( Before Encapsulation ) Fuel Level Before Change: " + garage.get(0).fuelLevel);
                                                                                            ^
Main.java:378: error: fuelLevel has private access in Vehicle
    garage.get(0).fuelLevel = 100;
                 ^
Main.java:381: error: fuelLevel has private access in Vehicle
    System.out.println("( Before Encapsulation ) Fuel Level After Change: " + garage.get(0).fuelLevel);
                                                                                           ^
7 errors
make: *** [Makefile:4: compile] Error 1
```

> Very Nice!

### Getter Method - Fuel Level

We are now going to make a method that is will be `public` and therefore be able to be used by other `class`es so that we are able to "**extract**" the values for `fuelLevel`.

```java
  // Getter Method for `fuelLevel` to get fuel level of vehicle
  public int getFuelLevel() {
    // Simply return the fuel level to whoever is asking for it
    return this.fuelLevel;
  }
```

> [!WARNING]
> This means that *every place* **outside** the `Vehicle` class that currently uses `this.fuelLevel` like in our `drive` method of our `Car` class.
> 
> We need to **replace** `this.fuelLevel` with `getFuelLevel`!
> 
> > [!NOTE]
> > Given that `fuelLevel` was *defined* **inside** the `Vehicle` class.
> > 
> > This means that we **don't** need to do anything with the usage of `fuelLevel` in the *methods* of `Vehicle` class.

### Setter Method - Fuel Level

Similarly, we need a new way to *set* the value for `fuelLevel` from **other** `class`es like `Car`.

```java
  // Setter Method for `fuelLevel` to update fuel level of vehicle
  public void setFuelLevel(int userFuelLevel) {
    // Update the `fuelLevel` through the parameter / argument
    this.fuelLevel = userFuelLevel;
  }
```

### Getter and Setter Usage

- Modify our `drive` method for `Car` class:

```java
  @Override
  public void drive(Scanner scanner) {
    if (this.trunkStatus.equals("opened")) {
      System.out.println("\n\t<< Cannot Drive: Trunk Is Open!!! >>\n");

      return;
    }

    System.out.println("\n\t== Car Drive Mode: Sport ==\n");

    // Get the current fuel level of the 'Car' object
    // INFO: Update to use 'getter' method from `Vehicle`
    int fuelBeforeDrive = this.getFuelLevel();
	
    super.drive(scanner);

    if (getFuelLevel() < fuelBeforeDrive) {
      // INFO: Update to use 'getter' and 'setter' method from `Vehicle`

      // Therefore, create the variable to be passed as argument
      int userFuelLevel = Math.max(0, getFuelLevel() - 2);

      // INFO: Use `setFuelLevel` method to set the new fuel level
      setFuelLevel(userFuelLevel);
    }
  }
```

- *Updated* `main` function:

```java
// Our main class
public class Main {
  // Our main function
  public static void main(String[] args) {
    // Create an array list to hold objects of different classes
    List<Vehicle> garage = new ArrayList<>();

    // Create object of the child class of `Vehicle` and add to `garage` array-list
    garage.add(new Vehicle("Mazda", "RX-7 FD", 500000, "Canary Yellow", 65, 1, 1, 1300));
    // Create object of the child class of `Car` and add to `garage` array-list
    garage.add(new Car("Nissan", "R32 GTR", 600000, "Black", 55, 1, 1, 2568, 2));

    // Showing "Encapsulation" ( after implementation )

    // Display the fuel level of the 'Car' object before changing
    System.out.println("( After Encapsulation ) Fuel Level Before Change: " + garage.get(0).getFuelLevel());

    // Change the fuel level ( directly ) for our 'Car' object

    garage.get(0).setFuelLevel(100);

    // Display the fuel level of the 'Car' object after changing
    System.out.println("( After Encapsulation ) Fuel Level After Change: " + garage.get(0).getFuelLevel());
  }
}
```

- Hence, instead of an error, we do get our correct output:

```console
( After Encapsulation ) Fuel Level Before Change: 50
( After Encapsulation ) Fuel Level After Change: 100
```

# Abstraction

Abstraction is about focusing on **"What"** an object does instead of **"How"** it does it.

- **The Blueprint:** It acts as a mandatory template. By marking a class as `abstract`, we prevent anyone from creating a generic, "half-finished" version of that object (e.g., you can't create a 'Vehicle', only a 'Car').
- **The Contract:** It forces subclasses to implement certain methods. If the parent says `drive()` is abstract, the child **must** provide the code for it.
- **The Goal:** It ensures consistency. No matter how many types of Vehicles we add, we are guaranteed they will all have the same essential methods, making our loops and logic much safer.

> [!WARNING]
> The above note was created with [Gemini](https://gemini.google.com).
> 
> I think its good enough for this explanation as I did provide my own shitty understanding first and then ask Gemini to refine it.
> 
> > But I still don't really understand the "*abstraction*" completed!

Currently, we have *simple*, _**vague**_ `Vehicle` class that creates, well a "*vehicle*" **object**.

Compared the the `Car` class that `drive`s in 'Sport Mode'

Therefore, you could say that the `Vehicle` class is simply a *template* / *guide* for the `Car`.

> Meaning that other `class`es are going to be based on `Vehicle` ( *in our case* ).

Therefore, why not enforce that rule? Well, we can simply **use** the `abstract` *keyword* in front of the `Vehicle` class definition!

```java
// Our 'Vehicle' class definition
// NOTE: Updated 'Vehicle' class definition to be a template for others
abstract class Vehicle { ... }
```

> The **implementation** of the class stays the same!

> [!WARNING] The 'Vehicle' Class Becomes A Template / Structure!
> 
> Yes, as from now on; you will <strong><span style="color: red;">not</span></strong> be able to *create* / *instantiate* and object with the `Vehicle` type!
> 
> The `Vehicle` class as officially become an `abstract` class!
> 
> > [!TIP]
> > Therefore, *in our case*, we are going to have to create `Car` objects that basically **inherits** *data* from the `Vehicle` class.
> > 
> > If you look it in that way; the `Vehicle` class did become a "*template*".

## Further Example

Let's create a **abstract method** that will need to be implemented by other classes.

- In our `Vehicle` class:

```java
  // Abstract method to be implemented by other "inherited" classes
  public abstract void displayDisplacement();
```

- Therefore using *Method Overriding*; **implementation** in `Car` class:

```java
  // Implementation of `displayDisplacement` method in `Car` class
  @Override
  public void displayDisplacement() {
    // Display the displacement of the 'Car' object
    System.out.println("\n\t== Engine Displacement: " + this.engineCapacity + "cc " + "==\n");
  }
```

- Our *updated* `main` function:

```java
// Our main class
public class Main {
  // Our main function
  public static void main(String[] args) {
    // Create an array list to hold objects of different classes
    List<Vehicle> garage = new ArrayList<>();

    // Create first object of the child class of `Car` and add to `garage`
    garage.add(new Car("Mazda", "RX-7 FD", 500000, "Canary Yellow", 65, 1, 1, 1300, 2));
    // Create second object of the child class of `Car` and add to `garage`
    garage.add(new Car("Nissan", "R32 GTR", 600000, "Black", 55, 1, 1, 2568, 2));

    // Display the engine capacity / displacement of the first 'Car' object
    garage.get(0).displayDisplacement();
  }
}
```

- Therefore, we are going to have this output:

```console
	-- Engine Displacement: 1300cc --
```

> [!BUG]
> Same Obsidian - Dataview error!
> 
> I needed to change the `=` character to `-`!
> 
> Don't worry, the original output was good.

# Multiple Inheritance - Interfaces

In short, **interfaces** are a way to get the ability to have **multiple** inheritance whereby a *child* / sub-class can *inherit* from **multiple** *parent* classes.

Compared to [[Python - Object Oriented Programming Basics | Python]], many languages like Java, Swift, C# **don't** offer multiple inheritance because of the **Diamond Problem**.

> Whereby the *child* class gets **confused** by **conflicting codes** from the *parent* classes.

So in short, `interface`s was created in Java to be **able** to have the *functionality* of **multiple inheritance** without the hassle of conflicting codes between multiple parents.

> [!NOTE] Relationships
> 
> In terms of theory, this is an '**CAN-DO**' relationship!
> 
> Whereby we say that: "*`Car` can have `GPS`*".

- Define the `GPS` interface ( *to be used by sub-classes* ):

```java
// `interface` definition for 'GPS'
interface GPS {
  // Define methods that we want to implement
  // ==> Sub-classes to have to implement
  // INFO: All method inside and interface are `abstract` by default
  void calculateRoute();
}
```

- Implement the `GPS` interface inside the `Car` *child* class ( *updated `Car` class* ).

```java
// "Multiple inheritance" through the use of `interface`
// 'Car' class is a child of 'Vehicle' and has a 'GPS' interface
class Car extends Vehicle implements GPS {
  // INFO: The rest of the code stays the same!

  // Implementation of `calculateRoute` method from the 'GPS' interface
  // Use Method Overriding to implement interface's method(s)
  @Override
  public void calculateRoute() {
    // Display the displacement of the 'Car' object
    System.out.println("\n\t== GPS ( Interface ): Calculating Route ==\n");
  }
}
```

- *Updated* `main` function to show its usage:

```java
// Our main class
public class Main {
  // Our main function
  public static void main(String[] args) {
    // Create a `nissanGTR` 'Car' object
    Car nissanGTR = new Car("Nissan", "R32 GTR", 600000, "Black", 55, 1, 1, 2568, 2);

    // Treat the `nissanGTR` 'Car' object as a 'Vehicle' object
    // INFO: Fun Thing! We can now instantiate object of type 'Vehicle'
    // Again, as you already know, we add `abstract` at the front of 'Vehicle' class
    // Nevertheless, instantiating a 'Vehicle' object directly won't cut it
    Vehicle nissanVehicle = nissanGTR;

    // Treat `nissanGTR` 'Car' object as a device / interface
    GPS gpsDevice = nissanGTR;

    // "Simply ask the device itself / directly to calculate the route"
    gpsDevice.calculateRoute();
  }
}
```

- Therefore, we are going to have this output:

```console
	-- GPS ( Interface ): Calculating Route --
```

> [!BUG]
> Same Obsidian - Dataview error!
> 
> I needed to change the `=` character to `-`!
> 
> Don't worry, the original output was good.

# Composition

This is considered to be a "*rival*" of **inheritance**.

> [!INFO]
> From what [Gemini](https://gemini.google.com) is saying... *Composition* is **favoured** compared to *inheritance*.
> 
> This is because *inheritance* makes your code very **rigid** and **brittle** while *composition* makes your code ( *actually* ) **modular**.

> [!NOTE] Relationships
> 
> In terms of theory, this is an '**HAS-A**' relationship!
> 
> Whereby we say that: "*`Car` has and `Engine`*".

Therefore, what we are basically going to do right now is find **attributes** of the `Vehicle` and then simply check if they are *complex* enough for them to **become** an *object* in-of-itself.

In our case, we are going to be **removing** the `engineNum` and `chassisNum` *attributes* and therefore, make them into their own objects.

- Create the `Engine` and `Chassis` class:

> [!NOTE]
> I know that Java is a **compiled** language and therefore, we could; in theory, write our code anywhere we want to.
> 
> I am going to be defining these classes ( *mentioned above* ) just above the `Vehicle` class.

```java
// Our 'Engine' class definition ==> For composition
class Engine {
  // Declare variables so that we can hold attributes of object 'Engine'
  int engineNum;
  int capacity;

  // Constructor to assign those variables to the object
  public Engine(int engineNum, int capacity) {
    this.engineNum = engineNum;
    this.capacity = capacity;
  }
}

// Our 'Chassis' class definition ==> For composition
class Chassis {
  // Declare variables so that we can hold attributes of object 'Chassis'
  int chassisNum;

  // Constructor to assign those variables to the object
  public Chassis(int chassisNum) {
    this.chassisNum = chassisNum;
  }
}
```

- Update our 'Vehicle' class so as to use the new objects:

```java
abstract class Vehicle {
  // Declare variables so that we can hold attributes of object 'Vehicle'
  String brand;
  String model;
  double price;
  String colour;
  int health;

  // Declare variables from other objects ==> Composition
  // NOTE: This is not going to be used in `main`
  Engine engine;
  Chassis chassis;

  // Declare class's instance variable here
  boolean isRunning;
  boolean locked;

  // Update the fuel level to be a private class / instance variable
  private int fuelLevel;

  // Constructor to assign those variables to the object
  public Vehicle(
      String brand,
      String model,
      double price,
      String colour,
      int health,
      int engineNum,
      int chassisNum,
      int engineCapacity) {
    // Intialise the attributes for an object
    this.brand = brand;
    this.model = model;
    this.price = price;
    this.colour = colour;
    this.health = health;

    // Initialise attributes to be used for composition
    // NOTE: This currently has the 'HAS-A' relationship
    // WARNING: we don't pass `engine` and `chassis` as arguments!
    // this is because of how we use it ( see `main` ).
    this.engine = new Engine(engineNum, engineCapacity);
    this.chassis = new Chassis(chassisNum);

    // Set the values for the class variables
    this.fuelLevel = 50;
    this.isRunning = false;
    this.locked = true;
  }

  // Slight modification to the rest of the code
  
}
```

> [!WARNING]
> After changing the **attributes** to *become* actual **objects**... We are going to have to **access** the *attributes* of those **objects** instead of just using `engineNum`, `engineCapacity` and `chassisNum`.
> 
> > This **has** to be done in both 'Vehicle' and 'Car' class.

- Therefore if we update our `main` function to something like this:

```java
// Our main class
public class Main {
  // Our main function
  public static void main(String[] args) {
    // Create a `nissanGTR` 'Car' object
    Car nissanGTR = new Car("Nissan", "R32 GTR", 600000, "Black", 55, 1, 1, 2568, 2);

    // Use some methods found for 'Car' - 'Vehicle' class
    nissanGTR.displayInfo();
  }
}
```

- Thus, we should get and output like so ( *without errors* ):

```console
	-----------------------------------

		Vehicle Information

	-----------------------------------

		Brand: Nissan
		Model: R32 GTR
		Price: 600000.0
		Colour: Black
		Health: 55
		Engine Number: 1
		Chassis Number: 1
		Engine Capacity: 2568

	-----------------------------------
```

# Aggregation

**Aggregation** is a *type* of **composition** whereby the '*HAS-A*' relationship is **weak**!

Take our `Engine` and `Chassis` code above, we are actually **creating** the 'Engine' and 'Chassis' *object* **inside** the `Vehicle` class.

> *Removing* / *Deleting* a `Vehicle` **also** *removes* its `Engine` and `Chassis` ( **objects** ) automatically.

> [!INFO]
> Therefore we say that **composition** has a *strong* relationship!

Compared to composition, **aggregation** an object could still be *present* when we **delete** / **remove** the `Vehicle` class.

> [!INFO] Asked Gemini To Review The Above Note...
> 
> Both are "HAS-A" relationships, but they differ in **strength** and **lifecycle**.
> - **Composition ( Strong ):** The parts are physically part of the whole. 
> 	- *Example:* Engine & Chassis. If you delete the `Vehicle` object, the `Engine` and `Chassis` usually die with it because they were made specifically for that car.
> - **Aggregation ( Weak ):** The part is an independent entity that is just "associated" with the whole. 
> 	- *Example:* Driver & Vehicle. If you delete the `Vehicle` object, the `Driver` ( object ) still exists in your program. They are just no longer assigned to that car.

> In terms of coding, we are going to show this with a `Driver` class!

- Create our `Driver` class:

```java
// Our 'Driver' class definition ==> For aggregation
class Driver {
  // Declare variables so that we can hold attributes of object 'Driver'
  String driverName;

  // Constructor to assign those variables to the object
  public Driver(String driverName) {
    this.driverName = driverName;
  }
}
```

- Update our `Vehicle` class implementation:

```java
abstract class Vehicle {
  // INFO: The rest of the code stays the same!

  // Declare variables for other objects ==> Aggregation
  Driver vehicleDriver;
  
  // INFO: The rest of the code stays the same!
  }
  
  // INFO: The rest of the code stays the same!
  
  // Method to assign driver to a 'Vehicle' object ==> Aggregation
  public void setDriver(Driver driver) {
    // Get the 'Driver' "object"
    this.vehicleDriver = driver;

    // Output appropriate message
    System.out
        .println(
            "\n\t== Driver Name Of '" + this.brand + " " + this.model + "': " + vehicleDriver.driverName + " ==\n");
  }
}
```

- The *updated* `main` function:

```java
// Our main class
public class Main {
  // Our main function
  public static void main(String[] args) {
    // Create a `nissanGTR` 'Car' object
    Car nissanGTR = new Car("Nissan", "R32 GTR", 600000, "Black", 55, 1, 1, 2568, 2);

    // Create the `champion` 'Driver' object
    Driver champion = new Driver("Lewis Hamilton");

    // Assign the driver object to the car object
    nissanGTR.setDriver(champion);
  }
}
```

- Therefore, we should see this as output:

```console
	-- Driver Name Of 'Nissan R32 GTR': Lewis Hamilton --
```

> [!BUG]
> Same Obsidian - Dataview error!
> 
> I needed to change the `=` character to `-`!
> 
> Don't worry, the original output was good.

---

# Split Files

Currently, if I run a the `wc -l Main.java` command, I am going to get `476` as *output*.

> Well, this means that we have **476** lines of code in our `Main.java` file!

Even though that everything is working fine right now. The way that our `Main.java` file is right now it a bit "*dirty*". Adding more things to it would make it **more** *unreadable*, *unmaintainable* and generally a *pain* to work with!

Therefore, I am going to **split** the *codes* inside the `Main.java` file in different **folders** and **files** so that its **more** *modular*, *easier to work with* and generally better programming practice.

> Let's get started.

> [!WARNING]
> Given that we now have splitted the files into their own "*package*"; we need to add `public` **before** all the *definitions* for the `class`es, `interface`s.
> 
> > Else our `Main.java` file or even things like `Car.java` file which uses the **different** *packages* won't work!

## Project Structure

Here is how the project structure looks like:

```console
 .
├──  components
│   ├──  Chassis.java
│   └──  Engine.java
├──  interfaces
│   └──  GPS.java
├──  Main.java
├──  Makefile
├──  people
│   └──  Driver.java
└──  vehicles
    ├──  Car.java
    └──  Vehicle.java
```

## Files Contents

### Components Folder

- `Chassis.java` File:

```java
package components;

// Our 'Chassis' class definition ==> For composition
public class Chassis {
  // Declare variables so that we can hold attributes of object 'Chassis'
  public int chassisNum;

  // Constructor to assign those variables to the object
  public Chassis(int chassisNum) {
    this.chassisNum = chassisNum;
  }
}
```

- `Engine.java` File:

```java
package components;

// Our 'Engine' class definition ==> For composition
public class Engine {
  // Declare variables so that we can hold attributes of object 'Engine'
  public int engineNum;
  public int capacity;

  // Constructor to assign those variables to the object
  public Engine(int engineNum, int capacity) {
    this.engineNum = engineNum;
    this.capacity = capacity;
  }
}
```

### Interfaces Folder

- `GPS.java` File:

```java
package interfaces;

// `interface` definition for 'GPS'
public interface GPS {
  // Define methods that we want to implement
  // ==> Sub-classes to have to implement
  // INFO: All method inside and interface are `abstract` by default
  void calculateRoute();
}
```

### People Folder

- `Driver.java` File:

```java
package people;

// Our 'Driver' class definition ==> For aggregation
public class Driver {
  // Declare variables so that we can hold attributes of object 'Driver'
  public String driverName;

  // Constructor to assign those variables to the object
  public Driver(String driverName) {
    this.driverName = driverName;
  }
}
```

### Vehicles Folder

- `Vehicles.java` File:

```java
package vehicles;

// import java packages
import java.util.Scanner;

// import our required packages
import components.*;
import people.Driver;

// Our 'Vehicle' class definition
// NOTE: Updated 'Vehicle' class definition to be a template for others
public abstract class Vehicle {
  // Declare variables so that we can hold attributes of object 'Vehicle'
  String brand;
  String model;
  double price;
  String colour;
  int health;

  // Declare variables from other objects ==> Composition
  // NOTE: This is not going to be used in `main`
  Engine engine;
  Chassis chassis;

  // Declare variables for other objects ==> Aggregation
  Driver vehicleDriver;

  // Declare class's instance variable here
  boolean isRunning;
  boolean locked;

  // Update the fuel level to be a private class / instance variable
  private int fuelLevel;

  // Constructor to assign those variables to the object
  public Vehicle(
      String brand,
      String model,
      double price,
      String colour,
      int health,
      int engineNum,
      int chassisNum,
      int engineCapacity) {
    // Intialise the attributes for an object
    this.brand = brand;
    this.model = model;
    this.price = price;
    this.colour = colour;
    this.health = health;

    // Initialise attributes to be used for composition
    // NOTE: This currently has the 'HAS-A' relationship
    // WARNING: we don't pass `engine` and `chassis` as arguments!
    // this is because of how we use it ( see `main` ).
    this.engine = new Engine(engineNum, engineCapacity);
    this.chassis = new Chassis(chassisNum);

    // Set the values for the class variables
    this.fuelLevel = 50;
    this.isRunning = false;
    this.locked = true;
  }

  // Abstract method to be implemented by other "inherited" classes
  public abstract void displayDisplacement();

  // Static method that is going to display a simple horizontal rule
  public static void displayRule(int num_of_char) {
    System.out.printf("\n\t");

    // Iterate through the number of characters
    for (int i = 0; i < num_of_char; i++) {
      System.out.printf("-");
    }

    System.out.printf("\n\n");
  }

  // Method that will be able to display the information about vehicle
  public void displayInfo() {
    displayRule(35);
    System.out.println("\t\tVehicle Information");
    displayRule(35);

    // Display the individual attributes
    System.out.println("\t\tBrand: " + brand);
    System.out.println("\t\tModel: " + model);
    System.out.println("\t\tPrice: " + price);
    System.out.println("\t\tColour: " + colour);
    System.out.println("\t\tHealth: " + health);
    System.out.println("\t\tEngine Number: " + engine.engineNum);
    System.out.println("\t\tChassis Number: " + chassis.chassisNum);
    System.out.println("\t\tEngine Capacity: " + engine.capacity);

    displayRule(35);
  }

  // Method that is going to be able to lock the vehicle
  public void lock() {
    // Check if the vehicle has already been locked
    if (locked) {
      // Output appropriate message
      System.out.println("\n\t<< Vehicle Has Already Been Locked!!! >>\n");

      // If the vehicle has not yet been locked ==> lock the doors
    } else {
      locked = true;

      // Output appropriate message
      System.out.println("\n\t<< Vehicle Has Now Been Locked!!! >>\n");
    }
  }

  // Method that is going to be able to unlock the vehicle
  public void unlock() {
    // Check if the vehicle has already been unlocked
    if (!locked) {
      // Output appropriate message
      System.out.println("\n\t<< Vehicle Has Already Been Unlocked!!! >>\n");

      // If the vehicle has not yet been unlocked ==> unlock the doors
    } else {
      locked = false;

      // Output appropriate message
      System.out.println("\n\t<< Vehicle Has Now Been Unlocked!!! >>\n");
    }
  }

  // Method that is going to be able to start the engines of the vehicle
  public void startEngines() {
    // Check if the vehicle's engine has already been running
    if (isRunning) {
      // Output appropriate message
      System.out.println("\n\t<< Vehicle's Engines Has Already Been Running!!! >>\n");

      // If the vehicle's engine has not yet been running ==> start the engines
    } else {
      isRunning = true;

      // Output appropriate message
      System.out.println("\n\t<< Vehicle's Engines Was Started And Now Running!!! >>\n");
    }
  }

  // Method that is going to be able to stop the engines of the vehicle
  public void stopEngines() {
    // Check if the vehicle's engine has already been "off"
    if (!isRunning) {
      // Output appropriate message
      System.out.println("\n\t<< Vehicle's Engines Has Already Been 'Off'!!! >>\n");

      // If the vehicle's engine has been running ==> stop the engines
    } else {
      isRunning = false;

      // Output appropriate message
      System.out.println("\n\t<< Vehicle's Engines Was Stopped!!! >>\n");
    }
  }

  // Method that is going to allow the vehicle to drive
  public void drive(Scanner scanner) {
    // First check if the vehicle has fuel to start with
    if (fuelLevel == 0) {
      // Output appropriate message
      System.out.println("\n\t<< Please Refuel Vehicle!!! >>\n");

      // Return the to "main" function
      return;
    }

    // If the vehicle's engines are not running
    if (!isRunning) {
      // Output appropriate message
      System.out.println("\n\t<< Engines Has Not Yet Been Started - Fuel Level Good!!! >>\n");

      // Ask the user if he / she wants to start the engines
      System.out.print("Do You Want To Start The Engines[y/n]: ");
      // NOTE: as `.next()` takes in a string... Use `.charAt(0)` to get character
      char user_input = scanner.next().charAt(0);

      // If the user does NOT want to start the engines
      if (Character.toLowerCase(user_input) != 'y') {
        // Return the to "main" function
        return;
      }

      // Change the current running status
      isRunning = true;
    }

    // Check if we have a minimum level of fuel to be able to drive the car
    if (fuelLevel < 10) {
      // Output appropriate message
      System.out.println("\n\t<< The Vehicle Need To Be Refueled!!! >>\n");
    }

    // If the vehicle has fuel and engines has already been started
    System.out.println("\n\t== The Vehicle Is Being Driven!!! ==\n");

    // Decrease the fuel level by '5' but don't let it go below '0'
    fuelLevel = Math.max(0, fuelLevel - 5);
  }

  // Method that is going to allow the vehicle to brake
  public void brake() {
    // Display a simple message that will show vehicle is braking
    System.out.println("\n\t== The Vehicle Is Slowing Down / Braking! ==\n");
  }

  // Getter Method for `fuelLevel` to get fuel level of vehicle
  public int getFuelLevel() {
    // Simply return the fuel level to whoever is asking for it
    return this.fuelLevel;
  }

  // Setter Method for `fuelLevel` to update fuel level of vehicle
  public void setFuelLevel(int userFuelLevel) {
    // Update the `fuelLevel` through the parameter / argument
    this.fuelLevel = userFuelLevel;
  }

  // Method that is going to allow us to refuel the vehicle
  public void refuel() {
    // Check if the tank if already full for vehicle
    if (fuelLevel == 100) {
      // Output appropriate message
      System.out.println("\n\t<< Vehicle's Fuel Tank Already Full!!! >>\n");

      // if the fuel level for vehicle is less than '100'
    } else if (fuelLevel < 100) {
      // Output appropriate message
      System.out.println("\n\t== Refuelling The Vehicle ==\n");

      // Increase the fuel level by '10' but don't let it go above 100
      fuelLevel = Math.min(fuelLevel + 10, 100);

    }

  }

  // Method that is going to handle general repairs
  public void repair() {
    // Check if the vehicle is already repaired
    if (health >= 70) {
      // Output appropriate message
      System.out.println("\n\t<< Vehicle's Already Repaired!!! >>\n");

      // Check if the vehicle need repairing
    } else {
      // Increase the health level by '10' but don't let it go above 100
      health = Math.min(health + 10, 100);

      // Output appropriate message
      System.out.println("\n\t== Repairing The Vehicle ==\n");
    }
  }

  // Method to that is going to handle specific repairs
  public void repair(String partName, int estimatedCost) {
    // Output appropriate message
    System.out.println("\n\t== Part Name: " + partName + " | Estimated Cost: " + estimatedCost + " ==\n");
  }

  // Method to assign driver to a 'Vehicle' object ==> Aggregation
  public void setDriver(Driver driver) {
    // Get the 'Driver' "object"
    this.vehicleDriver = driver;

    // Output appropriate message
    System.out
        .println(
            "\n\t== Driver Name Of '" + this.brand + " " + this.model + "': " + vehicleDriver.driverName + " ==\n");
  }
}
```

- `Car.java` File:

```java
package vehicles;

// import java packages
import java.util.Scanner;

// import our required packages
import components.*;
import interfaces.GPS;

// "Multiple inheritance" through the use of `interface`
// 'Car' class is a child of 'Vehicle' and has a 'GPS' interface
public class Car extends Vehicle implements GPS {
  // Declare variables so that we can hold attributes of object 'Car'
  int numOfDoors;

  // Declare class's instance variable here
  String trunkStatus;

  // Constructor to assign those variables to the object 'Car'
  public Car(
      String brand,
      String model,
      double price,
      String colour,
      int health,
      int engineNum,
      int chassisNum,
      int engineCapacity,
      int numOfDoors) {

    // Set the vehicle's attributes to the 'Vehicle' class
    super(brand, model, price, colour, health, engineNum, chassisNum, engineCapacity);

    // Initialise specific attributes for the 'Car' class
    this.numOfDoors = numOfDoors;

    // Class instance variable for 'Car' object
    this.trunkStatus = "closed";
  }

  // Specific method for 'Car' class to open the object's trunk
  public void openTrunk() {
    // Check if the car's trunk has already been opened
    if (trunkStatus.equals("opened")) {
      // Output appropriate message
      System.out.println("\n\t<< Car's Trunk Has Already Been Opened!!! >>\n");

      // If the car's trunked has not yet been opened ==> open the trunk
    } else {
      trunkStatus = "opened";

      // Output appropriate message
      System.out.println("\n\t<< Car's Trunk Has Been Opened!!! >>\n");
    }
  }

  // Specific method for 'Car' class to close the object's trunk
  public void closeTrunk() {
    // Check if the car's trunk has already been closed
    if (trunkStatus.equals("closed")) {
      // Output appropriate message
      System.out.println("\n\t<< Car's Trunk Has Already Been Closed!!! >>\n");

      // If the car's trunked has not yet been closed ==> close the trunk
    } else {
      trunkStatus = "closed";

      // Output appropriate message
      System.out.println("\n\t<< Car's Trunk Has Been Closed!!! >>\n");
    }
  }

  /*
   * INFO: Overridden `drive` method for the 'Car' subclass.
   * WARNING: The importance of `@Override`.
   * This is an optional "decorator" in Java, but it is better to include it!
   * In our case, we could do WITHOUT it simply because the method name and
   * parameters match.
   * However, if we made a typo like `Drive`, it wouldn't apply our
   * changes when calling `<carObjectInstanceName>.drive()`, and would
   * run the Vehicle's `drive` method instead!
   */
  @Override
  public void drive(Scanner scanner) {
    // Check if the trunk is open or now
    if (this.trunkStatus.equals("opened")) {
      // Output appropriate message
      System.out.println("\n\t<< Cannot Drive: Trunk Is Open!!! >>\n");

      // Return to the "main" function
      return;
    }

    // 'Car' objects drive in 'Sport' mode only
    System.out.println("\n\t== Car Drive Mode: Sport ==\n");

    // Get the current fuel level of the 'Car' object
    // INFO: Update to use 'getter' method from `Vehicle`
    int fuelBeforeDrive = this.getFuelLevel();

    // NOTE: Call the actual implementation from Vehicle's `drive` method
    // Therefore, in this way; we can still get the implementation of `drive`
    // WITHOUT needing to re-write everything again!
    // WARNING: We added the line below here because:
    // 1. We need to check if the trunk is open first
    // 2. We need to make sure that the we override the fuel level
    // ( given 'Sport' mode... We should remove more fuel )
    super.drive(scanner);

    // Update the fuel level in addition to the Vehicle's `drive` method fuel burn
    // This means that consume fuel in `super().drive()` and also Car's `drive`
    // method
    if (getFuelLevel() < fuelBeforeDrive) {
      // INFO: Update to use 'getter' and 'setter' method from `Vehicle`

      // Therefore, create the variable to be passed as argument
      int userFuelLevel = Math.max(0, getFuelLevel() - 2);

      // INFO: Use `setFuelLevel` method to set the new fuel level
      setFuelLevel(userFuelLevel);
    }
  }

  // INFO: Overriden `brake` method for the 'Car' subclass
  @Override
  public void brake() {
    // NOTE: Call the actual implementation from Vehicle's `brake` method
    super.brake();

    // 'Car' objects has ABS engaged ==> display it
    System.out.println("\t== ABS Engaged: Controlled Braking ==\n");
  }

  // Implementation of `displayDisplacement` method in `Car` class
  @Override
  public void displayDisplacement() {
    // Display the displacement of the 'Car' object
    System.out.println("\n\t== Engine Displacement: " + this.engine.capacity + "cc " + "==\n");
  }

  // Implementation of `calculateRoute` method from the 'GPS' interface
  // Use Method Overriding to implement interface's method(s)
  @Override
  public void calculateRoute() {
    // Display the displacement of the 'Car' object
    System.out.println("\n\t== GPS ( Interface ): Calculating Route ==\n");
  }
}
```

### Main Files

> [!WARNING]
> The following **codes** below were *written* by [Claude](https://claude.ai) Haiku through [Opencode](https://opencode.ai/)!

- `Main.java` File:

```java

// import java standard library packages
import java.util.List;
import java.util.ArrayList;
import java.util.Scanner;

// import our custom packages
import interfaces.GPS;
import people.Driver;
import vehicles.Vehicle;
import vehicles.Car;

// Our main class
public class Main {
  // Our main function
  public static void main(String[] args) {
    // Create Scanner for interactive drive() method
    Scanner scanner = new Scanner(System.in);

    // Object Creation & Inheritance
    Car nissanGTR = new Car("Nissan", "R32 GTR", 600000, "Black", 55, 1, 1, 2568, 2);
    Car bmwM3 = new Car("BMW", "E46 M3", 85000, "Silver", 70, 2, 2, 3246, 4);
    Car teslaModelS = new Car("Tesla", "Model S Plaid", 130000, "Red", 90, 3, 3, 0, 4);

    // Encapsulation - Display Vehicle Info
    nissanGTR.displayInfo();

    // Aggregation - Assign Driver
    Driver champion = new Driver("Lewis Hamilton");
    nissanGTR.setDriver(champion);

    // Method Overloading - repair() vs repair(String, int)
    nissanGTR.repair();
    nissanGTR.repair("Brake Pads", 250);

    // Abstraction - Abstract method implementation
    nissanGTR.displayDisplacement();

    // Interfaces - GPS interface usage
    GPS gps = nissanGTR;
    gps.calculateRoute();

    // State Management - Lock/Unlock & Engine Control
    nissanGTR.unlock();
    nissanGTR.lock();
    nissanGTR.lock();
    nissanGTR.startEngines();
    nissanGTR.stopEngines();
    nissanGTR.startEngines();

    // Car-specific - Trunk Operations
    nissanGTR.openTrunk();
    nissanGTR.openTrunk();
    nissanGTR.closeTrunk();

    // Polymorphism - List of Vehicles
    List<Vehicle> garage = new ArrayList<>();
    garage.add(nissanGTR);
    garage.add(bmwM3);
    garage.add(teslaModelS);

    // Polymorphic behavior - overridden methods
    for (Vehicle v : garage) {
      v.displayInfo();
      v.displayDisplacement();
      v.refuel();
      v.brake();
    }

    // Refueling & Fuel Management
    System.out.println("Fuel Before: " + nissanGTR.getFuelLevel());
    nissanGTR.refuel();
    System.out.println("Fuel After: " + nissanGTR.getFuelLevel());

    // Drive Operations - Interactive with Scanner
    nissanGTR.startEngines();
    nissanGTR.drive(scanner);
    nissanGTR.brake();
    nissanGTR.stopEngines();

    // Close the scanner to avoid memory leaks
    scanner.close();
  }
}
```

- `Makefile` File:

```bash
program: compile run clean

compile:
	@javac -d . Main.java vehicles/*.java components/*.java people/*.java interfaces/*.java
run:
	@java Main

clean:
	@rm -rf *.class vehicles/*.class components/*.class people/*.class interfaces/*.class
```

### The Output

Here is what the output of our `Main.java` file looks like:

> Again Claude '*Haiku*' wrote the code for this!

```console
	-----------------------------------

		Vehicle Information

	-----------------------------------

		Brand: Nissan
		Model: R32 GTR
		Price: 600000.0
		Colour: Black
		Health: 55
		Engine Number: 1
		Chassis Number: 1
		Engine Capacity: 2568

	-----------------------------------


	== Driver Name Of 'Nissan R32 GTR': Lewis Hamilton ==


	== Repairing The Vehicle ==


	== Part Name: Brake Pads | Estimated Cost: 250 ==


	== Engine Displacement: 2568cc ==


	== GPS ( Interface ): Calculating Route ==


	<< Vehicle Has Now Been Unlocked!!! >>


	<< Vehicle Has Now Been Locked!!! >>


	<< Vehicle Has Already Been Locked!!! >>


	<< Vehicle's Engines Was Started And Now Running!!! >>


	<< Vehicle's Engines Was Stopped!!! >>


	<< Vehicle's Engines Was Started And Now Running!!! >>


	<< Car's Trunk Has Been Opened!!! >>


	<< Car's Trunk Has Already Been Opened!!! >>


	<< Car's Trunk Has Been Closed!!! >>


	-----------------------------------

		Vehicle Information

	-----------------------------------

		Brand: Nissan
		Model: R32 GTR
		Price: 600000.0
		Colour: Black
		Health: 65
		Engine Number: 1
		Chassis Number: 1
		Engine Capacity: 2568

	-----------------------------------


	== Engine Displacement: 2568cc ==


	== Refuelling The Vehicle ==


	== The Vehicle Is Slowing Down / Braking! ==

	== ABS Engaged: Controlled Braking ==


	-----------------------------------

		Vehicle Information

	-----------------------------------

		Brand: BMW
		Model: E46 M3
		Price: 85000.0
		Colour: Silver
		Health: 70
		Engine Number: 2
		Chassis Number: 2
		Engine Capacity: 3246

	-----------------------------------


	== Engine Displacement: 3246cc ==


	== Refuelling The Vehicle ==


	== The Vehicle Is Slowing Down / Braking! ==

	== ABS Engaged: Controlled Braking ==


	-----------------------------------

		Vehicle Information

	-----------------------------------

		Brand: Tesla
		Model: Model S Plaid
		Price: 130000.0
		Colour: Red
		Health: 90
		Engine Number: 3
		Chassis Number: 3
		Engine Capacity: 0

	-----------------------------------


	== Engine Displacement: 0cc ==


	== Refuelling The Vehicle ==


	== The Vehicle Is Slowing Down / Braking! ==

	== ABS Engaged: Controlled Braking ==

Fuel Before: 60

	== Refuelling The Vehicle ==

Fuel After: 70

	<< Vehicle's Engines Has Already Been Running!!! >>


	== Car Drive Mode: Sport ==


	== The Vehicle Is Being Driven!!! ==


	== The Vehicle Is Slowing Down / Braking! ==

	== ABS Engaged: Controlled Braking ==


	<< Vehicle's Engines Was Stopped!!! >>
```

---

# Socials

- **Instagram**: https://www.instagram.com/s.sunhaloo
- **YouTube**: https://www.youtube.com/@s.sunhaloo
- **GitHub**: https://www.github.com/Sunhaloo

---

S.Sunhaloo
Thank You!