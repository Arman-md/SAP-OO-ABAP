
# Polymorphism in Object-Oriented Programming

**Definition**  
Polymorphism means *many shapes*. In programming, it refers to:  
> *“…the provision of a single interface to entities of different types.”*  
(Source: [Oracle Java Tutorial](https://docs.oracle.com/javase/tutorial/javamethod name based on context.

---

## Types of Polymorphism

### 1. Static Polymorphism (Compile-time)
- Achieved via **method overloading**.
- Same method name, different signatures (parameter count or types).
- Example:
    ```pseudo
    class textFormatter
      method advancePointer(a type integer, b type integer)
        return a + b

      method advancePointer(a type integer, b type integer, c type integer)
        return a + b + c
    ```

#### How It Works
- The **number and type of parameters** supplied by the caller determine which implementation is executed.
- Example:
    ```pseudo
    spacesBetweenWords type integer
    positionOfThisWord type integer
    lengthOfThisWord type integer

    positionOfNextWord = advancePointer(positionOfThisWord, lengthOfThisWord, spacesBetweenWords)
    positionOfComma    = advancePointer(positionOfThisWord, lengthOfThisWord)
    ```
- **Binding**: Occurs at compile-time (statically bound). Cannot change during execution.
- Supported by languages like **C++, C#, Java**.
- **ABAP does NOT support static polymorphism** (method overloading is not available).

---

### 2. Dynamic Polymorphism (Runtime)
- Achieved via **method overriding** in inheritance.
- Behavior determined by the **dynamic type** of the object at runtime.
- Implemented through **dynamic dispatch**:
    - The actual instance type decides which method implementation runs.
- **Static methods cannot be overridden**, so dynamic polymorphism applies only to instance methods.

---

## Key Differences
| Feature              | Static Polymorphism       | Dynamic Polymorphism       |
|----------------------|---------------------------|----------------------------|
| Binding             | Compile-time             | Runtime                   |
| Technique           | Method Overloading       | Method Overriding         |
| Flexibility         | Limited                  | High                      |
| ABAP Support        | ❌ Not Supported         | ✅ Supported              |

---

### Notes
- ABAP deviates from Java and similar languages by **not supporting method overloading**.
- Dynamic polymorphism in ABAP is implemented using `METHODS ... REDEFINITION` in subclasses.



# Dynamic Polymorphism in Object-Oriented Programming

**Definition**  
Dynamic polymorphism occurs when a method call is made through an object reference variable whose **static type** and **dynamic type** are different.  
- **Static type**: The type declared for the reference variable.
- **Dynamic type**: The actual type of the object instance at runtime.

Dynamic dispatch ensures that the method implementation corresponding to the **dynamic type** is executed.

---

## Example: Watercraft Hierarchy

### Class Hierarchy

<img width="550" height="280" alt="image" src="https://github.com/user-attachments/assets/547146e3-3a5c-4a3e-b40b-5df720613bb9" />

!Class Diagram

---

### Listing 6-1: Abstract Class `boat`
```pseudo
abstract class boat
  public abstract method start
  public abstract method turnLeft
  public abstract method turnRight
  public abstract method stop
endclass

```

``` PSEUDO
class motorBoat inherits from boat
  public method start
    engage propeller
  endmethod

  public method turnLeft
    rotate steering wheel counterclockwise
  endmethod

  public method turnRight
    rotate steering wheel clockwise
 
```


``` PSEUDO

class sailBoat inherits from boat
  public method start
    raise sail
  endmethod

  public method turnLeft
    push tiller to right
  endmethod

  public method turnRight
    push tiller to left
  endmethod

  public method stop
    lower sail
  endmethod
endclass


```


### Initial Marina Implementation (No Polymorphism)

``` PSEUDO

class marina
  public method launchMotorBoat
    thisMotorBoat type class of motorBoat
    create new instance of motorBoat into thisMotorBoat
    call method maneuverMotorBoat(thisMotorBoat)
  endmethod

  public method launchSailBoat
    thisSailBoat type class of sailBoat
    create new instance of sailBoat into thisSailBoat
    call method maneuverSailBoat(thisSailBoat)
  endmethod

  private method maneuverMotorBoat(thisBoat type class of motorBoat)
    invoke start, turnLeft, turnRight, stop
  endmethod

  private method maneuverSailBoat(thisBoat type class of sailBoat)
    invoke start, turnLeft, turnRight, stop
  endmethod
endclass


```


### Improved Marina Implementation (Using Polymorphism)


``` PSEUDO

class marina
  public method launchMotorBoat
    thisMotorBoat type class of motorBoat
    create new instance of motorBoat into thisMotorBoat
    call method maneuverBoat(thisMotorBoat)
  endmethod

  public method launchSailBoat
    thisSailBoat type class of sailBoat
    create new instance of sailBoat into thisSailBoat
    call method maneuverBoat(thisSailBoat)
  endmethod

  private method maneuverBoat(thisBoat type class of boat)
    invoke start, turnLeft, turnRight, stop
  endmethod
endclass


```


# Eliminating Conditional Logic with Polymorphism

## Procedural Approach (Using Conditional Logic)
Procedural code often relies on **conditional statements** to determine behavior based on type.  
Example: Maneuvering boats using `CASE` statements.

### Listing 6-6: Procedural Subroutines
```pseudo
form start
  case boat_type
    when motor_boat
      engage propeller
    when sail_boat
      raise sail
  endcase
endform

form turn_left
  case boat_type
    when motor_boat
      rotate steering wheel counterclockwise
    when sail_boat
      push tiller to right
  endcase
endform

form turn_right
  case boat_type
    when motor_boat
      rotate steering wheel clockwise
    when sail_boat
      push tiller to left
  endcase
endform

form stop
  case boat_type
    when motor_boat
      disengage propeller
    when sail_boat
      lower sail
  endcase
endform

```


``` PSEUDO


form start
  case boat_type
    when motor_boat
      engage propeller
    when sail_boat
      raise sail
    when row_boat
      pull both oars
  endcase
endform

form turn_left
  case boat_type
    when motor_boat
      rotate steering wheel counterclockwise
    when sail_boat
      push tiller to right
    when row_boat
      pull right oar while dragging left oar
  endcase
endform

form turn_right
  case boat_type
    when motor_boat
      rotate steering wheel clockwise
    when sail_boat
      push tiller to left
    when row_boat
      pull left oar while dragging right oar
  endcase
endform

form stop
  case boat_type
    when motor_boat
      disengage propeller
    when sail_boat
      lower sail
    when row_boat
      push both oars
  endcase
endform


```


``` PSEUDO

class rowBoat inherits from boat
  public method start
    pull both oars
  endmethod

  public method turnLeft
    push right oar while dragging left oar
  endmethod

  public method turnRight
    push left oar while dragging right oar
  endmethod

  public method stop
    push both oars
  endmethod
endclass


```


Benefits:

No conditional logic required.
All new code is contained in one class.
Easier maintenance and testing.


Real-World Example: Seven Seas Forwarding Company
Procedural approach uses cascade conditions for tasks like:

Determining language at receiving port.
Calculating gross weight unit.



``` ABAP
if receivingPort is "Melbourne" or "New Orleans"
  paperworkLanguage = "English"
else if receivingPort is "Le Havre" or "Majunga"
  paperworkLanguage = "French"
else if receivingPort is "Santos" or "Lisbon"
  paperworkLanguage = "Portuguese"
...
execute printPaperwork(paperworkLanguage)


if receivingCountry is "United States" or "Liberia"
  grossWeightUnit = "pound"
else if receivingCountry is "Myanmar"
  grossWeightUnit = "peittha"
else
  grossWeightUnit = "kilogram"

execute calculateGrossWeight(grossWeightUnit)


```



## Instead of scattered conditions, define an abstract class and let subclasses handle specifics.

``` ABAP


CLASS destination_port DEFINITION.
  PUBLIC SECTION.
    METHODS:
      print_paperwork ABSTRACT
        IMPORTING target_language TYPE language,
      calculate_gross_weight ABSTRACT
        IMPORTING weight TYPE quantity
                  gross_weight_unit TYPE weight_unit
        EXPORTING gross_weight TYPE quantity.
ENDCLASS.

CLASS destination_port_new_orleans DEFINITION
  INHERITING FROM destination_port.
  PUBLIC SECTION.
    METHODS:
      print_paperwork REDEFINITION,
      calculate_gross_weight REDEFINITION.
  PRIVATE SECTION.
    CONSTANTS:
      gross_weight_unit TYPE mass_unit VALUE 'pound',
      paperwork_language TYPE language VALUE 'English'.
ENDCLASS.



```


## Key Advantage:
### Once the correct subclass is instantiated, no conditional logic is needed for determining language, weight unit, tariffs, etc.

### Why Polymorphism Eliminates Conditional Logic

### Procedural approach → scattered CASE or IF statements.
### OOP approach → encapsulates behavior in subclasses.
### Maintenance becomes easier, code remains clean and extensible.



# ABAP Language Support for Polymorphism

## How ABAP Supports Polymorphism
The object-oriented extensions to ABAP accommodate polymorphism in the following ways:
- ✅ **Dynamic Polymorphism (Dynamic Dispatch)**  
  Occurs when a method call is resolved at runtime based on the **dynamic type** of the object.
- ✅ **Abstract Methods**  
  Allows defining method signatures in abstract classes without implementation.
- ✅ **Redefinition of Inherited Methods**  
  Subclasses can override inherited methods using `REDEFINITION`.

> There are no specific ABAP statements for polymorphism.  
It occurs naturally when:
- A subclass provides its own implementation for inherited methods.
- An instance of the subclass is referenced through a variable of the superclass type.

---

## Key Points
- ABAP **does not support static polymorphism** (method overloading).
- Dynamic polymorphism is achieved via:
  ```abap
  METHODS method_name REDEFINITION.
 

Abstract classes and interfaces enable polymorphic behavior.


Why Polymorphism Matters

Eliminates scattered conditional logic.
Simplifies maintenance by encapsulating behavior in subclasses.
Supports case-less programming (Horst Keller & Sascha Krüger).


Summary

Two kinds of polymorphism: Static and Dynamic.
ABAP supports only dynamic polymorphism through dynamic dispatch.
Major benefit: reduces conditional logic, making code easier to maintain and extend.
