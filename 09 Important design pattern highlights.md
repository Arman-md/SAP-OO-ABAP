# 1. The Observer Pattern
**Keeping your Objects in the Know**  
You don’t want to miss out when something interesting happens, do you?  
We’ve got a pattern that keeps your objects **in the know** when something they care about happens.  
It’s the **Observer Pattern**—one of the most commonly used design patterns, and it’s incredibly useful.

We’ll look at:
- **One-to-many relationships**
- **Loose coupling**

---

<img width="521" height="303" alt="image" src="https://github.com/user-attachments/assets/6c350715-635b-49da-be50-af5ae5a4c5bc" />


### 📚 Topics Covered
- The Weather Monitoring application overview — *p.39*
- Meet the Observer Pattern — *p.44*
- Publishers + Subscribers = Observer Pattern — *p.45*
- The Observer Pattern defined — *p.51*
- The Power of Loose Coupling — *p.54*
- Designing the Weather Station — *p.57*
- Implementing the Weather Station — *p.58*
- Power up the Weather Station — *p.61*
- Looking for the Observer Pattern in the Wild — *p.65*
- Coding the life-changing application — *p.66*
- Meanwhile, back at Weather-O-Rama — *p.69*
- Test Drive the new code — *p.71*
- Tools for your Design Toolbox — *p.72*
- Design Principle Challenge — *p.73*

---

### 🧠 OO Principles
- **Encapsulate what varies**
- **Favor Composition over inheritance**
- **Program to interfaces, not implementations**
- **Strive for loosely coupled designs between objects that interact**

<img width="403" height="389" alt="image" src="https://github.com/user-attachments/assets/c389a3cf-efe2-4cb0-b84f-6f33a2677f01" />

---



# 📘 The Decorator Pattern

## 3. Decorating Objects
**Just call this chapter “Design Eye for the Inheritance Guy.”**  
We’ll re-examine the typical overuse of inheritance and you’ll learn how to decorate your classes at runtime using a form of object composition.  

**Why?**  
Once you know the techniques of decorating, you’ll be able to give your (or someone else’s) objects new responsibilities **without making any code changes to the underlying classes**.

---

<img width="373" height="460" alt="image" src="https://github.com/user-attachments/assets/043ff929-174b-4c28-aa8e-a328cc4dbe0a" />


---

### 📚 Topics Covered
- Welcome to Starbuzz Coffee — *p.80*
- The Open-Closed Principle — *p.86*
- Meet the Decorator Pattern — *p.88*
- Constructing a drink order with Decorators — *p.89*
- The Decorator Pattern defined — *p.91*
- Decorating our Beverages — *p.92*
- Writing the Starbuzz code — *p.95*
- Coding beverages — *p.96*
- Coding condiments — *p.97*
- Serving some coffees — *p.98*
- Real-World Decorators: Java I/O — *p.100*
- Decorating the java.io classes — *p.101*
- Writing your own Java I/O Decorator — *p.102*
- Test out your new Java I/O Decorator — *p.103*
- Tools for your Design Toolbox — *p.105*

---



# 📘 The Factory Pattern

## 4. Baking with OO Goodness
**Get ready to bake some loosely coupled OO designs.**  
There is more to making objects than just using the `new` operator.  
You’ll learn that instantiation is an activity that shouldn’t always be done in public and can often lead to **coupling problems**.  
And we don’t want that, do we?  

Find out how Factory Patterns can help save you from embarrassing dependencies.

<img width="962" height="901" alt="image" src="https://github.com/user-attachments/assets/78f1f39c-67de-4e8c-a26f-28ea4b73a6bd" />

---

### 📚 Topics Covered
- Identifying the aspects that vary — *p.112*
- Encapsulating object creation — *p.114*
- Building a simple pizza factory — *p.115*
- The Simple Factory defined — *p.117*
- A framework for the pizza store — *p.120*
- Allowing the subclasses to decide — *p.121*
- Declaring a factory method — *p.125*
- It’s finally time to meet the Factory Method Pattern — *p.131*
- View Creators and Products in Parallel — *p.132*
- Factory Method Pattern defined — *p.134*
- Looking at object dependencies — *p.138*
- The Dependency Inversion Principle — *p.139*
- Applying the Principle — *p.140*
- Families of ingredients… — *p.145*
- Building the ingredient factories — *p.146*
- Reworking the pizzas… — *p.149*
- Revisiting our pizza stores — *p.152*
- What have we done? — *p.153*
- Abstract Factory Pattern defined — *p.156*
- Factory Method and Abstract Factory compared — *p.160*
- Tools for your Design Toolbox — *p.162*

---

### 🔍 Key Concept
> Factory Patterns help you **encapsulate object creation** and reduce coupling between classes.

---

✅ Ready to use as `FactoryPattern.md` or part of your GitHub `README.md`.


# Recap :


# 📘 Design Patterns Summary

## Strategy Pattern
**Definition:**  
Defines a family of algorithms, encapsulates each one, and makes them interchangeable.  
Strategy lets the algorithm vary independently from clients that use it.

---

## Observer Pattern
**Definition:**  
Defines a one-to-many dependency between objects so that when one object changes state, all its dependents are notified and updated automatically.

