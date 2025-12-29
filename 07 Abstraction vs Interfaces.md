
# Abstract Classes vs Interfaces in ABAP OO  
**Why both exist, their major differences, objectives, and practical examples**

---

## ✅ Why Do We Have Both?
Both **abstract classes** and **interfaces** enable polymorphism in ABAP OO, but they serve different design purposes:

- **Abstract Classes**: Provide a base structure and allow partial implementation of methods.
- **Interfaces**: Define a pure contract (method signatures only) without any implementation.

---

## 🔍 Major Differences Between Abstract Classes and Interfaces

| Feature                | Abstract Class                              | Interface                                  |
|------------------------|--------------------------------------------|-------------------------------------------|
| **Purpose**           | Share common behavior + enforce contract  | Define capability contract only           |
| **Contains**          | Attributes, constants, implemented methods, and abstract methods | Only method signatures, types, constants |
| **Implementation**    | Can provide default logic for some methods | No implementation at all                 |
| **Inheritance**       | Single inheritance (one superclass only)   | Multiple interfaces can be implemented   |
| **Polymorphism**      | Achieved via superclass reference          | Achieved via interface reference         |
| **State**             | Can hold state (attributes)                | Cannot hold state (except constants)     |
| **Use Case**          | When classes share common logic and structure | When classes share only behavior contract |
| **Flexibility**       | Less flexible (due to single inheritance)  | Highly flexible (multiple interfaces)    |

---

## ✅ Objective in OO ABAP
- **Abstract Class**:
  - Used when you want to **reuse code** and enforce a common structure.
  - Example: `ZCL_VEHICLE` with implemented methods like `start_engine` and abstract methods like `move`.
- **Interface**:
  - Used when you want to **define capabilities** without dictating implementation.
  - Example: `IF_MANEUVERABLE` for `start`, `turn_left`, `turn_right`, `stop`.

---

## 🔑 Design Principle
- Use **abstract classes** for **is-a** relationships with shared logic.
- Use **interfaces** for **can-do** capabilities (e.g., Serializable, FuelConsumable, Maneuverable).

---

## ✅ ABAP Example: Combining Both

```abap
" Abstract Class
CLASS zcl_vehicle DEFINITION ABSTRACT PUBLIC.
  PUBLIC SECTION.
    METHODS start_engine.
    METHODS move ABSTRACT.
ENDCLASS.

CLASS zcl_vehicle IMPLEMENTATION.
  METHOD start_engine.
    WRITE: / 'Engine started'.
  ENDMETHOD.
ENDCLASS.

" Interface
INTERFACE if_maneuverable PUBLIC.
  METHODS start.
  METHODS turn_left.
  METHODS turn_right.
  METHODS stop.
ENDINTERFACE.

" Concrete Class implementing both
CLASS zcl_car DEFINITION PUBLIC INHERITING FROM zcl_vehicle CREATE PUBLIC.
  PUBLIC SECTION.
    INTERFACES if_maneuverable.
    METHODS move REDEFINITION.
ENDCLASS.

CLASS zcl_car IMPLEMENTATION.
  METHOD move.
    WRITE: / 'Car is moving'.
  ENDMETHOD.

  METHOD if_maneuverable~start.
    WRITE: / 'Car started'.
  ENDMETHOD.
  METHOD if_maneuverable~turn_left.
    WRITE: / 'Car turns left'.
  ENDMETHOD.
  METHOD if_maneuverable~turn_right.
    WRITE: / 'Car turns right'.
  ENDMETHOD.
  METHOD if_maneuverable~stop.
    WRITE: / 'Car stopped'.
  ENDMETHOD.
ENDCLASS.

" Client Code Demonstrating Polymorphism
REPORT z_demo_poly.

DATA: lo_vehicle TYPE REF TO zcl_vehicle,
      lo_maneuver TYPE REF TO if_maneuverable.

lo_vehicle = NEW zcl_car( ).
lo_maneuver = NEW zcl_car( ).

" Polymorphism via abstract class reference
lo_vehicle->start_engine( ).
lo_vehicle->move( ).

" Polymorphism via interface reference
lo_maneuver->start( ).
lo_maneuver->turn_left( ).
lo_maneuver->stop( ).


```

### ✅ When to Use Which?

#### Abstract Class:

When you need shared logic and common attributes.
Example: All vehicles share start_engine logic.


#### Interface:

When you need capabilities that can apply across unrelated classes.
Example: IF_MANEUVERABLE can apply to Car, Boat, Drone.




#### ✅ Summary

Abstract classes = Base class + partial implementation + enforce structure.
Interfaces = Pure contract + multiple implementation flexibility.
Both together = Powerful design: Abstract class for common logic, interfaces for capabilities.


#### ✅ Visual Diagram (Conceptual)

 Abstract Class: ZCL_VEHICLE

 
          ----------------------------
          | start_engine()           |
          | move() [ABSTRACT]        |
          ----------------------------
                    ^
                    |
          ----------------------------
          | Concrete Class: ZCL_CAR |
          ----------------------------
          | Implements IF_MANEUVERABLE |
          ----------------------------

          

Interface: IF_MANEUVERABLE


````
----------------------------
| start()                   |
| turn_left()               |
| turn_right()              |
| stop()                    |
----------------------------
