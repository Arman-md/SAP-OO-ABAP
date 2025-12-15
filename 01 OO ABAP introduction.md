# CLASS - Is a template

``` abap

CLASS zcl_am_test_oo DEFINITION
  PUBLIC
  FINAL
  CREATE PUBLIC .

  PUBLIC SECTION.
  PROTECTED SECTION.
  PRIVATE SECTION.
ENDCLASS.

CLASS zcl_am_test_oo IMPLEMENTATION.
ENDCLASS.



```


## What each keyword/section means

### 

CLASS ... DEFINITION
Declares the class interface (its shape). This is where you define:

Attributes (data members)
Methods (signatures only)
Interfaces
Aliases
Friends
Events

PUBLIC : The class itself is visible to all consumers in the system. (Opposed to PRIVATE classes declared inside another class or local to programs.)
FINAL : Prevents inheritance. No one can create a subclass of this class.

Use when: You want to guarantee behavior isn’t extended/overridden (e.g., utility classes, helpers).
Don’t use if: You expect others to enhance/extend via subclassing.
CREATE PUBLIC
Controls instantiation visibility:

CREATE PUBLIC → NEW zcl_am_test_oo( ) is allowed everywhere.
CREATE PROTECTED → Only subclasses (and friends) can instantiate.
CREATE PRIVATE → Only the class itself (and friends) can instantiate (use with factory methods).


#### ⚠️ Common pitfall: Developers sometimes mark a class FINAL but forget they still can control instantiation with CREATE PRIVATE and expose a factory method instead.


## Visibility sections

### PUBLIC SECTION.
Anything declared here is visible to all consumers:

Public methods
Public constants/types
Public attributes (usually avoid mutable public attributes—prefer getter/setter or read-only access)

### PROTECTED SECTION.
Visible to the class and subclasses (and friends).
Typical use: Template method pattern hooks, reusable helper methods for subclasses.

### PRIVATE SECTION.
Visible only within the class.
Put implementation details here: internal attributes, helper methods, caches.

Let’s understand Object-Oriented ABAP (OO ABAP) vs Procedural ABAP using a real-life example — something simple and relatable:

🛒 Scenario: Online Shopping System
Imagine you're building a system for an online store. You need to manage orders, customers, and products.

🧱 Procedural ABAP Approach
In procedural programming, you’d write separate routines (FORMs or function modules) like:

FORM create_order
FORM calculate_total
FORM print_invoice

Each routine handles a specific task, and data is passed around manually.

🔧 Example:

``` abap

DATA: v_price TYPE p,
      v_quantity TYPE i,
      v_total TYPE p.

v_price = 100.
v_quantity = 2.

PERFORM calculate_total.

FORM calculate_total.
  v_total = v_price * v_quantity.
ENDFORM.



```

Here, everything is global and loosely connected. If you want to add discounts or taxes, you’ll need to modify multiple routines.

🧠 OO ABAP Approach
In OO ABAP, you think in terms of objects — like a Customer, Order, or Product. Each object has attributes (data) and methods (behavior).

🔧 Example:

``` abap

CLASS lcl_order DEFINITION.
  PUBLIC SECTION.
    METHODS: calculate_total,
             set_details.
    DATA: price TYPE p,
          quantity TYPE i,
          total TYPE p.
ENDCLASS.

CLASS lcl_order IMPLEMENTATION.
  METHOD set_details.
    price = 100.
    quantity = 2.
  ENDMETHOD.

  METHOD calculate_total.
    total = price * quantity.
  ENDMETHOD.
ENDCLASS.

DATA(lo_order) = NEW lcl_order( ).
lo_order->set_details( ).
lo_order->calculate_total( ).


```

Now, the order object knows how to calculate its own total. You can easily extend it with discounts, taxes, or shipping logic — all encapsulated inside the class.

🎯 Real-Life Analogy
Imagine you're managing a car:

Procedural: You manually control each part — engine, brakes, lights — with separate switches and wires.

OO: You have a Car object. You just call car->start() or car->brake(). Internally, it knows how to handle everything.


✅ Benefits of OO ABAP

Encapsulation: Keeps data and logic together.
Reusability: You can reuse classes across projects.
Maintainability: Easier to update and debug.
Scalability: Ideal for large applications like Fiori, RAP, and BTP.


## Object-Oriented Design with ABAP A Practical Approach James E. McDonough

### 
• Encapsulation
• Abstraction
• Inheritance
• Polymorphism


<img width="835" height="631" alt="image" src="https://github.com/user-attachments/assets/3e5531bf-9bcd-416c-bb7d-13d4fd212861" />







