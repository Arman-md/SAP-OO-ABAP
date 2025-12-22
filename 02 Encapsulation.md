## Separation of Concerns

Encapsulation is a technique used to facilitate modularizing code in pursuit of the design principle known
as separation of concerns.

## Visibility

<img width="802" height="376" alt="image" src="https://github.com/user-attachments/assets/436d2533-775b-4dea-9f3d-719cefbac57b" />


<img width="819" height="243" alt="image" src="https://github.com/user-attachments/assets/37760231-bc88-4025-aeae-961705add027" />


### • Variables should be defined as local method variables unless there is a compelling reason for them to be defined as attributes of the class.


### • Class members should be assigned private visibility unless there is a compelling reason for the visibility to be set to a wider visibility level.

### a QUICK BROWN FOX JUMPS OVER A LAZY DOG

<img width="738" height="218" alt="image" src="https://github.com/user-attachments/assets/ae9d546b-9757-4e17-9b47-9e39479712a7" />


## The Encapsulation Unit

### Instance Encapsulation Units

-> We can define a class such that every one of its members belongs to the instance realm; that is, none of
its members are marked as static.


### Static Encapsulation Units
-> We can define a class such that every one of its members belongs to the static realm; that is, each member
is marked as static. This constitutes a static class.

### Hybrid Encapsulation Units
-> We can define a class such that some of its members belong to the instance realm while other members
belong to the static realm. This constitutes a hybrid class



# Constructors, Destructors & Friendship in OOP

## ✅ Constructors
- **Purpose**: Initialize attributes when creating a class or object.
- **Types**:
  - **Instance Constructor**:
    - Invoked automatically when creating an object.
    - Runs **once per object**.
    - Can have parameters (method signature).
    - Accesses both **static and instance members**.
  - **Static Constructor**:
    - Invoked automatically when the class is first accessed (static member or first instance).
    - Runs **once per class**.
    - No parameters allowed.
    - Accesses **only static members**.
    - Executes **before** the first instance constructor.

## ✅ Destructors
- **Purpose**: Cleanup resources during destruction.
- **Instance Destructor**:
  - Invoked automatically when an object is destroyed.
  - Common in languages supporting **RAII** (e.g., C++).
  - Not supported in **Java** or **ABAP** (use Dispose pattern instead).
