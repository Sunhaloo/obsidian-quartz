---
id: Java - Object Oriented Programming Basics
aliases: Object Oriented Prgramming Basics in Java
tags:
  - java
  - basics
  - oop
author: S.Sunhaloo
date: 2025-09-05
status: In-Progress
---

## List of Contents

- [[#Creation of Parent Class]]
	- [[#Implementing The Parent Class]]
	- [[#Create Instance of Parent Class]]
- [[#Creation of Methods Of Objects Of Parent Class]]
	- [[#Instance / Class Variables]]
	- [[#Creation Of Some Method For Parent Class]]
		- [[#Methods Related To Parent Class]]

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

  // Declare class / instance variable here
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
    // Declare scanner that will read user input from 'stdin'
    Scanner scanner = new Scanner(System.in);

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

    // close the scanner object
    scanner.close();
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
    // Declare scanner that will read user input from 'stdin'
    Scanner scanner = new Scanner(System.in);

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

    // close the scanner object
    scanner.close();
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
    // Declare scanner that will read user input from 'stdin'
    Scanner scanner = new Scanner(System.in);

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

    // close the scanner object
    scanner.close();
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



---

# Socials

- **Instagram**: https://www.instagram.com/s.sunhaloo
- **YouTube**: https://www.youtube.com/@s.sunhaloo
- **GitHub**: https://www.github.com/Sunhaloo

---

S.Sunhaloo
Thank You!