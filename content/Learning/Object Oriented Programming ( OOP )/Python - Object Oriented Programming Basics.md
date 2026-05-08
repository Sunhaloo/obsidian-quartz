---
id: Python - Object Oriented Programming Basics
aliases: Object Oriented Prgramming Basics in Python
tags:
  - python
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
- [[#Multiple Inheritance]]
- [[#Composition]]
- [[#Aggregation]]

---

> [!INFO]
> Please refer to the first note / file with the name '[[Introduction to Object Oriented Programming]]'.
>
> These are my notes about *theoretical* aspect of Object Oriented Programming. There I talked about the `Vehicle` class.
>
> I am going to try to *implement* that same **parent** `Vehicle` class as example here also.
>
> Let's get **practical**!

# Creation of Parent Class

The thing about Object Oriented Programming, its that we need to first understand what we going to be coding.

For example; yes we are going to be coding something related to *vehicles*, *cars* and others. But **what are data are we going to store about them**? **What can each of the entities do**?

These are all the questions that we need to ask ourselves as 'OOP' programmers.

> Else what are we actually implementing?

> [!TIP] Parent Class - `Vehicle`
> - Attributes:
> 	- Brand
> 	- Model
> 	- Price
> 	- Colour
> 	- Engine Number
> 	- Chassis Number
> 	- Engine Capacity
>
> - Functions / "*Abilities*" Related to `Vehicle` class
> 	- `lock`
> 	- `unlock`
> 	- `start_engine`
> 	- `drive`
> 	- `brake`
> 	- `stop_engine`
> 	- `refuel`
> 	- `repair`
> 		- `general` / `service`
> 		- `part_name`
> 		- `cost` / `estimated_cost`

Now that we know what we are actually doing... We can start the *coding* process!

> [!NOTE]
> For the moment instead of breaking it into multiple files. I am going to stick to a **single file** setup for the moment.

## Implementing The Parent Class

Below you are going to find the code on how to create the **parent** class of `Vehicle`.

```python
class Vehicle:
    # constructor to define attributes of vehicle instances
    def __init__(
        self,
        brand: str,
        model: str,
        price: float,
        colour: str,
        health: int,
        engine_num: int,
        chassis_num: int,
        engine_capacity: int,
    ) -> None:
        # intialise the attributes for a vehicle object
        self.brand = brand
        self.model = model
        self.price = price
        self.colour = colour
        self.health = health
        self.engine_num = engine_num
        self.chassis_num = chassis_num
        self.engine_capacity = engine_capacity
```

## Create Instance of Parent Class

Let's go ahead and actually make use of our `Vehicle` **parent** class.

> [!NOTE]
> Therefore, this is what I am going to write in my `main` function!
>
> > [!TIP]
> > We can also use '*Type Annotations*' with **objects** also!

```python
# our main function
def main():
    # create first object of the parent class of `Vehicle`
    vehicle_1: Vehicle = Vehicle(
        "Mazda", "RX-7 FD", 500000, "Canary Yellow", 65, 1, 1, 1300
    )


# source the main function
if __name__ == "__main__":
    main()
```

### Displaying Information About Object In `main`

- Update Our `main` Function

```python
# our main function
def main():
    # create first object of the parent class of `Vehicle`
    vehicle_1: Vehicle = Vehicle(
        "Mazda", "RX-7 FD", 500000, "Canary Yellow", 65, 1, 1, 1300
    )

    # display each attributes for the vehicle object created
    print(f"Vehicle 1's Brand: {vehicle_1.brand}")
    print(f"Vehicle 1's Model: {vehicle_1.model}")
    print(f"Vehicle 1's Price: {vehicle_1.price}")
    print(f"Vehicle 1's Colour: {vehicle_1.colour}")
	print(f"Vehicle 1's Health: {vehicle_1.health}")
    print(f"Vehicle 1's Engine Number: {vehicle_1.engine_num}")
    print(f"Vehicle 1's Chassis Number: {vehicle_1.chassis_num}")
    print(f"Vehicle 1's Engine Capacity: {vehicle_1.engine_capacity}")


# source the main function
if __name__ == "__main__":
    main()
```

- Therefore, running our `main.py` file we should be able to display all the **attributes** of `vehicle_1`

```console
Vehicle 1's Brand: Mazda
Vehicle 1's Model: RX-7 FD
Vehicle 1's Price: 500000
Vehicle 1's Health: 65
Vehicle 1's Colour: Canary Yellow
Vehicle 1's Engine Number: 1
Vehicle 1's Chassis Number: 1
Vehicle 1's Engine Capacity: 1300
```

> [!SUCCESS]
> As you can see, our object `vehicle_1` has been successfully created with its proper attributes!

# Creation of Methods Of Objects Of Parent Class

## Instance / Class Variables

Our current object `vehicle_1` of the parent class `Vehicle` currently does not really do anything!

Lets go ahead and add some **more** *attributes* to it and allow our object created to *do* somethings.

- Modify our *constructor* / attributes to add the following **class attributes**

```python
class Vehicle:
    # constructor to define attributes of vehicle instances
    def __init__(
        self,
        brand: str,
        model: str,
        price: float,
        colour: str,
        health: int,
        engine_num: int,
        chassis_num: int,
        engine_capacity: int,
    ) -> None:
        # intialise the attributes for a vehicle object
        self.brand = brand
        self.model = model
        self.price = price
        self.colour = colour
        self.health = health
        self.engine_num = engine_num
        self.chassis_num = chassis_num
        self.engine_capacity = engine_capacity

        # class variables for `Vehicle` object
        self.fuel_level = 50
        self.is_running = False
        self.locked = True
```

As you can see we have added `fuel_level`, `is_running` and the `locked` **class variables** that are going to be *initialised* for **any** `Vehicle` object created.

- Check `Vehicle` object **instance variable** by updating `main` to this:

```python
# our main function
def main():
    # create first object of the parent class of `Vehicle`
    vehicle_1: Vehicle = Vehicle(
        "Mazda", "RX-7 FD", 500000, "Canary Yellow", 65, 1, 1, 1300
    )

    # display each attributes for the vehicle object created
    print(f"Vehicle 1's Brand: {vehicle_1.brand}")
    print(f"Vehicle 1's Model: {vehicle_1.model}")
    print(f"Vehicle 1's Price: {vehicle_1.price}")
    print(f"Vehicle 1's Colour: {vehicle_1.colour}")
    print(f"Vehicle 1's Health: {vehicle_1.health}")
    print(f"Vehicle 1's Engine Number: {vehicle_1.engine_num}")
    print(f"Vehicle 1's Chassis Number: {vehicle_1.chassis_num}")
    print(f"Vehicle 1's Engine Capacity: {vehicle_1.engine_capacity}")

    # display the class variables of `Vehicle` object
    print(f"\nVehicle 1's Fuel Level: {vehicle_1.fuel_level} <--")
    print(f"Vehicle 1's Engine Running?: {vehicle_1.is_running} <--")
    print(f"Vehicle 1's Doors Locked?: {vehicle_1.locked} <--")


# source the main function
if __name__ == "__main__":
    main()
```

- Therefore, we should see that we do *see* the **class variable** of `vehicle1`.

```console
Vehicle 1's Brand: Mazda
Vehicle 1's Model: RX-7 FD
Vehicle 1's Price: 500000
Vehicle 1's Colour: Canary Yellow
Vehicle 1's Health: 65
Vehicle 1's Engine Number: 1
Vehicle 1's Chassis Number: 1
Vehicle 1's Engine Capacity: 1300

Vehicle 1's Fuel Level: 50 <--
Vehicle 1's Engine Running?: False <--
Vehicle 1's Doors Locked?: True <--
```

> [!SUCCESS]
> We have now been able to **create** *instance variables* and been able to **display** these variables!

## Creation Of Some Method For Parent Class

Therefore, let's go ahead and create some **methods** that's going to work with our `Vehicle` objects.

### Static Methods

As the name suggests.... **Static** methods are well "*static*" whereby they are **not** really related to *specifically* to a class.

This means that we can use them even if we have **not** yet created any objects!

> [!NOTE]
> They are so fucking useful!
>
> Back when I first started learning and working with 'OOP'. Whenever I needed to use a static method; I would **create** a "*fake*" object whereby I would call these the methods on.
>
> But I think you can realise how **inefficient** that was as each time it would have to reference that object in memory ( *like RAM* ) and then call / use that method function.
>
> Therefore, do make sure that you know how to use them well!

#### Static Method To Display Horizontal Rule

```python
    # static method that is going to display a simple horizontal rule
    @staticmethod
    def display_rule(num_of_chars) -> None:
        print("\n\t", "-" * num_of_chars, "\n")
```

> As you can see we use the little `@staticmethod` property!

- Usage:

```python
# our main function
def main():
    # create first object of the parent class of `Vehicle`
    vehicle_1: Vehicle = Vehicle(
        "Mazda", "RX-7 FD", 500000, "Canary Yellow", 65, 1, 1, 1300
    )

    # use the static method `displayRule` WITHOUT creating any objects
    Vehicle.display_rule(50)


# source the main function
if __name__ == "__main__":
    main()
```

- Therefore this is what we should get as output:

```console
         --------------------------------------------------
```

> [!WARNING]
> <h5 align="center" style="color: white;"> When Should You Use A <code> staticmethod</code> ?</h5>
>
> To know if you need to use a `staticmethod` or a method **related** to the *Object* itself. Then you are going to have to ask yourself this question:
>
> "*Does this method need to operate on a specific object and its unique attributes, or does it perform a general task that is the same for all objects of this class*?"
>
> In the case of `display_rule`. It could be use by pretty much **any** *objects* of **any** *class*. Heck, its just printing a simple horizontal rule! We could even use it by *itself*!
>
> Like we did above!

### Methods Related To Parent Class

#### Display All Information About Vehicle

```python
    # method that will be able to display the information about vehicle
    def display_info(self) -> None:
        self.display_rule(35)
        print("\t\tVehicle Information")
        self.display_rule(35)

        print(f"\t\tBrand: {self.brand}")
        print(f"\t\tModel: {self.model}")
        print(f"\t\tPrice: {self.price}")
        print(f"\t\tColour: {self.colour}")
        print(f"\t\tHealth: {self.health}")
        print(f"\t\tEngine Number: {self.engine_num}")
        print(f"\t\tChassis Number: {self.chassis_num}")
        print(f"\t\tEngine Capacity: {self.engine_capacity}")

        self.display_rule(35)
```

- Usage:

```python
# our main function
def main():
    # create first object of the parent class of `Vehicle`
    vehicle_1: Vehicle = Vehicle(
        "Mazda", "RX-7 FD", 500000, "Canary Yellow", 65, 1, 1, 1300
    )

    # display all the information about `vehicle_1`
    vehicle_1.display_info()


# source the main function
if __name__ == "__main__":
    main()
```

- This is the output after running the above function:

```console
        -----------------------------------

                Vehicle Information

        -----------------------------------

                Brand: Mazda
                Model: RX-7 FD
                Price: 500000
                Colour: Canary Yellow
                Health: 65
                Engine Number: 1
                Chassis Number: 1
                Engine Capacity: 1300

        -----------------------------------
```

#### Lock and Unlock Vehicle

- Method to **lock** the *vehicle*:

```python
    # method that is going to be able to lock the vehicle
    def lock(self) -> None:
        # check if the vehicle has already been locked
        if self.locked:
            # output appropriate message
            print("\n\t<< Vehicle Has Already Been Locked!!!  > \n")

        # if the vehicle has not been locked yet ==> lock the doors
        else:
            self.locked = True

            # output appropriate message
            print("\n\t<< Vehicle Has Now Been Locked!!!  > \n")
```

- Method to _**un**lock_ the *vehicle*:

```python
    # method that is going to be able to unlock the vehicle
    def unlock(self) -> None:
        # check if the vehicle has already been locked
        if not self.locked:
            # output appropriate message
            print("\n\t<< Vehicle Has Already Been Unlocked!!!  > \n")

        # if the vehicle has not yet been unlocked ==> unlock the doors
        else:
            self.locked = False

            # output appropriate message
            print("\n\t<< Vehicle Has Now Been Unlocked!!!  > \n")
```

- Show usage of **both** `unlock` and `lock`:

```python
# our main function
def main():
    # create first object of the parent class of `Vehicle`
    vehicle_1: Vehicle = Vehicle(
        "Mazda", "RX-7 FD", 500000, "Canary Yellow", 65, 1, 1, 1300
    )

    # get the current lock status of the `vehicle1`
    print(f"Current Lock Status Of Vehicle: {vehicle_1.locked}")

    # call the method to unlock the vehicle
    vehicle_1.unlock()

    # get the current lock status of the `vehicle1` after unlocking
    print(f"Current Lock Status Of Vehicle: {vehicle_1.locked}")

    # call the method to lock the vehicle
    vehicle_1.lock()

    # get the current lock status of the `vehicle1` after locking
    print(f"Current Lock Status Of Vehicle: {vehicle_1.locked}")


# source the main function
if __name__ == "__main__":
    main()
```

- Therefore, this is the output that we are going to get:

```console
Current Lock Status Of Vehicle: True

        << Vehicle Has Now Been Unlocked!!!  > 

Current Lock Status Of Vehicle: False

        << Vehicle Has Now Been Locked!!!  > 

Current Lock Status Of Vehicle: True
```

#### Start and Stop Engine

- Method to **start** the *engine*:

```python
    # method that is going to be able to start the engines of the vehicle
    def start_engine(self) -> None:
        # check if the vehicle's engine has already been running
        if self.is_running:
            # output appropriate message
            print("\n\t<< Vehicle's Engines Has Already Been Running!!!  > \n")

        # if the vehicle's engine has not yet been running ==> start the engines
        else:
            self.is_running = True

            # output appropriate message
            print("\n\t<< Vehicle's Engines Was Started And Now Running!!!  > \n")
```

- Method to **stop** the *engine*:

```python
    # method that is going to be able to stop the engines of the vehicle
    def stop_engine(self) -> None:
        # check if the vehicle's engine has already been "off"
        if not self.is_running:
            # output appropriate message
            print("\n\t<< Vehicle's Engines Has Already Been 'Off'!!!  > \n")

        # if the vehicle's engine has been running ==> stop the engines
        else:
            self.is_running = False

            # output appropriate message
            print("\n\t<< Vehicle's Engines Was Stopped!!!  > \n")
```

- Show usage of **both** `startEngines` and `stopEngines`:

```python
# our main function
def main():
    # create first object of the parent class of `Vehicle`
    vehicle_1: Vehicle = Vehicle(
        "Mazda", "RX-7 FD", 500000, "Canary Yellow", "New", 1, 1, 1300
    )

    # get the current engine running status of the `vehicle1`
    print(f"Current Engine Running Status Of Vehicle: {vehicle_1.is_running}")

    # call the method to start the engines of the vehicle
    vehicle_1.start_engine()

    # get the current engine running status after starting engines vehicle
    print(f"Current Engine Running Status Of Vehicle: {vehicle_1.is_running}")

    # call the method to stop the engines of the vehicle
    vehicle_1.stop_engine()

    # get the current engine running status of the `vehicle1` after shutdown
    print(f"Current Engine Running Status Of Vehicle: {vehicle_1.is_running}")


# source the main function
if __name__ == "__main__":
    main()
```

- Therefore this is the output that we get:

```console
Current Engine Running Status Of Vehicle: False

        << Vehicle's Engines Was Started And Now Running!!!  > 

Current Engine Running Status Of Vehicle: True

        << Vehicle's Engines Was Stopped!!!  > 

Current Engine Running Status Of Vehicle: False
```

#### Drive and Brake Vehicle

- Method to **drive** the *vehicle*:

```python
    # method that is going allow the vehicle to drive
    def drive(self) -> None:
        # first check if the vehicle has fuel to start with
        if self.fuel_level == 0:
            # output appropriate message
            print("\n\t<< Please Refuel Vehicle  > \n")

            # return to the "main" function
            return

        # if the vehicle's engines are not running
        if not self.is_running:
            # output appropriate message
            print("\n\t<< Engines Has Not Yet Been Started - Fuel Level Good!!!  > \n")

            # ask the user if he / she wants to start the vehicle's engines
            start_vehicle = input("Do You Want To Start The Engines[y/n]: ")

            # if the user wants does NOT to start the engines
            if start_vehicle.lower() != "y":
                return

            # change the current running status
            self.is_running = True

        # check if we have a minimum level of fuel to be able to drive the car
        if self.fuel_level < 10:
            # output appropriate message
            print("\n\t<< The Vehicle Need To Be Refueled!!!  > \n")

        # if the vehicle has fuel and engines has already been started
        print("\n\t== The Vehicle Is Being Driven!!! ==\n")

        # decrease the fuel level by '5' but don't let it go below '0'
        self.fuel_level = max(0, self.fuel_level - 5)
```

- Method to "_**brake**_" the *vehicle*:

```python
    # method that is going allow the vehicle to brake
    def brake(self) -> None:
        # display a simple message that will show vehicle is braking
        print("\n\t== The Vehicle Is Slowing Down / Braking! ==\n")
```

- Show usage of **both** `drive` and `brake`:

```python
# our main function
def main():
    # create first object of the parent class of `Vehicle`
    vehicle_1: Vehicle = Vehicle(
        "Mazda", "RX-7 FD", 500000, "Canary Yellow", 65, 1, 1, 1300
    )

    # display the current fuel level of `vehicle_1`
    print(f"\nCurrent Fuel Level ( Before Driving ): {vehicle_1.fuel_level}")

    # call the method to start the engines the vehicle
    vehicle_1.start_engine()

    # call the method to drive the vehicle
    vehicle_1.drive()

    # call the method to allow the vehicle to slow down
    vehicle_1.brake()

    # call the method to stop the engines the vehicle
    vehicle_1.stop_engine()

    # display the current fuel level after driving
    print(f"\nCurrent Fuel Level ( After Driving ): {vehicle_1.fuel_level}")


# source the main function
if __name__ == "__main__":
    main()
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

```python
    # method that is going to allow us to refuel the vehicle
    def refuel(self) -> None:
        # check if tank is already full for vehicle
        if self.fuel_level == 100:
            # output appropriate message
            print("\n\t<< Vehicle's Fuel Tank Already Full!!!  > \n")

        # if the fuel level for vehicle is less than '100'
        elif self.fuel_level < 100:
            # output appropriate message
            print("\n\t== Refuelling The Vehicle ==\n")

            # increase the fuel level by '10' but don't let it go above 100
            self.fuel_level = min(self.fuel_level + 10, 100)
```

- Usage:

```python
# our main function
def main():
    # create first object of the parent class of `Vehicle`
    vehicle_1: Vehicle = Vehicle(
        "Mazda", "RX-7 FD", 500000, "Canary Yellow", 65, 1, 1, 1300
    )

    # change the fuel level of `vehicle_1`
    vehicle_1.fuel_level = 20

    # display the current fuel level of `vehicle_1`
    print(f"\nCurrent Fuel Level ( Before Driving ): {vehicle_1.fuel_level}")

    # iterate through the loop 3 times
    for i in range(3):
        # call the method to refuel the vehicle
        vehicle_1.refuel()

    # display the current fuel level after driving
    print(f"\nCurrent Fuel Level ( After Driving ): {vehicle_1.fuel_level}")


# source the main function
if __name__ == "__main__":
    main()
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

> Before we start, I have to say something...

> [!WARNING]
> <h6 align="center" style="color: white;"> There Are <strong> No</strong> Method Overloading in Python!!!</h6>
>
> Yes, the concept of '*Method Overloading*' is **not** present in Python like the *traditional sense*!
>
> In Python, you <span style="color: orange;"> cannot</span> make *two* functions / methods with the **same** identifier name.
>
> Therefore, we have to play with the **parameters** themselves and `None` keyword.
>
 > [!INFO] Rabbit Hole
 > This has put me into a few rabbit holes and here are some resources:
 > 
 > - https://stackoverflow.com/questions/10202938/how-do-i-use-method-overloading-in-python
 > - https://docs.python.org/3/tutorial/controlflow.html#default-argument-values
 > - https://stackoverflow.com/questions/1132941/least-astonishment-and-the-mutable-default-argument
 > - https://web.archive.org/web/20200221224620id_/http://effbot.org/zone/default-values.htm

##### Method Overloading ( Repair Vehicle )

```python
    # method that is going to allow us to repair the vehicle
    def repair(
        self, part_name=None, estimated_cost=None, repair_type: str = "general"
    ) -> None:
        # check if its a general servicing
        if repair_type == "general":
            # check for the vehicle's health
            if self.health > = 70:
                # output appropriate message
                print("\n\t<< Vehicle's Already Repaired!!!  > \n")

            else:
                # increase the health level by '10' but don't let it go above 100
                self.health = min(self.health + 10, 100)

                # output appropriate message
                print("\n\t== Repairing The Vehicle ==\n")

        # if the repair is a specific service
        elif repair_type == "specific":
            print(
                f"\n\t== Part Damaged: {part_name} | Estimated Cost: {estimated_cost} ==\n"
            )

        # if the repair type does not exists
        else:
            # output appropriate message
            print("\n\t<< Repair Type Does NOT Exists!!!  > \n")
```

- **General** Service Usage:

```python
# our main function
def main():
    # create first object of the parent class of `Vehicle`
    vehicle_1: Vehicle = Vehicle(
        "Mazda", "RX-7 FD", 500000, "Canary Yellow", 65, 1, 1, 1300
    )

    # change the vehicle's health level
    vehicle_1.health = 50

    # display the current health level of `vehicle_1`
    print(f"\nCurrent Health Level ( Before Repairing ): {vehicle_1.health}")

    # iterate through the loop 3 times
    for i in range(3):
        # call the method to repair the vehicle ( general )
        vehicle_1.repair()

    # display the current health level after repairing
    print(f"\nCurrent Health Level ( After Repairing ): {vehicle_1.health}")
```

- Output of **General** Service:

```console
Current Health Level ( Before Repairing ): 50

        == Repairing The Vehicle ==


        == Repairing The Vehicle ==


        << Vehicle's Already Repaired!!!  > 


Current Health Level ( After Repairing ): 70
```

- **Specific** Service Usage:

```python
# our main function
def main():
    # create first object of the parent class of `Vehicle`
    vehicle_1: Vehicle = Vehicle(
        "Mazda", "RX-7 FD", 500000, "Canary Yellow", 65, 1, 1, 1300
    )

    # change the vehicle's health level
    vehicle_1.health = 50

    # display the current health level of `vehicle_1`
    print(f"\nCurrent Health Level ( Before Repairing ): {vehicle_1.health}")

    # iterate through the loop 3 times
    for i in range(3):
        # call the method to repair the vehicle ( general )
        vehicle_1.repair("Gear Lever", 700, "specific")

    # display the current health level after repairing
    print(f"\nCurrent Health Level ( After Repairing ): {vehicle_1.health}")
```

- Output of **General** Service:

```console
Current Health Level ( Before Repairing ): 50

        == Part Damaged: Gear Lever | Estimated Cost: 700 ==


        == Part Damaged: Gear Lever | Estimated Cost: 700 ==


        == Part Damaged: Gear Lever | Estimated Cost: 700 ==


Current Health Level ( After Repairing ): 50
```

---

# Creation of Subclass

## Implementing The Child Class

```python
# our 'Car' subclass from the 'Vehicle' parent class
class Car(Vehicle):
    # constructor to define the attributes of car instances
    def __init__(
        self,
        brand: str,
        model: str,
        price: float,
        colour: str,
        health: int,
        engine_num: int,
        chassis_num: int,
        engine_capacity: int,
        num_of_doors: int,
    ) -> None:
        # set the vehicle's attributes to the 'Vehicle' class
        super().__init__(
            brand,
            model,
            price,
            colour,
            health,
            engine_num,
            chassis_num,
            engine_capacity,
        )

        # initialise specific attributes for the 'Car' class
        self.num_of_doors = num_of_doors

        # class instance variable for 'Car' object
        self.trunk_status = "closed"

    # specific method for the 'Car' class to open the object's trunk
    def open_trunk(self) -> None:
        # check if the car's trunk has already been opened
        if self.trunk_status == "opened":
            # output appropriate message
            print("\n\t<< Car's Trunk Has Already Been Opened!!! >>\n")

        # if the car's trunked has not yet been opened ==> open the trunk
        else:
            self.trunk_status = "opened"

            # output appropriate message
            print("\n\t<< Car's Trunk Has Been Opened!!! >>\n")

    # specific method for the 'Car' class to close the object's trunk
    def close_trunk(self) -> None:
        # check if the car's trunk has already been closed
        if self.trunk_status == "closed":
            # output appropriate message
            print("\n\t<< Car's Trunk Has Already Been Closed!!! >>\n")

        # if the car's trunked has not yet been closed ==> close the trunk
        else:
            self.trunk_status = "closed"

            # output appropriate message
            print("\n\t<< Car's Trunk Has Been Closed!!! >>\n")
```

Given that we already know how to create **methods** for a `class`.

I simply add the **methods** for the `Car` *subclass* in the code block above instead of making a separate heading in this note for it.

## Create Instance Of Child Subclass

Let us now go ahead and create our first **object** of the **child** class of `Car`.

```python
# our main function
def main():
    # create first object of the child class of `Car`
    car_1: Car = Car("Nissan", "R32 GTR", 600000, "Black", 55, 1, 1, 2568, 2)


# source the main function
if __name__ == "__main__":
    main()
```

### Calling Some Methods On Child Object

```python
# our main function
def main():
    # create first object of the parent class of `Vehicle`
    vehicle_1: Vehicle = Vehicle(
        "Mazda", "RX-7 FD", 500000, "Canary Yellow", 65, 1, 1, 1300
    )

    # create first object of the child class of `Car`
    car_1: Car = Car("Nissan", "R32 GTR", 600000, "Black", 55, 1, 1, 2568, 2)

    # call parent methods of `Vehicle` on the `Car` child class
    car_1.display_info()

    Vehicle.display_rule(55)

    car_1.unlock()
    car_1.start_engine()
    car_1.drive()

    Vehicle.display_rule(55)

    car_1.brake()
    car_1.stop_engine()

    for _ in range(3):
        car_1.refuel()

    Vehicle.display_rule(55)

    car_1.start_engine()
    car_1.drive()

    Vehicle.display_rule(55)

    car_1.brake()
    car_1.stop_engine()

    Vehicle.display_rule(55)

    car_1.unlock()

    # call `Car` child class specific methods
    car_1.open_trunk()

    for _ in range(2):
        car_1.close_trunk()

    car_1.lock()

    Vehicle.display_rule(55)


# source the main function
if __name__ == "__main__":
    main()
```

- This is the output after running the above *updated* `main` function:

```console
	 ----------------------------------- 

		Vehicle Information

	 ----------------------------------- 

		Brand: Nissan
		Model: R32 GTR
		Price: 600000
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

```python
    # INFO: overriden `drive` method for the 'Car' subclass
    def drive(self) -> None:
        # check if the trunk is open or now
        if self.trunk_status == "opened":
            # output appropriate message
            print("\n\t<< Trunk Is Open! ==> Cannot Drive Car!!! >>\n")

            # return to the "main" function
            return

        # 'Car' objects drive in 'Sport' mode only
        print("\n\t== Car Drive Mode: Sport ==\n")

        # get the current fuel level of the 'Car' object
        fuel_before_drive = self.fuel_level

        # NOTE: call the actual implementation from Vehicle's `drive` method
        # therefore, in this way; we can still get the implementation of `drive`
        # WITHOUT needing to re-write everything again!
        # WARNING: we added the line below here because:
        # 1. we need to check if the trunk is open first
        # 2. we need to make sure that the we override the fuel level
        # ( given 'Sport' mode... We should remove more fuel )
        super().drive()

        # update the fuel level in addition to the Vehicle's `drive` method fuel burn
        # this means that consume fuel in `super().drive()` and also Car's `drive` method
        if self.fuel_level < fuel_before_drive:
            self.fuel_level = max(0, self.fuel_level - 2)
```

- Method to "_**brake**_" the *car*:

```python
    # INFO: overriden `brake` method for the 'Car' subclass
    def brake(self) -> None:
        # NOTE: call the actual implementation from Vehicle's `brake` method
        super().brake()

        # 'Car' objects has ABS engaged ==> display it
        print("\t== ABS Engaged: Controlled Braking ==\n")
```

- Show usage of **both** `drive` and `brake`:

```python
# our main function
def main():
    # create first object of the child class of `Car`
    car_1: Car = Car("Nissan", "R32 GTR", 600000, "Black", 55, 1, 1, 2568, 2)

    # display the current fuel level of `vehicle_1`
    print(f"\nCurrent Fuel Level ( Before Driving ): {car_1.fuel_level}")

    # call the method to start the engines the vehicle
    car_1.start_engine()

    # call the method to drive the vehicle
    car_1.drive()

    # call the method to allow the vehicle to slow down
    car_1.brake()

    # call the method to stop the engines the vehicle
    car_1.stop_engine()

    # display the current fuel level after driving
    print(f"\nCurrent Fuel Level ( After Driving ): {car_1.fuel_level}")


# source the main function
if __name__ == "__main__":
    main()
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
> Therefore, they are **not** a *requirement* for the "*showing*" 'Inheritance' in both [[Java - Object Oriented Programming Basics | Java]] and Python.

# Polymorphism?

From what we already know in our little adventure in '[[Introduction to Object Oriented Programming#Polymorphism | Introduction to Object Oriented Programming]]'.

Polymorphism is basically '**Method Overloading**' and '**Method Overriding**'.

Hence, can we say that we already know about '*Polymorphism*' itself?

> The answer is **no**!

Method Overloading and Method overriding is just the "*tool*" that **allows** for *Polymorphism* but it does **not**, *by itself*, show the overall concept well.

> Let's take a little example and then you should be able to understand what I am trying to say.

```python
# our main function
def main():
    # create a list to hold objects of different classes
    garage: list = [
        # create first object of the parent class of `Vehicle`
        Vehicle("Mazda", "RX-7 FD", 500000, "Canary Yellow", 65, 1, 1, 1300),
        # create first object of the child class of `Car`
        Car("Nissan", "R32 GTR", 600000, "Black", 55, 1, 1, 2568, 2),
    ]

    # INFO: polymorphism in action
    # we are now going to treat all the objects, inside the list, as a generic vehicle
    for vehicle in garage:
        # call the `brake` method on these "vehicles"
        vehicle.brake()

        # display a horizontal rule using static method
        Vehicle.display_rule(50)


# source the main function
if __name__ == "__main__":
    main()
```

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

> [!INFO] Resource(s)
> 
> - [[Introduction to Object Oriented Programming#Encapsulation | Introduction to Object Oriented Programming]]
> - Python Official Documentation ( Decorators ): https://peps.python.org/pep-0318/
> - Medium Article: https://medium.com/@christopher.kelly1997/python-decorators-and-dynamic-properties-55402a2e1aff

As the word implies; we are going to "*encapsulate*" our **data** and hence, **hide** our data from other `class`es so that only a **selected** few can modify them.

> This is what we mean by "*data hiding*"!

Therefore, to avoid data being manipulated **without** our *consent*. We therefore, provide `public` methods like '**getters**' and '**setters**' that can work on these data *in a specific manner*.

Let's modify the above `main` function so that it looks like this:

```python
# our main function
def main():
    # create a list to hold objects of different classes
    garage: list = [
        # create first object of the parent class of `Vehicle`
        Vehicle("Mazda", "RX-7 FD", 500000, "Canary Yellow", 65, 1, 1, 1300),
        # create first object of the child class of `Car`
        Car("Nissan", "R32 GTR", 600000, "Black", 55, 1, 1, 2568, 2),
    ]

    # showing "encapsulation" ( before implementation )

    # display the fuel level of the `Vehicle` object before changing
    print(f"( Before Encapsulation ) Fuel Level Before Change: {garage[0].fuel_level}")

    # change the fuel level ( directly ) for our `Vehicle` object
    garage[0].fuel_level = 100

    # display the fuel level of the `Vehicle` object after changing
    print(f"( Before Encapsulation ) Fuel Level After Change: {garage[0].fuel_level}")


# source the main function
if __name__ == "__main__":
    main()
```

As you can see we can simply change the `fuelLevel` [[#Instance / Class Variables | class instance variable]] was **able** to be *modified* **without** any issues inside the `Main` class!

> Well, we are now going to try to stop that from happening!

> [!WARNING] Its different in Python
> 
> As you can see, we don't even have `private` or `protected` *variables* or *methods* here.
> 
> We simply use a "*gentleman's agreement*" to *get* things like **encapsulation** and stuff.
> 
> Therefore, if you want real Object Oriented Programming Encapsulation and stuff; just go take a look at the 'Encapsulation' heading over at '[[Java - Object Oriented Programming Basics#Encapsulation | Java - Object Oriented Programming Basics]]'

## Hiding The Fuel Level

We are now going to modify the `fuel_level` class **instance** variable so that we need to use '*getters*' and '*setters*' to be able to **get** and **update** the value.

- Modify the variable definition of `fuel_level` to be `private`:

> Again and again and again, its **not** really making the variable "*private*"...

```python
        # class variables for `Vehicle` object
        self.is_running = False
        self.locked = True

        # update the fuel level to be a "private" class / instance variable
        self.__fuel_level = 50

    # static method that is going to display a simple horizontal rule
```

### Getter Method - Fuel Level

We are now going to make a method that is will be `public` and therefore be able to be used by other `class`es so that we are able to "**extract**" the values for `fuel_level`.

```python
    # getter method for `fuel_level` to get fuel level of vehicle
    # INFO: see how we are using the decorator here
    @property
    def fuel_level(self) -> int:
        # simply return the fuel level to whoever is asking for it
        return self.__fuel_level
```

### Setter Method - Fuel Level

Similarly, we need a new way to *set* the value for `fuelLevel` from **other** `class`es like `Car`.

```python
    # setter method for `fuel_level` to update fuel level of vehicle
    # INFO: see how we are using the decorator here ==> same method name as 'getter'
    @fuel_level.setter
    def fuel_level(self, user_fuel_level: int) -> None:
        # update the `fuel_level` through the parameter / argument
        self.__fuel_level = max(0, min(user_fuel_level, 100))
```

---

> [!WARNING] The `@property` and `@<method_name>.setter`!
> 
> You are going to see that compared to our [[Java - Object Oriented Programming Basics#Getter and Setter Usage | Java]] note / program, we used the `getFuelLevel` and `setFuelLevel` method **name**.
> 
> But this is **not** possible in Python ( *in the way that we are trying to use it* )!
> 
> Given that we want to use the Python **decorators** to show a '*getter*' and '*setter*' method.
> 
> > We **need** to use the **same** *method name* for **both** the 'getter' and 'setter' method!
> 
> Originally, I used `get_fuel_level` and `set_fuel_level` but that is **not** possible.
> 
> In our case, we **do** want Python's "*property*" **decorator** to do the hard work for us and therefore, we simply rename **both** methods to `fuel_level`.

---

### Getters and Setters Usage

- Modify our `drive` method for `Car` class:

```python
# our main function
def main():
    # create a list to hold objects of different classes
    garage: list = [
        # create first object of the parent class of `Vehicle`
        Vehicle("Mazda", "RX-7 FD", 500000, "Canary Yellow", 65, 1, 1, 1300),
        # create first object of the child class of `Car`
        Car("Nissan", "R32 GTR", 600000, "Black", 55, 1, 1, 2568, 2),
    ]

    # showing "encapsulation" ( after implementation )

    # display the fuel level of the `Vehicle` object before changing
    # INFO: it is accessing the `fuel_level` through the `fuel_level()` getter
    print(f"( Before Encapsulation ) Fuel Level Before Change: {garage[0].fuel_level}")

    # change the fuel level ( directly ) for our `Vehicle` object
    # INFO: it is updating the `fuel_level` through the `fuel_level()` setter
    garage[0].fuel_level = 100

    # display the fuel level of the `Vehicle` object after changing
    # INFO: it is accessing the `fuel_level` through the `fuel_level()` getter
    print(f"( Before Encapsulation ) Fuel Level After Change: {garage[0].fuel_level}")


# source the main function
if __name__ == "__main__":
    main()
```

- *Updated* `main` function:

- Hence, instead of an error, we do get our correct output:

```console
( After Encapsulation ) Fuel Level Before Change: 50
( After Encapsulation ) Fuel Level After Change: 100
```

# Abstraction

> [!INFO] Resource(s)
> - Python 'ABC' Module Official Documentation: https://docs.python.org/3/library/abc.html

> [!WARNING] Its Python!
> 
> If you really want to learn about how *abstraction* actually works; head over to our Java version of this note over at '[[Java - Object Oriented Programming Basics#Abstraction | Java - Object Oriented Programming Basics]]'.
> 
> Because, 'abc' module? It's the first time I am going to use this module... I generally **don't** like 'Object Oriented Programming'.
> 
> > Yeah, what are you going to do... "*Crucify Me*"?
> 
> Therefore, if one day, I work in a place where we use Python and do 'OOP' with it. Then I am going to actually go in-depth with the 'abc' module.
> 
> > I bet you that companies that uses Python, don't really use it for its 'OOP' ( *just use Java or C++* ).

Again, I suggest you to read the '[[Java - Object Oriented Programming Basics#Abstraction | Abstraction]]' from the Java version; because the code below is going to be a shittier version of it.

```python
# INFO: the rest of class implementation stays the same
class Vehicle(ABC):
```

> Yes! I did *import* the `abc` module to get `ABC` and `abstractmethod`!

- In our `Vehicle` class:

```python
    # abstract method to be implemented by other "inherited" classes
    @abstractmethod
    def display_displacement(self) -> None:
        # simply don't write anything
        pass
```

- Our *updated* `main` function:

```python
# our main function
def main():
    # create a list to hold objects of different classes
    garage = [
        # create first object of the child class of `Car` and add to `garage`
        Car("Mazda", "RX-7 FD", 500000, "Canary Yellow", 65, 1, 1, 1300, 2),
        # create second object of the child class of `Car` and add to `garage`
        Car("Nissan", "R32 GTR", 600000, "Black", 55, 1, 1, 2568, 2),
    ]

    # display the engine capacity / displacement of the first 'Car' object
    garage[0].display_displacement()


# source the main function
if __name__ == "__main__":
    main()
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

# Multiple Inheritance

Compared to Java's [[Java - Object Oriented Programming Basics#Multiple Inheritance - Interfaces | interfaces]]; Python is one of the languages that **does** *support* **multiple inheritance**.

Nevertheless, using the 'abc' module and `ABS` plus `abstractmethod`... We are able to "*mimic*" the `interface` from Java.

- Create 'GPS' class

> Again, creation of class because Python because **does** support multiple inheritance.

```python
# "interface" definition for 'GPS' ==> in Python another class definitiona
class GPS(ABC):
    # abstract method to be implemented by other "inherited" classes
    @abstractmethod
    def calculate_route(self) -> None:
        # simply don't write anything
        pass
```

- Implement the `GPS` interface inside the `Car` *child* class ( *updated `Car` class* ).

```python
# our 'Car' subclass from the 'Vehicle' parent class
class Car(Vehicle, GPS):
	# INFO: The rest of the code stays the same!
	
    # implementation of `calculate_route` method from 'GPS' class
    # ==> multiple inheritance / "interface" from Java
    def calculate_route(self) -> None:
        print("\n\t== GPS ( Interface ): Calculating Route ==\n")
```

- *Updated* `main` function to show its usage:

```python
# our main function
def main():
    # create a `nissanGTR` 'Car' object
    nissan_gtr: Car = Car("Nissan", "R32 GTR", 600000, "Black", 55, 1, 1, 2568, 2)

    # simply use the method `calculate_route` on the 'Car' object
    nissan_gtr.calculate_route()


# source the main function
if __name__ == "__main__":
    main()
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

> [!WARNING]
> This is **not** a *compiled* language.
> 
> Therefore, you are going to **have** to write the following code below above the 'Vehicle' class.

```python
# 'Engine' class definition ==> for composition
class Engine:
    def __init__(self, engine_num: int, capacity: int):
        # constructor to define attributes of engine instances
        self.engine_num = engine_num
        self.capacity = capacity


# 'Chassis' class definition ==> for composition
class Chassis:
    # constructor to define attributes of chassis instances
    def __init__(self, chassis_num: int):
        self.chassis_num = chassis_num
```

- Update our 'Vehicle' class so as to use the new objects:

```python
class Vehicle(ABC):
    # constructor to define attributes of vehicle instances
    def __init__(
        self,
        brand: str,
        model: str,
        price: float,
        colour: str,
        health: int,
        engine_num: int,
        chassis_num: int,
        engine_capacity: int,
    ) -> None:
        # intialise the attributes for a vehicle object
        self.brand = brand
        self.model = model
        self.price = price
        self.colour = colour
        self.health = health
        self.engine_num = engine_num
        self.chassis_num = chassis_num
        self.engine_capacity = engine_capacity

        # declare variables from other objects ==> composition
        # INFO: this now has the 'HAS-A' relationship
        # WARNING: we don't pass `engine` and `chassis` as arguments!
        # this is because of how we use it ( see `main` ).
        self.engine = Engine(engine_num, engine_capacity)
        self.chassis = Chassis(chassis_num)

        # class variables for `Vehicle` object
        self.is_running = False
        self.locked = True

        # update the fuel level to be a "private" class / instance variable
        self.__fuel_level = 50
        
    # the rest of the code is the same
```

> [!WARNING]
> After changing the **attributes** to *become* actual **objects**... We are going to have to **access** the *attributes* of those **objects** instead of just using `engineNum`, `engineCapacity` and `chassisNum`.
> 
> > This **has** to be done in both 'Vehicle' and 'Car' class.

- Therefore if we update our `main` function to something like this:

```python
# our main function
def main():
    # create a `nissanGTR` 'Car' object
    nissan_gtr = Car("Nissan", "R32 GTR", 600000, "Black", 55, 1, 1, 2568, 2)

    # simply use the method `calculate_route` on the 'Car' object
    # display the car's information
    nissan_gtr.display_info()


# source the main function
if __name__ == "__main__":
    main()
```

- Thus, we should get and output like so ( *without errors* ):

```console
	 -----------------------------------

		Vehicle Information

	 -----------------------------------

		Brand: Nissan
		Model: R32 GTR
		Price: 600000
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

```python
# 'Driver' class definition ==> for aggregation
class Driver:
    # constructor to define attributes of chassis instances
    def __init__(self, driver_name: str):
        self.driver_name = driver_name
```

- Update our `Vehicle` class implementation:

```python
class Vehicle(ABC):
        # INFO: the rest of the code stays the same
		
        self.engine = Engine(engine_num, engine_capacity)
        self.chassis = Chassis(chassis_num)

        # declare variables for other objects ==> aggregation
        self.vehicle_driver = None

        # class variables for `Vehicle` object
        self.is_running = False
        self.locked = True
		
        # INFO: the rest of the code stays the same
        
    # method to assign driver to a 'vehicle' object ==> aggregation
    def set_driver(self, driver: Driver):
        # get the 'Driver' "object"
        self.vehicle_driver = driver

        # output appropriate message
        print(
            f"\n\t== Driver Name Of '{self.brand} {self.model}': {driver.driver_name} ==\n"
        )
```

- The *updated* `main` function:

```python
# our main function
def main():
    # create a `nissanGTR` 'Car' object
    nissan_gtr: Car = Car("Nissan", "R32 GTR", 600000, "Black", 55, 1, 1, 2568, 2)

    # create the `champion` 'Driver' object
    champion: Driver = Driver("Lewis Hamilton")

    # assign the driver object to the car object
    nissan_gtr.set_driver(champion)


# source the main function
if __name__ == "__main__":
    main()
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

Currently, if I run a the `wc -l main.py` command, I am going to get `401` as *output*.

> Well, this means that we have **401** lines of code in our `main.py` file!

Even though that everything is working fine right now. The way that our `main.py` file is right now it a bit "*dirty*". Adding more things to it would make it **more** *unreadable*, *unmaintainable* and generally a *pain* to work with!

Therefore, I am going to **split** the *codes* inside the `main.py` file in different **folders** and **files** so that its **more** *modular*, *easier to work with* and generally better programming practice.

> Let's get started.

## Project Structure

Here is how the project structure looks like:

```console
 .
├──  components
│   ├──  __init__.py
│   ├──  __pycache__
│   │   ├──  __init__.cpython-314.pyc
│   │   ├──  chassis.cpython-314.pyc
│   │   └──  engine.cpython-314.pyc
│   ├──  chassis.py
│   └──  engine.py
├──  interfaces
│   ├──  __init__.py
│   ├──  __pycache__
│   │   ├──  __init__.cpython-314.pyc
│   │   └──  gps.cpython-314.pyc
│   └──  gps.py
├──  main.py
├──  Makefile
├──  people
│   ├──  __init__.py
│   ├──  __pycache__
│   │   ├──  __init__.cpython-314.pyc
│   │   └──  driver.cpython-314.pyc
│   └──  driver.py
└──  vehicles
    ├──  __init__.py
    ├──  __pycache__
    │   ├──  __init__.cpython-314.pyc
    │   ├──  car.cpython-314.pyc
    │   └──  vehicle.cpython-314.pyc
    ├──  car.py
    └──  vehicle.py
```

> [!NOTE]
> As you know from '[[Java - Object Oriented Programming Basics#Split Files | Java - Object Oriented Programming Basics]]', we have our `package` *keyword* that allows us to specify that a *file* is part of a `package`.
> 
> Well, we **don't** really have that keyword in Python ( *obviously* ).
> 
> > Then how do we tell Python that its a "*package*".
> 
> Well, we simply create an empty `__init__.py` file, inside of each *folder*, whereby that file does *contains* **nothing** inside of it!

## Files Contents

### Components Folder

- `chassis.py` File:

```python
# 'Chassis' class definition ==> for composition
class Chassis:
    # constructor to define attributes of chassis instances
    def __init__(self, chassis_num: int):
        self.chassis_num = chassis_num
```

- `engine.py` File:

```python
# 'Engine' class definition ==> for composition
class Engine:
    def __init__(self, engine_num: int, capacity: int):
        # constructor to define attributes of engine instances
        self.engine_num = engine_num
        self.capacity = capacity
```

### Interfaces Folder

- `gps.py` File:

```python
# import the following module to get "abstraction" in Python
from abc import ABC, abstractmethod


# "interface" definition for 'GPS' ==> in Python another class definitiona
class GPS(ABC):
    # abstract method to be implemented by other "inherited" classes
    @abstractmethod
    def calculate_route(self) -> None:
        # simply don't write anything
        pass
```

### People Folder

- `driver.py` File:

```python
# 'Driver' class definition ==> for aggregation
class Driver:
    # constructor to define attributes of chassis instances
    def __init__(self, driver_name: str):
        self.driver_name = driver_name
```

### Vehicles Folder

- `vehicles.py` File:

```python
# import the following module to get "abstraction" in Python
from abc import ABC, abstractmethod

# import the following components ( class )
from components.chassis import Chassis
from components.engine import Engine

# import the following people ( class )
from people.driver import Driver


class Vehicle(ABC):
    # constructor to define attributes of vehicle instances
    def __init__(
        self,
        brand: str,
        model: str,
        price: float,
        colour: str,
        health: int,
        engine_num: int,
        chassis_num: int,
        engine_capacity: int,
    ) -> None:
        # intialise the attributes for a vehicle object
        self.brand = brand
        self.model = model
        self.price = price
        self.colour = colour
        self.health = health
        self.engine_num = engine_num
        self.chassis_num = chassis_num
        self.engine_capacity = engine_capacity

        # declare variables from other objects ==> composition
        # INFO: this now has the 'HAS-A' relationship
        # WARNING: we don't pass `engine` and `chassis` as arguments!
        # this is because of how we use it ( see `main` ).
        self.engine = Engine(engine_num, engine_capacity)
        self.chassis = Chassis(chassis_num)

        # declare variables for other objects ==> aggregation
        self.vehicle_driver = None

        # class variables for `Vehicle` object
        self.is_running = False
        self.locked = True

        # update the fuel level to be a "private" class / instance variable
        self.__fuel_level = 50

    # abstract method to be implemented by other "inherited" classes
    @abstractmethod
    def display_displacement(self) -> None:
        # simply don't write anything
        pass

    # static method that is going to display a simple horizontal rule
    @staticmethod
    def display_rule(num_of_chars) -> None:
        print("\n\t", "-" * num_of_chars, "\n")

    # method that will be able to display the information about vehicle
    def display_info(self) -> None:
        self.display_rule(35)
        print("\t\tVehicle Information")
        self.display_rule(35)

        print(f"\t\tBrand: {self.brand}")
        print(f"\t\tModel: {self.model}")
        print(f"\t\tPrice: {self.price}")
        print(f"\t\tColour: {self.colour}")
        print(f"\t\tHealth: {self.health}")
        print(f"\t\tEngine Number: {self.engine.engine_num}")
        print(f"\t\tChassis Number: {self.chassis.chassis_num}")
        print(f"\t\tEngine Capacity: {self.engine.capacity}")

        self.display_rule(35)

    # method that is going to be able to lock the vehicle
    def lock(self) -> None:
        # check if the vehicle has already been locked
        if self.locked:
            # output appropriate message
            print("\n\t<< Vehicle Has Already Been Locked!!! >>\n")

        # if the vehicle has not been locked yet ==> lock the doors
        else:
            self.locked = True

            # output appropriate message
            print("\n\t<< Vehicle Has Now Been Locked!!! >>\n")

    # method that is going to be able to unlock the vehicle
    def unlock(self) -> None:
        # check if the vehicle has already been locked
        if not self.locked:
            # output appropriate message
            print("\n\t<< Vehicle Has Already Been Unlocked!!! >>\n")

        # if the vehicle has not yet been unlocked ==> unlock the doors
        else:
            self.locked = False

            # output appropriate message
            print("\n\t<< Vehicle Has Now Been Unlocked!!! >>\n")

    # method that is going to be able to start the engines of the vehicle
    def start_engine(self) -> None:
        # check if the vehicle's engine has already been running
        if self.is_running:
            # output appropriate message
            print("\n\t<< Vehicle's Engines Has Already Been Running!!! >>\n")

        # if the vehicle's engine has not yet been running ==> start the engines
        else:
            self.is_running = True

            # output appropriate message
            print("\n\t<< Vehicle's Engines Was Started And Now Running!!! >>\n")

    # method that is going to be able to stop the engines of the vehicle
    def stop_engine(self) -> None:
        # check if the vehicle's engine has already been "off"
        if not self.is_running:
            # output appropriate message
            print("\n\t<< Vehicle's Engines Has Already Been 'Off'!!! >>\n")

        # if the vehicle's engine has been running ==> stop the engines
        else:
            self.is_running = False

            # output appropriate message
            print("\n\t<< Vehicle's Engines Was Stopped!!! >>\n")

    # method that is going allow the vehicle to drive
    def drive(self) -> None:
        # first check if the vehicle has fuel to start with
        if self.__fuel_level == 0:
            # output appropriate message
            print("\n\t<< Please Refuel Vehicle >>\n")

            # return to the "main" function
            return

        # if the vehicle's engines are not running
        if not self.is_running:
            # output appropriate message
            print("\n\t<< Engines Has Not Yet Been Started - Fuel Level Good!!! >>\n")

            # ask the user if he / she wants to start the vehicle's engines
            start_vehicle = input("Do You Want To Start The Engines[y/n]: ")

            # if the user wants does NOT to start the engines
            if start_vehicle.lower() != "y":
                return

            # change the current running status
            self.is_running = True

        # check if we have a minimum level of fuel to be able to drive the car
        if self.__fuel_level < 10:
            # output appropriate message
            print("\n\t<< The Vehicle Need To Be Refueled!!! >>\n")

        # if the vehicle has fuel and engines has already been started
        print("\n\t== The Vehicle Is Being Driven!!! ==\n")

        # decrease the fuel level by '5' but don't let it go below '0'
        self.__fuel_level = max(0, self.__fuel_level - 5)

    # method that is going allow the vehicle to brake
    def brake(self) -> None:
        # display a simple message that will show vehicle is braking
        print("\n\t== The Vehicle Is Slowing Down / Braking! ==\n")

    # getter method for `fuel_level` to get fuel level of vehicle
    # INFO: see how we are using the decorator here
    @property
    def fuel_level(self) -> int:
        # simply return the fuel level to whoever is asking for it
        return self.__fuel_level

    # setter method for `fuel_level` to update fuel level of vehicle
    # INFO: see how we are using the decorator here ==> same method name as 'getter'
    @fuel_level.setter
    def fuel_level(self, user_fuel_level: int) -> None:
        # update the `fuel_level` through the parameter / argument
        self.__fuel_level = max(0, min(user_fuel_level, 100))

    # method that is going to allow us to refuel the vehicle
    def refuel(self) -> None:
        # check if tank is already full for vehicle
        if self.__fuel_level == 100:
            # output appropriate message
            print("\n\t<< Vehicle's Fuel Tank Already Full!!! >>\n")

        # if the fuel level for vehicle is less than '100'
        elif self.__fuel_level < 100:
            # output appropriate message
            print("\n\t== Refuelling The Vehicle ==\n")

            # increase the fuel level by '10' but don't let it go above 100
            self.__fuel_level = min(self.__fuel_level + 10, 100)

    # method that is going to allow us to repair the vehicle
    def repair(
        self, part_name=None, estimated_cost=None, repair_type: str = "general"
    ) -> None:
        # check if its a general servicing
        if repair_type == "general":
            # check for the vehicle's health
            if self.health >= 70:
                # output appropriate message
                print("\n\t<< Vehicle's Already Repaired!!! >>\n")

            else:
                # increase the health level by '10' but don't let it go above 100
                self.health = min(self.health + 10, 100)

                # output appropriate message
                print("\n\t== Repairing The Vehicle ==\n")

        # if the repair is a specific service
        elif repair_type == "specific":
            print(
                f"\n\t== Part Damaged: {part_name} | Estimated Cost: {estimated_cost} ==\n"
            )

        # if the repair type does not exists
        else:
            # output appropriate message
            print("\n\t<< Repair Type Does NOT Exists!!! >>\n")

    # method to assign driver to a 'vehicle' object ==> aggregation
    def set_driver(self, driver: Driver):
        # get the 'Driver' "object"
        self.vehicle_driver = driver

        # output appropriate message
        print(
            f"\n\t== Driver Name Of '{self.brand} {self.model}': {driver.driver_name} ==\n"
        )
```

- `car.py` File:

```python
# import the following "interfaces" ( class )
from interfaces.gps import GPS

# import the actual vehicle class
from vehicles.vehicle import Vehicle


# our 'Car' subclass from the 'Vehicle' parent class
class Car(Vehicle, GPS):
    # constructor to define the attributes of car instances
    def __init__(
        self,
        brand: str,
        model: str,
        price: float,
        colour: str,
        health: int,
        engine_num: int,
        chassis_num: int,
        engine_capacity: int,
        num_of_doors: int,
    ) -> None:
        # set the vehicle's attributes to the 'Vehicle' class
        super().__init__(
            brand,
            model,
            price,
            colour,
            health,
            engine_num,
            chassis_num,
            engine_capacity,
        )

        # initialise specific attributes for the 'Car' class
        self.num_of_doors = num_of_doors

        # class instance variable for 'Car' object
        self.trunk_status = "closed"

    # specific method for the 'Car' class to open the object's trunk
    def open_trunk(self) -> None:
        # check if the car's trunk has already been opened
        if self.trunk_status == "opened":
            # output appropriate message
            print("\n\t<< Car's Trunk Has Already Been Opened!!! >>\n")

        # if the car's trunked has not yet been opened ==> open the trunk
        else:
            self.trunk_status = "opened"

            # output appropriate message
            print("\n\t<< Car's Trunk Has Been Opened!!! >>\n")

    # specific method for the 'Car' class to close the object's trunk
    def close_trunk(self) -> None:
        # check if the car's trunk has already been closed
        if self.trunk_status == "closed":
            # output appropriate message
            print("\n\t<< Car's Trunk Has Already Been Closed!!! >>\n")

        # if the car's trunked has not yet been closed ==> close the trunk
        else:
            self.trunk_status = "closed"

            # output appropriate message
            print("\n\t<< Car's Trunk Has Been Closed!!! >>\n")

    # INFO: overriden `drive` method for the 'Car' subclass
    def drive(self) -> None:
        # check if the trunk is open or now
        if self.trunk_status == "opened":
            # output appropriate message
            print("\n\t<< Trunk Is Open! ==> Cannot Drive Car!!! >>\n")

            # return to the "main" function
            return

        # 'Car' objects drive in 'Sport' mode only
        print("\n\t== Car Drive Mode: Sport ==\n")

        # get the current fuel level of the 'Car' object
        # NOTE: this is using the 'getter' method `fuel_level`!
        # personally, I don't really know how it works interally but from what I
        # understand; Python and the `@property` is going its magic
        # and using `fuel_level()` automatically ==> just need to simply use `self.fuel_level`
        fuel_before_drive = self.fuel_level

        # NOTE: call the actual implementation from Vehicle's `drive` method
        # therefore, in this way; we can still get the implementation of `drive`
        # WITHOUT needing to re-write everything again!
        # WARNING: we added the line below here because:
        # 1. we need to check if the trunk is open first
        # 2. we need to make sure that the we override the fuel level
        # ( given 'Sport' mode... We should remove more fuel )
        super().drive()

        # update the fuel level in addition to the Vehicle's `drive` method fuel burn
        # this means that consume fuel in `super().drive()` and also Car's `drive` method
        if self.fuel_level < fuel_before_drive:
            # NOTE: this is using the 'setter' method `fuel_level`!
            # again, the `@property` is doings its magic and therefore, we only
            # have to do this: `self.fuel_level = ...`
            self.fuel_level = max(0, self.fuel_level - 2)

    # INFO: overriden `brake` method for the 'Car' subclass
    def brake(self) -> None:
        # NOTE: call the actual implementation from Vehicle's `brake` method
        super().brake()

        # 'Car' objects has ABS engaged ==> display it
        print("\t== ABS Engaged: Controlled Braking ==\n")

    # implementation of `display_displacement` method in `Car` class
    def display_displacement(self) -> None:
        # display the displacement of the 'Car' object
        print(f"\n\t== Engine Displacement: {self.engine.capacity}cc " + "==\n")

    # implementation of `calculate_route` method from 'GPS' class
    # ==> multiple inheritance / "interface" from Java
    def calculate_route(self) -> None:
        print("\n\t== GPS ( Interface ): Calculating Route ==\n")
```

### Main Files

> [!WARNING]
> The following **codes** below were *written* by 'Big Pickle' ( *which is basically [GLM](https://z.ai)* )  Haiku through [Opencode](https://opencode.ai/)!

- `main.py` File:

```python
# import the following components ( class )
from components.chassis import Chassis
from components.engine import Engine

# import the actual vehicle class
from vehicles.vehicle import Vehicle

# import the class car
from vehicles.car import Car

# import the following "interfaces" ( class )
from interfaces.gps import GPS

# import the following people ( class )
from people.driver import Driver


# our main function
def main() -> None:
    # Object Creation & Inheritance
    nissan_gtr: Car = Car("Nissan", "R32 GTR", 600000, "Black", 55, 1, 1, 2568, 2)
    bmw_m3: Car = Car("BMW", "E46 M3", 85000, "Silver", 70, 2, 2, 3246, 4)
    tesla_model_s: Car = Car(
        "Tesla", "Model S Plaid", 130000, "Red", 90, 3, 3, 0, 4
    )

    # Encapsulation - Display Vehicle Info
    nissan_gtr.display_info()

    # Aggregation - Assign Driver
    champion: Driver = Driver("Lewis Hamilton")
    nissan_gtr.set_driver(champion)

    # Method Overloading - repair() with default vs specific
    nissan_gtr.repair()
    nissan_gtr.repair(
        part_name="Brake Pads", estimated_cost=250, repair_type="specific"
    )

    # Abstraction - Abstract method implementation
    nissan_gtr.display_displacement()

    # Interfaces - GPS interface usage
    gps: GPS = nissan_gtr
    gps.calculate_route()

    # State Management - Lock/Unlock & Engine Control
    nissan_gtr.unlock()
    nissan_gtr.lock()
    nissan_gtr.lock()
    nissan_gtr.start_engine()
    nissan_gtr.stop_engine()
    nissan_gtr.start_engine()

    # Car-specific - Trunk Operations
    nissan_gtr.open_trunk()
    nissan_gtr.open_trunk()
    nissan_gtr.close_trunk()

    # Polymorphism - List of Vehicles
    garage: list[Vehicle] = [nissan_gtr, bmw_m3, tesla_model_s]

    # Polymorphic behavior - overridden methods
    for v in garage:
        v.display_info()
        v.display_displacement()
        v.refuel()
        v.brake()

    # Refueling & Fuel Management
    print(f"Fuel Before: {nissan_gtr.fuel_level}")
    nissan_gtr.refuel()
    print(f"Fuel After: {nissan_gtr.fuel_level}")

    # Drive Operations - Interactive with input()
    nissan_gtr.start_engine()
    nissan_gtr.drive()
    nissan_gtr.brake()
    nissan_gtr.stop_engine()


# source the main function
if __name__ == "__main__":
    main()
```

- `Makefile` File:

```bash
program:
	@python main.py
```

> Yeah... I know, don't you dare fucking roast me... `make` is shorter to *type* than `python main.py`!

### The Output

```console
	 ----------------------------------- 

		Vehicle Information

	 ----------------------------------- 

		Brand: Nissan
		Model: R32 GTR
		Price: 600000
		Colour: Black
		Health: 55
		Engine Number: 1
		Chassis Number: 1
		Engine Capacity: 2568

	 ----------------------------------- 


	== Driver Name Of 'Nissan R32 GTR': Lewis Hamilton ==


	== Repairing The Vehicle ==


	== Part Damaged: Brake Pads | Estimated Cost: 250 ==


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
		Price: 600000
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
		Price: 85000
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
		Price: 130000
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