- **Static Destructor**:
  - Invoked when static members are destroyed.
  - Rarely supported (C++, C#, Java, ABAP **do not** support).

## ✅ Language Support
- **Instance Constructors**: Supported in most OOP languages.
- **Static Constructors**: Supported in **C#** and **ABAP**; not in C++ or Java (Java uses static blocks).
- **Instance Destructors**: Supported in C++ (RAII); not in Java/ABAP.
- **Static Destructors**: Generally **not supported**.

## ✅ Friendship
- **Definition**: Allows one class to grant another unrestricted access to its members.
- **Supported in**: C++ and ABAP.
- **Characteristics**:
  - Friendship is **offered**, not reciprocal.
  - Breaks **encapsulation** (friends can access private/protected members).
  - Makes **maintenance/refactoring harder** (private changes can break friend classes).
- **Best Practice**: Use **with caution**; many OOP experts discourage it.

---

### ⚠️ Key Takeaways
- Constructors initialize; destructors clean up.
- Static constructors run once per class; instance constructors run once per object.
- Destructors are rare in garbage-collected environments (Java, ABAP).
- Friendship breaks encapsulation and complicates maintenance.




# ✅ Effective Use of Encapsulation in OOP (ABAP Focus)

## 🔍 Guidelines for Encapsulation
- **Encapsulate Repetition**  
  - Write code once and reuse it (methods or classes).
  - Example: A method called by multiple methods within the same class.

- **Encapsulate Complexity**  
  - Move long or complex algorithms into separate methods or classes.
  - Improves readability and maintainability.

- **Encapsulate What Is Likely to Vary**  
  - Separate processes that are likely to change (e.g., business rules, pricing logic).
  - Example: Pizza ordering system → menu items and promotions change frequently.

- **Single Responsibility Principle (SRP)**  
  - Each encapsulation unit (method/class) should have **one reason to change**.
  - Example:
    - Method A: Set print parameters.
    - Method B: Issue print request.
    - Avoid combining both in one method.

---

## 🔍 ABAP Language Support for Encapsulation
- Supports **classes with attributes and methods**.
- Visibility control: `PUBLIC`, `PROTECTED`, `PRIVATE` sections.
- Method variables and signatures supported.
- Instance and static members allowed.
- Supports **instance classes**, **static classes**, and **hybrid classes**.
- Supports **instance and static constructors**.
- Friendship between classes (use with caution).

### ABAP Class Syntax


- **Definition** and **Implementation** are separate:
  ```abap
  CLASS class_name DEFINITION.
    PUBLIC SECTION.
      METHODS: method_name IMPORTING param TYPE type.
    PRIVATE SECTION.
      DATA: attribute TYPE type      DATA: attribute TYPE type.
  ENDCLASS.

  CLASS class_name IMPLEMENTATION.
    METHOD method_name.
      " Implementation logic
    ENDMETHOD.



# ✅ ABAP Object Access: Instance vs Static Classes

## 🔍 Object Reference and Instance Access
- **Object Reference Variable**:
  - Example:  
    ```abap
    DATA rental_car TYPE REF TO car.
    CREATE OBJECT rental_car.
    ```
  - `CREATE OBJECT` → runtime creates an object in memory and assigns its reference to `rental_car`.

- **Accessing Instance Methods**:
  - Syntax:
    ```abap
    CALL METHOD rental_car->set_year
      EXPORTING year = '2014'.
    ```
  - `->` = **Object Component Selector** (used for instance members).
  - `rental_car` = reference variable, `set_year` = public method.

---

## 🔍 Static Classes in ABAP
- **Definition**:
  - Use `CLASS-METHODS` and `CLASS-DATA` for static members.
  - Example:
    ```abap
    CLASS car DEFINITION.
      PUBLIC SECTION.
        CLASS-METHODS: get_year EXPORTING year TYPE string,
                       set_year IMPORTING year TYPE string.
      PRIVATE SECTION.
        CLASS-DATA: model_year TYPE string.
    ENDCLASS.
    ```
- **Characteristics**:
  - No instantiation required (`CREATE OBJECT` not applicable).
  - Access via **class name** and `=>` (Class Component Selector):
    ```abap
    CALL METHOD car=>set_year
      EXPORTING year = '2014'.
    ```
- **Static Class Guarantee**:
  - Use qualifiers:
    ```abap
    CLASS class_name DEFINITION ABSTRACT FINAL.
    ```
  - `ABSTRACT` → cannot instantiate.
  - `FINAL` → cannot subclass.
  - Together ensure class is **static-only**.

---

## 🔍 Hybrid Classes (Static + Instance Members)
- ABAP supports **hybrid classes**:
  - Mix of `CLASS-DATA` / `CLASS-METHODS` (static) and `DATA` / `METHODS` (instance).
- Example:
    ```abap
    CLASS car DEFINITION.
      PUBLIC SECTION.
        CLASS-METHODS: class_constructor,
                       get_next_serial_number EXPORTING next_serial_number TYPE i.
        METHODS: constructor,
                 get_year EXPORTING year TYPE string,
                 set_year IMPORTING year TYPE string.
      PRIVATE SECTION.
        CLASS-DATA: last_used_serial_number TYPE i.
        DATA: serial_number TYPE i,
              model_year TYPE string.
    ENDCLASS.
    ```

---

## 🔍 Constructors in ABAP
- **Static Constructor**:
  - Name: `class_constructor`.
  - Declared in `CLASS-METHODS` (public section).
  - No signature allowed.
  - Invoked automatically when class is first accessed.
  - Used for initializing static attributes.
- **Instance Constructor**:
  - Name: `constructor`.
  - Declared in `METHODS` section.
  - May have a signature.
  - Invoked automatically when an object is created.
- Example:
    ```abap
    METHOD class_constructor.
      last_used_serial_number = 1000.
    ENDMETHOD.

    METHOD constructor.
      CALL METHOD get_next_serial_number
        IMPORTING next_serial_number = serial_number.
    ENDMETHOD.
    ```

---

## ✅ Key Syntax Differences
- **Instance Access**: `object_ref->method_name`.
- **Static Access**: `class_name=>method_name`.
- **Static Class Guarantee**: `ABSTRACT FINAL` in class definition.
- **Hybrid Classes**: Combine static and instance members.
- **Constructors**:
  - `class_constructor` → static setup.
  - `constructor` → instance setup.

---

### ⚠️ Best Practices
- Use **static constructors** for initializing static data.
- Use **instance constructors** for per-object initialization.
- Apply `ABSTRACT FINAL` for classes intended to be static-only.
- Keep




# ✅ ABAP Instance Constructor, Object Destruction & Friendship

## 🔍 Instance Constructor Behavior
- Invoked **each time a new instance is created**.
- Example from `car` class:
  - `constructor` calls `get_next_serial_number` (a **static method**).
  - `get_next_serial_number`:
    - Increments static attribute `last_used_serial_number`.
    - Returns updated value to assign a **unique serial number** to each new instance.
- **Key Point**:  
  - Static attributes are **shared across all instances**.
  - Ensures uniqueness for values like serial numbers.

---


## 🔍 Object Destruction in ABAP
- **No explicit destructors** in ABAP.
- To destroy an object:
  ```abap
  CLEAR object_ref.


  