---

## Decorator Pattern
**Definition:**  
Attach additional responsibilities to an object dynamically.  
Decorators provide a flexible alternative to subclassing for extending functionality.

---

## Abstract Factory Pattern
**Definition:**  
Provide an interface for creating families of related or dependent objects without specifying their concrete classes.

---

# 📘 The Singleton Pattern

## 5. One-of-a-Kind Objects
**Our next stop is the Singleton Pattern, our ticket to creating one-of-a-kind objects for which there is only one instance, ever.**  
You might be happy to know that of all patterns, the Singleton is the simplest in terms of its class diagram; in fact, the diagram holds just a single class!  
But don’t get too comfortable; despite its simplicity from a class design perspective, it’s going to require some deep object-oriented thinking in its implementation.

---

### 📚 Topics Covered
- Dissecting the classic Singleton Pattern implementation — *p.173*
- The Chocolate Factory — *p.175*
- Singleton Pattern defined — *p.177*
- Houston, we have a problem — *p.178*
- Dealing with multithreading — *p.180*
- Can we improve multithreading? — *p.181*
- Meanwhile, back at the Chocolate Factory… — *p.183*
- Tools for your Design Toolbox — *p.186*

---

### 🔍 Key Concept
> **Singleton Pattern:** Ensure a class only has one instance and provide a global point of access to it.

---



# 📘 The Command Pattern

## 6. Encapsulating Invocation
**In this chapter, we take encapsulation to a whole new level: we’re going to encapsulate method invocation.**  
By encapsulating method invocation, we can crystallize pieces of computation so that the object invoking the computation doesn’t need to worry about how to do things—it just uses our crystallized method to get it done.  

We can also do some smart things with these encapsulated method invocations, like:
- Save them away for logging
- Reuse them to implement **undo functionality** in our code


<img width="655" height="721" alt="image" src="https://github.com/user-attachments/assets/789ecd47-66a0-4c0a-96d4-170709255f18" />

---

### 📚 Topics Covered
- Home Automation or Bust — *p.192*
- Taking a look at the vendor classes — *p.194*
- A brief introduction to the Command Pattern — *p.197*
- From the Diner to the Command Pattern — *p.201*
- Our first command object — *p.203*
- Using the command object — *p.204*
- Assigning Commands to slots — *p.209*
- Implementing the Remote Control — *p.210*
- Implementing the Commands — *p.211*
- Putting the Remote Control through its paces — *p.212*
- Time to write that documentation… — *p.215*
- What are we doing? — *p.217*
- Time to QA that Undo button! — *p.220*
- Using state to implement Undo — *p.221*
- Adding Undo to the Ceiling Fan commands — *p.222*
- Every remote needs a Party Mode! — *p.225*
- Using a macro command — *p.226*
- More uses of the Command Pattern: queuing requests — *p.229*
- More uses of the Command Pattern: logging requests — *p.230*
- Command Pattern in the Real World — *p.231*
- Tools for your Design Toolbox — *p.233*

---

### 🔍 Key Concept
> **Command Pattern:** Encapsulate a request as an object, thereby letting you parameterize clients with different requests, queue or log requests, and support undoable operations.

---



# 📘 The Adapter and Facade Patterns

## 7. Being Adaptive
In this chapter, we’re going to attempt such impossible feats as **putting a square peg in a round hole**.  
Sound impossible? Not when we have Design Patterns.  

Remember the **Decorator Pattern**? We wrapped objects to give them new responsibilities.  
Now we’re going to wrap some objects with a different purpose: **to make their interfaces look like something they’re not**.  

Why would we do that?  
So we can adapt a design expecting one interface to a class that implements a different interface.  
That’s not all; while we’re at it, we’re going to look at another pattern that wraps objects to **simplify their interface**.


<img width="581" height="607" alt="image" src="https://github.com/user-attachments/assets/42e5f842-2ce7-4a68-9bfa-5efe24ba0249" />


<img width="1215" height="615" alt="image" src="https://github.com/user-attachments/assets/74089ef3-ba22-4cc9-864a-145d0d80d645" />

---

### 📚 Topics Covered
- Adapters all around us — *p.238*
- Object-oriented adapters — *p.239*
- If it walks like a duck and quacks like a duck, then it must be a duck turkey wrapped with a duck adapter… — *p.240*
- Test drive the adapter — *p.242*
- The Adapter Pattern explained — *p.243*
- Adapter Pattern defined — *p.245*
- Object and class adapters — *p.246*
- Real-world adapters — *p.250*
- Adapting an Enumeration to an Iterator — *p.251*
- Home Sweet Home Theater — *p.257*
- Watching a movie (the hard way) — *p.258*
- Lights, Camera, Facade! — *p.260*
- Constructing your home theater facade — *p.263*
- Implementing the simplified interface — *p.264*
- Time to watch a movie (the easy way) — *p.265*
- Facade Pattern defined — *p.266*
- The Principle of Least Knowledge — *p.267*
- How NOT to Win Friends and Influence Objects — *p.268*
- The Facade Pattern and the Principle of Least Knowledge — *p.271*
- Tools for your Design Toolbox — *p.272*

---

### 🔍 Adapter Pattern Diagram
``

