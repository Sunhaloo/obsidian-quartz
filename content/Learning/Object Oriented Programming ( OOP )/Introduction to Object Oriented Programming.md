---
id: Introduction to Object Oriented Programming
aliases: Object Oriented Progamming Fundamentals and Understanding
tags:
  - theory
  - basics
  - oop
author: S.Sunhaloo
date: 2025-09-05
status: Completed
---

## List of Contents

- [[#Theoretical Part of Object Oriented Programming]]
	- [[#Classes and Instances]]
	- [[#Instances / Objects]]
	- [[#Inheritance]]
	- [[#Encapsulation]]
	- [[#Polymorphism]]
		- [[#Method Overloading - Compile Time ( Static ) Polymorphism]]
		- [[#Method Overriding - Runtime ( Dynamic ) Polymorphism]]
- [[#Practical Part of Object Oriented Programming]]

---

> [!INFO] Resources
> 
> - https://en.wikipedia.org/wiki/Object-oriented_programming
> - https://developer.mozilla.org/en-US/docs/Learn_web_development/Extensions/Advanced_JavaScript_objects/Object-oriented_programming
> - https://www.geeksforgeeks.org/dsa/introduction-of-object-oriented-programming/
> 	- [David Sha](https://davidsha.me/) changed my mind about Geeks For Geeks... But still be careful as a beginner.
> - https://stackoverflow.com/questions/12374399/what-is-the-difference-between-method-overloading-and-overriding

# Theoretical Part of Object Oriented Programming

## What is Object Oriented Programming?

The 'Object Oriented Programming' Paradigm focuses itself on modelling *real life* entities or **objects** and having <span style="color: orange;"> specific</span> **attributes** ( "*properties*" ) and **methods** ( "*functions*" ) associated to each of them.

From my past experience of using the 'OOP' paradigm... It focuses heavily on **abstraction** and **hiding** the *complexities* of code from the user.

This "*abstraction*" is made possible by the following methods... Here are the **four** pillars of Object Oriented Programming:

1. Encapsulation
2. Abstraction
3. Inheritance
4. Polymorphism

### Classes and Instances

A class is basically a *user-defined* datatype which consists of **data members** having their own little *attributes* and *methods*!

Each **instance** in *that* class share the **same** *attributes* and *methods*; whereby when object is created... We can only apply the *methods* found **within** its class.

Think of a **class of '_Building_'**. There are many buildings that exists and but each has a **different** *type* and *purpose*. For example, a building can be a '*hospital*' or '*library*'.

Both of them might be "*fundamentally*" the **same**; and even share some properties like, having a toilet, etc. But in terms of *usage* and how people interact with them are completely **different**!

> It's the **blueprint** for creating / defining an Object!

#### Instances / Objects

Now, consider the following example: Given a class of `Vehicle`. We know that we have many **brands** and **types** of `Vehicle`.

Let's say that we have a [Dacia Sandero](https://en.wikipedia.org/wiki/Dacia_Sandero). Therefore, we can say *that* this **specific** '*Dacia Sandero*' is an **instance** or **object** of the class `Vehicle`!

Similarly, if you have a [Nissan R35 GTR](https://en.wikipedia.org/wiki/Nissan_GT-R). This is considered to be **another** instance of the class `Vehicle`.

Now, these 2 objects are *fundamentally* the **same** but the will *behave* differently in addition to having different *properties*! For example: the 'GTR' will have more horsepower and might have a different colour compared to the 'Dacia'.

### Inheritance

Going back to our example of our class of `Vehicle`. Its safe to say that a *car* is pretty much the **same** as a, let's say *lorry*!

Both of them have **similar** attributes like:

- Size
- Weight
- Horsepower
- Engine Number
- Chassis Number

> Additionally, both of them can `start`, `drive` and `refuel`!

Nevertheless, some of the things like 'number of doors', 'load capacity' and some other *data* / *attribute* might not be the **same**!

> This is where **inheritance** comes into play!

Instead of creating **separate** classes, one for `Car` and another one for `Lorry`... We can *inherit* the **parent** / **superclass** of `Vehicle` so that the **child** / **subclass** `Car` and `Lorry` can **inherit** some of the *attributes* that are found in the class of `Vehicles`!

This helps us in a few ways:

1. Improves code organisation
2. No need to write **same** attributes a number of times
3. **Modifying** *parent* or *children* class can be easily done

### Encapsulation

'Encapsulation' is the practice of **bundling** an object's *data* / *attributes* and the *methods* that operate on that data into a single, **self-contained** ( *isolated* ) unit: the **class**.

> Its primary purpose is to **control access** to the object's *data* from the outside world.

This is often referred to as **data hiding** or information hiding. By making *attributes* `private`, we **prevent** them from being directly *accessed* or *modified*. We then provide `public` methods ( *like `getters` and `setters`* ) as the **only** way to *interact* with that **private** data.

Think of it like a pill capsule . The outer shell ( *i.e the class* ) holds and protects the active ingredients ( *i.e the data and methods* ) inside. You can't just open the capsule and pour out the ingredients; you have to swallow the whole thing, which is the intended way to use it.

This ensures the *data* remains in a **valid** and **consistent state**, making the code more **robust** and **easier** to *maintain*.

> [!NOTE]
> - **Encapsulation** *protects* the **data** ( *inside the `class`es* )
> - **Abstraction** *protects* the **structure** ( *between the `class`es* )

### Polymorphism

As the word '*Polymorphism*' suggests... "*It can take many forms*"! For example: An *object* the subclass of `Car` be have **different** characteristics like that `Car` object can be:

- Sports Car
- Coupe
- High Performance
- Carbon Fibre

But each characteristic is going to be based on a *set period of time*... For example, the characteristic of '*High Performance*' and '*Carbon Fibre*' is going to shine through on the track while the characteristic of '*Coupe*' is going to shine through in the city as its small!

What I am trying it say that it can *change* depending on what is doing. In terms of **methods**. Let' say that we have a method `drive` for the subclass of `Lorry` which shows that an instance of `Lorry` is driving. But if we can have the **same** `drive` method but it will show that an instance of a `Car` is driving!

> Same **method** name but different *behaviour* **depending** on the class!

#### Method Overloading - Compile Time ( Static ) Polymorphism

Think of the subclass of `Vehicle` whereby we do also have "*a*" `drive` function.

Given that a `drive` method can take **only one parameter** and will show that **one** object of the parent / subclass of `Vehicle` is driving.

We can also have *another* `drive` method ( _Yes! with the **same** name_ ) that now takes **two parameters** and is going show that *2* objects of the parent / subclass of `Vehicle` are driving.

> Method **Overloading** happens inside the **same** class!

#### Method Overriding - Runtime ( Dynamic ) Polymorphism

> This is what is considered as the "*real*" Polymorphism!

Method **Overriding** compared to Method **Overloading** is a bit different in terms that is happens in **multiple** classes!

> Let's take a look at an example with our `Vehicle`, `Car` and `Lorry` class!

Given that we again have a method called `drive` that is present inside the `Vehicle` class; which when used with tell us that a "*vehicle*" is being driven.

Now, let's create a method with the **same** name as `drive` but now inside the `Car` class!
Now, when you call the `drive` method on a *instance* of a `Car`. Instead of seeing that a "*vehicle*" is driving; we are going to see that a **Car is being driven**!

> Method **Overriding** happens in **different** ( *parent - child* ) classes and based on an *instance* of a **specific** class!

---

# Practical Part of Object Oriented Programming

I am going to now try to implement '*Object Oriented Programming*' in **both** [[Learning/Python/Python Data View | Python]] and [[Learning/Java/Java Data View | Java]].

Therefore please refer to the note / files that I have linked below!

> [!INFO] Notes / Files Associated With Object Oriented Programming "*Notes*"
> 
> - [[Python - Object Oriented Programming Basics]]
> - [[Java - Object Oriented Programming Basics]]

> [!WARNING] Friendly Warning
> 
> When making the notes for the Python and Java versions... I coded for / in the [[Python - Object Oriented Programming Basics | Python]] part **first**
>
> Therefore, there are going be some things "*missing*" ( *per se* ) from the [[Java - Object Oriented Programming Basics | Java]] version.
>
> Hence, **note to future me**... Remember to open up both the Python and Java version to understand the notes that I took!

---

# Socials

- **Instagram**: https://www.instagram.com/s.sunhaloo
- **YouTube**: https://www.youtube.com/@s.sunhaloo
- **GitHub**: https://www.github.com/Sunhaloo

---

S.Sunhaloo
Thank You!