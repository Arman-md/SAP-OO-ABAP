
# 🏰 Journey to Objectropolis: From Abstraction to Inheritance

## 📌 Context
We move from **Abstraction** to **Inheritance**, exploring relationships between classes at different abstraction levels.

---

## 🔍 Classes and Their Members (Table 5-1)

| **Classes**                          | **Attributes**                              | **Behaviors**                                      |
|--------------------------------------|--------------------------------------------|----------------------------------------------------|
| **Enclosed shape**                  | `area`, `perimeter`                       | `getArea`, `getPerimeter`                         |
| **Enclosed shape with at least one angle** | `area`, `perimeter`, `smallest angle`     | `getArea`, `getPerimeter`, `getSmallestAngle`     |
| **Rectangle**                       | `area`, `perimeter`, `smallest angle`, `hypotenuse` | `getArea`, `getPerimeter`, `getSmallestAngle`, `getHypotenuse` |

---

## ✅ Key Observations
- All three classes have a **`getArea`** behavior → Each class currently has its own implementation.
- **Rectangle** is a specialization of **Enclosed shape with at least one angle**, and that class **is an Enclosed shape**.
- This creates an **“is-a” relationship**:
  - `Rectangle` **is an** `Enclosed shape with at least one angle`.
  - `Enclosed shape with at least one angle` **is an** `Enclosed shape`.

---

## 💡 Insight
- The implementation of `getArea` in **Enclosed shape** works for both **Rectangle** and **Enclosed shape with at least one angle**.
- Instead of writing unique implementations for each class:
  - **Copy the implementation** from the general class to the specific classes.
- Same applies to **attributes**:
  - Copy `area` and `perimeter` from **Enclosed shape** to other classes unchanged.

---

## 🎯 Benefit
- **Huge reduction in workload**:
  - No need to write code from scratch.
  - Reuse implementations wherever an **“is-a” relationship** exists.
- This concept stems from **Abstraction** and its aspect of **levels of abstraction**.

---

## 🌟 Core Concept
> Anytime we have an **“is-a” relationship** between two classes, we can reuse:
> - **Attributes** from the general class.
> - **Method implementations** from the general class.



# 🌐 Journey to Objectropolis: Inheritance

## 📌 Concept
Designers of object-oriented principles introduced **inheritance** to eliminate the need for copying implementation code between classes related via an **“is-a”** relationship. Instead of replicating code, programmers indicate this relationship, and the language environment makes members of the general class available to the specific class.

---

## 🔑 What is Inheritance?
- **Inheritance** enables a class to have members not defined within itself.
- A class can **reuse functionality** from other classes.
- This creates a **class hierarchy**, where classes inherit from others.

---

## 🏗 Class Hierarchy
- Classes are arranged vertically by abstraction level:
  - Higher classes → broader scope.
  - Lower classes → more detail.
- Connecting lines denote inheritance.
- Example:
  - `Rectangle` inherits from `Enclosed shape with at least one angle`.
  - `Enclosed shape with at least one angle` inherits from `Enclosed shape`.

### ✅ Benefits:
- Attributes like `area` and `perimeter` can be defined **only once** in `Enclosed shape`.
- Behaviors like `getArea` and `getPerimeter` also defined once and inherited.
- `Rectangle` now only needs to implement `getHypotenuse`.

---

## 🔍 Terminology (Table 5-2)
| **Superclass** (offers inheritance) | **Subclass** (inherits) |
|--------------------------------------|---------------------------|
| Base class                          | Derived class            |
| Superclass                          | Subclass                |

- **ABAP** uses **Superclass/Subclass** terminology.
- C++ uses **Base/Derived class**.
- Many languages have a **root base class**:
  - ABAP, Java, C#: `object`
  - Objective-C: `NSObject`
  - C++: No root base class.

---

## ⚠ Important Distinction
- **Child class** knows its parent (must declare inheritance).
- **Parent class** does **not** know its children.
- Parent should never assume existence of specific child classes.

---

## 🔗 Paths of Inheritance
- No limit to hierarchy depth.
- Each descendant acquires **all attributes and behaviors** of ancestor classes.

---

## 📊 Examples of Hierarchies
### Shapes:
- `Rectangle` → `Enclosed shape with at least one angle` → `Enclosed shape`

!Shape Hierarchy

### Student Employee:
- `StudentEmployee` → inherits from both `Student` and `Employee`

