---
id: Python - Object Oriented Programming Basics
aliases: Object Oriented Prgramming Basics in Python
tags:
  - python
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

## Implementing the Motorcycle Subclass



## Implementing the Lorry Subclass

---

# Socials

- **Instagram**: https://www.instagram.com/s.sunhaloo
- **YouTube**: https://www.youtube.com/@s.sunhaloo
- **GitHub**: https://www.github.com/Sunhaloo

---

S.Sunhaloo
Thank You!