![Student Employee Hierrchy

---

## 🧩 Types of Inheritance
### ✅ Single Inheritance
- Each class has **one direct ancestor**.
- Example: `Rectangle` inherits from `Enclosed shape with at least one angle`.

### ✅ Multiple Inheritance
- A class has **more than one direct ancestor**.
- Example: `StudentEmployee` inherits from both `Student` and `Employee`.

---

## 🔄 Overriding Inherited Behaviors
- A subclass can **override** an inherited method.
- Override means:
  - Replace parent’s implementation with a new one.
  - Must keep the **same method signature**.

---

## 🌟 Core Takeaways
- Inheritance reduces duplication.
- Enables **reuse**, **hierarchies**, and **polymorphism**.
- Supports **method overriding** for flexibility.



# 🧭 Objectropolis Notes: Inheritance, Overriding, Visibility, Constructors & Casting

> **Goal:** Preserve every important point from your notes in clean GitHub-flavored Markdown.

---

## 🧠 Inheritance: The Language Feature That Replaces Copy-Paste

- Object-oriented languages provide **inheritance** so a subclass **implicitly gains** members from its superclass without copying code.
- A class indicates it **inherits** from other classes; the language runtime makes **general-class** members available to the **more-specific** class.
- Inheritance creates a **class hierarchy** (levels of abstraction from general → specific).

---

## 🏗 Class Hierarchy Basics

- Classes are arranged vertically (more general at the top, more specific at the bottom).
- The **connecting line** between classes denotes **“inherits from”**.
- Example (shapes):
  - `Rectangle` **inherits from** `Enclosed shape with at least one angle`.
  - `Enclosed shape with at least one angle` **inherits from** `Enclosed shape`.
- **Attributes** `area` and `perimeter` can be defined **once** in `Enclosed shape` and **inherited** downstream.
- **Behaviors** `getArea` and `getPerimeter` can be defined **once** in `Enclosed shape` and **inherited** downstream.

### Diagrams
![hape Hierarchy
![Shape &Student Employee Hierarchies

---

## 🏷 Terminology (Pairs)

- **Superclass / Subclass** (ABAP commonly uses these).
- **Base class / Derived class** (C++ usage).
- Many languages have a **root base class**:
  - C#, Java, ABAP: `object`
  - Objective-C: `NSObject`
  - C++: **no** universal root base class.

> A **child** knows (declares) its **parents**; a **parent** knows **nothing** about its children and must not assume any child class exists when implementing its behaviors.

---

## 🔁 Paths & Depth of Inheritance

- There is essentially **no limit** to depth.
- A class at the bottom inherits **all attributes & behaviors** from **all ancestor paths** leading to it.
- **Single inheritance**: one direct parent per class (e.g., `Rectangle`).
- **Multiple inheritance**: more than one direct parent (e.g., `StudentEmployee` inherits from both `Student` and `Employee`).

---

## 🔧 Method Overriding

- **Only instance methods** can be **overridden**.
- **Static methods** can be **inherited** but **not overridden**.
- Example (optimization):
  - Base `Enclosed shape.getArea` is complex.
  - `Rectangle` overrides `getArea` with simple `height × width`.
- **Signature must not change** when overriding—only the implementation changes.

### Override + Use Parent (super/base) Pattern

- A child may **override** and still **invoke the parent implementation**:
  - Example: `Hollow Rectangle.getArea`:
    1. Compute inner shape area.
    2. **Invoke parent** (`super`) `getArea` for outer rectangle.
    3. Subtract inner area from outer area.

> **Qualifiers to call parent**: `super` (Java, ABAP), `base` (C#), class-qualified call (C++).

---

## 🧩 Abstract Methods & Classes

- A parent may define a **method signature without implementation** → **abstract method**.
- A class with abstract methods must be **marked abstract** and **cannot be instantiated**.
- Child classes **must** provide implementations for inherited abstract methods.

---

## 🚫 Controlling Inheritance

- **Final method**: cannot be overridden in child classes.
- **Final class**: cannot be used as a parent (no subclasses).

---

## 👀 Effect on Member Visibility

- **Protected** visibility: visible to the class and its **child classes** (direct/indirect).
- **Private** in parent: **not visible** to child classes.
- Common practice: **public behaviors** with **private & protected attributes** (i.e., encapsulation across inheritance).

---

## 🏗 Constructors in Inheritance

### Static Constructors
- Invoked **automatically on first access** to a class.
- Executed from **most generalized** → **most specialized** across the hierarchy that hasn’t been accessed yet.
- Example order for first access to `dachshund`:
  - `animal` → `mammal` → `canine` → `domesticPet` → `dog` → `dachshund`.
- If a class was already accessed earlier, its static constructor is **not re-run**.

### Instance Constructors
- Executed when an object is **created**.
- **Order differs by language**:
  - Some require **child first calls parent immediately** (C++, Java).
  - ABAP allows **child to do some work before invoking parent** constructors, but **must invoke them eventually**.
- Until parent constructors have been invoked:
  - Access in the constructor is **restricted** (no instance attributes/methods; only static members, parameters, locals).

### Animal/Canine/Fox/Dog Example

- Attributes & behaviors across classes (sample):

  | Class        | Attributes                                              | Behaviors                                 |
  |--------------|----------------------------------------------------------|-------------------------------------------|
  | `animal`     | height, weight, age, **alacrity**                        | eat, sleep, speak                          |
  | `mammal`     | —                                                        | **nurseOffspring**                         |
  | `canine`     | **furColor**                                             | run, jump, followScentTrail                |
  | `domesticPet`| petName, ownerName, lastVeterinarianVisit               | visitVeterinarian, get/setPetName          |
  | `dog`        | —                                                        | chaseCat, fetch                            |
  | `fox`        | —                                                        | raidChickenCoop                            |

- Constructors (example):
  - `animal`: instance constructor to set **alacrity**.
  - `canine`: instance constructor to set **furColor**.
  - `fox`, `dog`, `mammal`: **no explicit** instance constructors (implicit ones chain up).

- Pseudocode usage:



## ✅ Example: Object Creation & Constructor Chain

```text
create object fox("brown","quick")
create object dog(" ","lazy")
fox.jump(dog)



# 🔍 ABAP Language Support for Inheritance

ABAP’s object-oriented extensions support inheritance in the following ways:

---

## ✅ Key Features
- Provides a **root base class**: `object` (all classes implicitly inherit from it).
- Supports **single inheritance** (one immediate parent class).
- Offers **protected visibility** for members accessible only to parent and child classes.
- Ensures **constructor chaining** across the hierarchy in proper sequence.
- Allows **method overriding** (instance methods only).
- Enables overriding methods to **invoke parent implementation** via `super`.
- Supports **final** classes and methods (cannot be inherited or overridden).
- Supports **abstract** classes and methods (must be implemented by subclasses).
- Allows **generalizing and specializing casting assignments**.

---

## ✅ Syntax for Inheritance
```abap
CLASS child_class DEFINITION INHERITING FROM parent_class [options].
  PUBLIC SECTION.
    " Methods, attributes
  PROTECTED SECTION.
    " Members visible to parent and child classes
ENDCLASS.

CLASS child_class IMPLEMENTATION.
  " Method implementations
ENDCLASS.


```



# 📘 ABAP Inheritance — Complete Notes & Code (Markdown)

This document consolidates ABAP inheritance notes into a single **GitHub-flavored Markdown** file with explanatory text and **ABAP snippets**. Paste directly into `README.md`.

---

## 🔍 ABAP Language Support for Inheritance

ABAP’s object-oriented extensions support inheritance in the following ways:

- Root base class: **`object`** (all global classes implicitly inherit from it).
- **Single inheritance** (each class can inherit from one parent).
- **Protected visibility** for members intended for parent + child classes.
- Proper **constructor chaining** enforced by runtime.
- **Method overriding** (instance methods only).
- Overriding methods can call **parent implementation** via `super`.
- **Final** methods/classes (no overriding / no subclassing).
- **Abstract** methods/classes (no instantiation; subclasses must implement).
- **Casting** supported for both **generalizing** (child→parent) and **specializing** (parent→child) moves.

---

## 🧩 Basic Inheritance Syntax

```abap
CLASS child_class DEFINITION INHERITING FROM parent_class.
  PUBLIC SECTION.
    " Public methods/attributes
  PROTECTED SECTION.
    " Inheritable members (visible to this and children)
  PRIVATE SECTION.
    " Private members (visible only in this class)
ENDCLASS.

CLASS child_class IMPLEMENTATION.
  " Implementations here
ENDCLASS.


## 🔐 Visibility for Inheritance
CLASS parent_class DEFINITION.
  PUBLIC SECTION.
    METHODS do_public.
  PROTECTED SECTION.
    DATA mv_counter TYPE i.      " visible to parent and children
    METHODS do_inheritable.      " overridable in children
  PRIVATE SECTION.
    DATA mv_secret  TYPE string. " not visible to child classes
ENDCLASS.


## 🔗 Constructor Chaining


CLASS zcl_parent DEFINITION.
  PUBLIC SECTION.
    METHODS constructor IMPORTING iv_init TYPE i.
    METHODS get_value RETURNING VALUE(rv) TYPE i.
  PROTECTED SECTION.
    DATA mv_value TYPE i.
ENDCLASS.

CLASS zcl_parent IMPLEMENTATION.
  METHOD constructor.
    mv_value = iv_init.
  ENDMETHOD.
  METHOD get_value.
    rv = mv_value.
  ENDMETHOD.
ENDCLASS.

CLASS zcl_child DEFINITION INHERITING FROM zcl_parent.
  PUBLIC SECTION.
    METHODS constructor IMPORTING iv_init TYPE i iv_bonus TYPE i.
ENDCLASS.

CLASS zcl_child IMPLEMENTATION.
  METHOD constructor.
    " Not allowed yet: mv_value (instance) is not available before super call
    CALL METHOD super->constructor EXPORTING iv_init = iv_init.
    " Now instance members are available
    mv_value = mv_value + iv_bonus.
  ENDMETHOD.
ENDCLASS.


## 🔄 Method Overriding (with Optional Parent Call)


CLASS zcl_parent2 DEFINITION.
  PUBLIC SECTION.
    METHODS action.
  PROTECTED SECTION.
    METHODS hook REDEFINITION.
ENDCLASS.

CLASS zcl_parent2 IMPLEMENTATION.
  METHOD action.
    " Template Method: call hook for customization
    me->hook( ).
  ENDMETHOD.
  METHOD hook.
    " Default (possibly empty)
  ENDMETHOD.
ENDCLASS.

CLASS zcl_child2 DEFINITION INHERITING FROM zcl_parent2.
  PROTECTED SECTION.
    METHODS hook REDEFINITION.
ENDCLASS.

CLASS zcl_child2 IMPLEMENTATION.
  METHOD hook.
    " Optional: call parent version first
    CALL METHOD super->hook.
    " Child-specific behavior
  ENDMETHOD.
ENDCLASS.

### ---> Overriding applies to instance methods only. Static methods can be inherited but not overridden.


## Restricting Inheritance & Overriding




Final Class (No Subclassing)

CLASS zcl_no_children DEFINITION FINAL.
  PUBLIC SECTION.
    METHODS run.
ENDCLASS.


Final Method (No Overriding)


CLASS zcl_stable_api DEFINITION.
  PUBLIC SECTION.
    METHODS compute FINAL.
ENDCLASS.

## ABSTRACT 


CLASS zcl_shape DEFINITION ABSTRACT.
  PUBLIC SECTION.
    METHODS get_area       RETURNING VALUE(rv_area) TYPE decfloat34 ABSTRACT.
    METHODS get_perimeter  RETURNING VALUE(rv_per)  TYPE decfloat34 ABSTRACT.
  PROTECTED SECTION.
    DATA mv_color TYPE string.
ENDCLASS.

" Must implement abstract methods
CLASS zcl_rectangle DEFINITION INHERITING FROM zcl_shape.
  PUBLIC SECTION.
    METHODS constructor IMPORTING iv_w TYPE decfloat34 iv_h TYPE decfloat34.
    METHODS get_area      REDEFINITION.
    METHODS get_perimeter REDEFINITION.
  PRIVATE SECTION.
    DATA mv_w TYPE decfloat34.
    DATA mv_h TYPE decfloat34.
ENDCLASS.

CLASS zcl_rectangle IMPLEMENTATION.
  METHOD constructor.
    CALL METHOD super->constructor. " if parent defines one later
    mv_w = iv_w.
    mv_h = iv_h.
  ENDMETHOD.
  METHOD get_area.
    rv_area = mv_w * mv_h.
  ENDMETHOD.
  METHOD get_perimeter.
    rv_per = 2 * ( mv_w + mv_h ).
  ENDMETHOD.
ENDCLASS.


## 🧠 Overriding With Parent-Logic Reuse (Hollow Rectangle)


CLASS zcl_hollow_rectangle DEFINITION INHERITING FROM zcl_rectangle.
  PUBLIC SECTION.
    METHODS constructor
      IMPORTING
        iv_w_outer TYPE decfloat34
        iv_h_outer TYPE decfloat34
        iv_w_inner TYPE decfloat34
        iv_h_inner TYPE decfloat34.
    METHODS get_area REDEFINITION.
  PRIVATE SECTION.
    DATA mv_wi TYPE decfloat34.
    DATA mv_hi TYPE decfloat34.
ENDCLASS.

CLASS zcl_hollow_rectangle IMPLEMENTATION.
  METHOD constructor.
    " Outer dims go to parent
    CALL METHOD super->constructor
      EXPORTING iv_w = iv_w_outer iv_h = iv_h_outer.
    mv_wi = iv_w_inner.
    mv_hi = iv_h_inner.
  ENDMETHOD.

  METHOD get_area.
    " Inner area
    DATA(lv_inner) = mv_wi * mv_hi.
    " Use parent area for outer rectangle
    DATA(lv_outer) = super->get_area( ).
    rv_area = lv_outer - lv_inner.
  ENDMETHOD.
ENDCLASS.


