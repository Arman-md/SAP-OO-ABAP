
# Interfaces in Object-Oriented ABAP

## Overview
The term **interface** has multiple meanings in IT:
- **GUI Interface**: Enables user interaction with software.
- **RICEF "I"**: Represents Interfaces for data exchange with external systems.
- **Function Module Signature**: Known as its interface.

In **object-oriented programming**, an interface has a specific meaning:  
An **independent interface** is disconnected from GUI, external data exchange, or function module signatures.

---

## What is an Interface?
- A **set of definitions** for:
  - Data types
  - Constants
  - Methods (without implementation)
- Used by a class as a **supplement to its public visibility**.
- A class **implements** an interface (similar to inheritance but without method implementation in the interface).

---

## Key Characteristics
- **Methods in an interface have no implementation**.
- The implementing class **must provide implementations** for all interface methods.
- Similar to **abstract methods** in parent classes.
- **No visibility levels** in interfaces:
  - All members are implicitly **public**.
- Common naming convention: Interfaces often end with **`able`** or **`ible`** (e.g., `IF_SERIALIZABLE`).

---

## Why Only Public Visibility?
- Question: Why can't implementing classes define interface methods as `protected` or `private`?
- Answer: Interfaces are designed to **guarantee public contracts** for external use, ensuring consistent accessibility.

---

## Summary
- Interfaces **extend capabilities** of classes without inheritance.
- They enforce **method signatures** and **public accessibility**.
- Provide a way to achieve **polymorphism** and **loose coupling** in ABAP OO design.

``


# Interfaces in Object-Oriented ABAP (Extended)

## Why Interfaces Must Be Public
- Implementing an interface is a **proclamation** by the class to external entities about the members it offers publicly.
- If a class implements an interface but makes any method **private**, external users cannot access all capabilities.
- This breaks **interchangeability** among classes implementing the same interface (important for design patterns).
- Therefore, **all interface members must remain publicly accessible**.

---

## Example Interface: `fuelConsumable`
### Data Types Defined by Interface
- `consumptionRate` : Integer
- `consumptionUnit` : Unit of measure
- `fuelUnit` : Unit of measure
- `fuelType` : String
- `fuelQuantity` : Integer
- `remainingFuelPercentage` : Decimal (nnn.nn)
- `remainingConsumptionUnits` : Integer

> **Note:** Interface defines **types**, not actual data fields → Class retains control over attribute visibility.

---

### Methods Defined by Interface
#### Setter Methods
- `setConsumptionRate(consumptionRate)`
- `setConsumptionUnit(consumptionUnit)`
- `setFuelUnit(fuelUnit)`
- `setFuelType(fuelType)`
- `setFuelCapacity(fuelQuantity)`
- `setFuelLevel(fuelQuantity)`

#### Getter Methods
- `getConsumptionRate(consumptionRate)`
- `getConsumptionUnit(consumptionUnit)`
- `getFuelUnit(fuelUnit)`
- `getFuelType(fuelType)`
- `getFuelCapacity(fuelQuantity)`
- `getFuelLevel(fuelQuantity)`

#### Additional Methods
- `calculatePercentageFuelRemaining(remainingFuelPercentage)`
- `estimateFuelExhaustion(remainingConsumptionUnits)`

---

## Implementation Example: Class `Car`
- Implements **all 14 methods** from `fuelConsumable`.
- Attributes defined as **private**, using interface data types.
- **Setters** copy parameter → private attribute.
- **Getters** copy private attribute → parameter.
- Calculation methods:
  - `remainingFuelPercentage = currentFuelLevel * 100 / fuelCapacity`
  - `remainingConsumptionUnits = currentFuelLevel * consumptionRate`

---

### Pseudocode Example
```abap
unused_fuel_capacity TYPE fuelConsumable.remainingFuelPercentage
remaining_consumption TYPE fuelConsumable.remainingConsumptionUnits
consumption_unit TYPE fuelConsumable.consumptionUnit

DATA this_car TYPE REF TO car.
CREATE OBJECT this_car.

CALL METHOD this_car->setConsumptionRate( '30' ).
CALL METHOD this_car->setConsumptionUnit( 'Miles' ).
CALL METHOD this_car->setFuelUnit( 'Gallon' ).
CALL METHOD this_car->setFuelType( 'Gasoline' ).
CALL METHOD this_car->setFuelCapacity( '14' ).
CALL METHOD this_car->setFuelLevel( '05' ).

CALL METHOD this_car->calculatePercentageFuelRemaining( unused_fuel_capacity ).
CALL METHOD this_car->estimateFuelExhaustion( remaining_consumption ).
CALL METHOD this_car->getConsumptionUnit( consumption_unit ).

WRITE: / 'Unused fuel capacity:', unused_fuel_capacity, '%'.
WRITE: / 'Remaining consumption:', remaining_consumption, consumption_unit.
```


# Polymorphism with Interface References (ABAP OO)

## Core Idea
If client code refers to an object via an **interface type** (e.g., `REF TO IF_FUEL_CONSUMABLE`), the **same code** works regardless of which class instance is behind that reference (`ZCL_CAR`, `ZCL_TRUCK`, …), **as long as** each class implements the interface.

### Why the rename works
- Original: `this_car TYPE REF TO ZCL_CAR`
- Polymorphic: `this_fuel_consumer TYPE REF TO IF_FUEL_CONSUMABLE`

Only the **variable type** changes. The **invocations** (`set...`, `get...`, `calculate...`, `estimate...`) remain identical because they target the **interface contract**.

### Creation remains class-specific
Even though the variable is typed to the **interface**, you still **instantiate a concrete class**:
```abap
CREATE OBJECT this_fuel_consumer TYPE ZCL_CAR.

```




# Interfaces & Polymorphism in ABAP OO  
*A single, self-contained README.md with summary + full ABAP source snippets*

---

## 📌 Overview

This guide consolidates the concepts and examples you provided into one GitHub-ready Markdown file:

- **Interfaces in OO**: Their purpose, visibility rules, and how they supplement class public visibility.
- **Static vs Dynamic Type**: How polymorphism works with interface-typed references.
- **Dynamic Dispatch**: Runtime selection of the correct implementation.
- **Fuel-Consumption Example**: Interface types + getters/setters + calculations and a concrete `Car` class.
- **“Boat” → “Maneuverable” Refactor**: Converting an abstract class use case to an interface pattern for better reuse and flexibility.
- **Complete ABAP**: Interfaces, implementing classes, and client code that demonstrates polymorphism.

You can paste the code snippets into your SAP system (adjusting names as needed) or keep this file as a conceptual reference.

---

## 1) Interfaces: Why all members are publicly accessible

- An **interface** is a **public contract** a class *proclaims* to external entities.
- If a class implements an interface, **all interface methods must be externally callable** (public).  
  Making any implemented interface method `private` or `protected` would break the contract and **interchangeability** across different implementing classes.
- **Best practice**: Avoid defining *variables* inside interfaces (even if technically possible) to **preserve encapsulation**. Prefer defining **types** and **constants**; let classes define their own attributes with appropriate visibility.

---

## 2) Interfaces supplement a class’s public API

- An interface can provide:
  - **Types**
  - **Constants**
  - **Method definitions** (signatures only, without implementation)
- **Classes implement interfaces** and must provide **all required methods**.
- Interfaces are often named with the suffix **`able`/`ible`** (e.g., `Serializable`, `Maneuverable`) to describe a **capability**.

---

## 3) Static vs Dynamic Type & Polymorphism

- **Static type**: The declared type of the reference at compile time.  
  Example: `DATA this_fuel_consumer TYPE REF TO if_fuel_consumable.`
- **Dynamic type**: The actual object instance at runtime.  
  Example: `this_fuel_consumer = NEW zcl_car( ).` → Dynamic type is `ZCL_CAR`.
- Interface references are **always polymorphic** because you **instantiate classes**, not interfaces.
- **Dynamic dispatch**: At runtime, the correct implementation (e.g., `ZCL_CAR`’s `estimate_fuel_exhaustion`) is invoked based on the dynamic type.

---

## 4) Fuel-Consumption Interface & ABAP Implementation

### 4.1 Interface: `IF_FUEL_CONSUMABLE`

```abap
"-----------------------------------------------------------------------
" Interface: IF_FUEL_CONSUMABLE
" Purpose : Define types and method signatures for fuel consumption
"-----------------------------------------------------------------------
INTERFACE if_fuel_consumable PUBLIC.

  TYPES:
    consumption_rate            TYPE i,
    consumption_unit            TYPE string,   " Simplified UoM
    fuel_unit                   TYPE string,   " Simplified UoM
    fuel_type                   TYPE string,
    fuel_quantity               TYPE i,
    remaining_fuel_percentage   TYPE p LENGTH 5 DECIMALS 2, " nnn.nn
    remaining_consumption_units TYPE i.

  " Setters
  METHODS set_consumption_rate
    IMPORTING i_rate TYPE consumption_rate.

  METHODS set_consumption_unit
    IMPORTING i_unit TYPE consumption_unit.

  METHODS set_fuel_unit
    IMPORTING i_unit TYPE fuel_unit.

  METHODS set_fuel_type
    IMPORTING i_type TYPE fuel_type.

  METHODS set_fuel_capacity
    IMPORTING i_capacity TYPE fuel_quantity.

  METHODS set_fuel_level
    IMPORTING i_level TYPE fuel_quantity.

  " Getters
  METHODS get_consumption_rate
    EXPORTING e_rate TYPE consumption_rate.

  METHODS get_consumption_unit
    EXPORTING e_unit TYPE consumption_unit.

  METHODS get_fuel_unit
    EXPORTING e_unit TYPE fuel_unit.

  METHODS get_fuel_type
    EXPORTING e_type TYPE fuel_type.

  METHODS get_fuel_capacity
    EXPORTING e_capacity TYPE fuel_quantity.

  METHODS get_fuel_level
    EXPORTING e_level TYPE fuel_quantity.

  " Calculations
  METHODS calculate_percentage_fuel_remaining
    EXPORTING e_percent TYPE remaining_fuel_percentage.

  METHODS estimate_fuel_exhaustion
    EXPORTING e_units TYPE remaining_consumption_units.

ENDINTERFACE.
```

### Class: ZCL_CAR implements IF_FUEL_CONSUMABLE
``` abap

"-----------------------------------------------------------------------
" Class : ZCL_CAR
" Role  : Concrete implementer of IF_FUEL_CONSUMABLE
"-----------------------------------------------------------------------
CLASS zcl_car DEFINITION PUBLIC FINAL CREATE PUBLIC.
  PUBLIC SECTION.
    INTERFACES if_fuel_consumable.
  PRIVATE SECTION.
    DATA:
      mv_consumption_rate  TYPE if_fuel_consumable=>consumption_rate,
      mv_consumption_unit  TYPE if_fuel_consumable=>consumption_unit,
      mv_fuel_unit         TYPE if_fuel_consumable=>fuel_unit,
      mv_fuel_type         TYPE if_fuel_consumable=>fuel_type,
      mv_fuel_capacity     TYPE if_fuel_consumable=>fuel_quantity,
      mv_fuel_level        TYPE if_fuel_consumable=>fuel_quantity.
ENDCLASS.

CLASS zcl_car IMPLEMENTATION.

  " Setters
  METHOD if_fuel_consumable~set_consumption_rate.
    mv_consumption_rate = i_rate.
  ENDMETHOD.

  METHOD if_fuel_consumable~set_consumption_unit.
    mv_consumption_unit = i_unit.
  ENDMETHOD.

  METHOD if_fuel_consumable~set_fuel_unit.
    mv_fuel_unit = i_unit.
  ENDMETHOD.

  METHOD if_fuel_consumable~set_fuel_type.
    mv_fuel_type = i_type.
  ENDMETHOD.

  METHOD if_fuel_consumable~set_fuel_capacity.
    mv_fuel_capacity = i_capacity.
  ENDMETHOD.

  METHOD if_fuel_consumable~set_fuel_level.
    mv_fuel_level = i_level.
  ENDMETHOD.

  " Getters
  METHOD if_fuel_consumable~get_consumption_rate.
    e_rate = mv_consumption_rate.
  ENDMETHOD.

  METHOD if_fuel_consumable~get_consumption_unit.
    e_unit = mv_consumption_unit.
  ENDMETHOD.

  METHOD if_fuel_consumable~get_fuel_unit.
    e_unit = mv_fuel_unit.
  ENDMETHOD.

  METHOD if_fuel_consumable~get_fuel_type.
    e_type = mv_fuel_type.
  ENDMETHOD.

  METHOD if_fuel_consumable~get_fuel_capacity.
    e_capacity = mv_fuel_capacity.
  ENDMETHOD.

  METHOD if_fuel_consumable~get_fuel_level.
    e_level = mv_fuel_level.
  ENDMETHOD.

  " Calculations
  METHOD if_fuel_consumable~calculate_percentage_fuel_remaining.
    IF mv_fuel_capacity IS INITIAL.
      e_percent = 0.
    ELSE.
      e_percent = ( mv_fuel_level * 100 ) / mv_fuel_capacity.
    ENDIF.
  ENDMETHOD.

  METHOD if_fuel_consumable~estimate_fuel_exhaustion.
    e_units = mv_fuel_level * mv_consumption_rate.
  ENDMETHOD.

ENDCLASS.


```

### Client report demonstrating polymorphism via interface reference
``` abap


"-----------------------------------------------------------------------
" Report: Z_DEMO_FUEL_CONSUMABLE
"-----------------------------------------------------------------------
REPORT z_demo_fuel_consumable.

DATA:
  this_fuel_consumer     TYPE REF TO if_fuel_consumable,
  unused_fuel_capacity   TYPE if_fuel_consumable=>remaining_fuel_percentage,
  remaining_consumption  TYPE if_fuel_consumable=>remaining_consumption_units,
  consumption_unit       TYPE if_fuel_consumable=>consumption_unit.

" Polymorphic reference: interface-typed variable, class-typed instance
this_fuel_consumer = NEW zcl_car( ).

" Set sample values
this_fuel_consumer->set_consumption_rate( i_rate     = 30 ).
this_fuel_consumer->set_consumption_unit( i_unit     = 'Miles' ).
this_fuel_consumer->set_fuel_unit(        i_unit     = 'Gallon' ).
this_fuel_consumer->set_fuel_type(        i_type     = 'Gasoline' ).
this_fuel_consumer->set_fuel_capacity(    i_capacity = 14 ).
this_fuel_consumer->set_fuel_level(       i_level    = 5 ).

" Invoke behaviors (calls are against the interface contract)
this_fuel_consumer->calculate_percentage_fuel_remaining(
  IMPORTING e_percent = unused_fuel_capacity ).

this_fuel_consumer->estimate_fuel_exhaustion(
  IMPORTING e_units = remaining_consumption ).

this_fuel_consumer->get_consumption_unit(
  EXPORTING e_unit = consumption_unit ).

WRITE: / |this_fuel_consumer unused fuel capacity: { unused_fuel_capacity } %|.
WRITE: / |this_fuel_consumer remaining consumption: { remaining_consumption } { consumption_unit }|.


```

###
**Expected output
this_fuel_consumer unused fuel capacity: 35.71 %
this_fuel_consumer remaining consumption: 150 Miles**


# One of the best examples to show how intefaces can fascilitate dynamic polymorphism 

## Interface Definition : Interface: IF_MANEUVERABLE










``` abap

"-----------------------------------------------------------------------
" Interface: IF_MANEUVERABLE
" Purpose : Generic maneuvering capability
"-----------------------------------------------------------------------
INTERFACE if_maneuverable PUBLIC.
  METHODS start.
  METHODS turn_left.
  METHODS turn_right.
  METHODS stop.
ENDINTERFACE.


```


##  Implementers -> 1 : ZCL_MOTOR_BOAT

``` abap


CLASS zcl_motor_boat DEFINITION PUBLIC FINAL CREATE PUBLIC.
  PUBLIC SECTION.
    INTERFACES if_maneuverable.
ENDCLASS.

CLASS zcl_motor_boat IMPLEMENTATION.
  METHOD if_maneuverable~start.
    " engage propeller
  ENDMETHOD.
  METHOD if_maneuverable~turn_left.
    " rotate steering wheel counterclockwise
  ENDMETHOD.
  METHOD if_maneuverable~turn_right.
    " rotate steering wheel clockwise
  ENDMETHOD.
  METHOD if_maneuverable~stop.
    " disengage propeller
  ENDMETHOD.
ENDCLASS.

```

## Implementers -> 2 : ZCL_SAIL_BOAT

``` abap


CLASS zcl_sail_boat DEFINITION PUBLIC FINAL CREATE PUBLIC.
  PUBLIC SECTION.
    INTERFACES if_maneuverable.
ENDCLASS.

CLASS zcl_sail_boat IMPLEMENTATION.
  METHOD if_maneuverable~start.
    " raise sail
  ENDMETHOD.
  METHOD if_maneuverable~turn_left.
    " push tiller to the right
  ENDMETHOD.
  METHOD if_maneuverable~turn_right.
    " push tiller to the left
  ENDMETHOD.
  METHOD if_maneuverable~stop.
    " lower sail
  ENDMETHOD.
ENDCLASS.

```

## Implementers -> 3 : ZCL_BOAT_MOVER (not a boat, still maneuverable)


``` abap


CLASS zcl_boat_mover DEFINITION PUBLIC FINAL CREATE PUBLIC.
  PUBLIC SECTION.
    INTERFACES if_maneuverable.
ENDCLASS.

CLASS zcl_boat_mover IMPLEMENTATION.
  METHOD if_maneuverable~start.
    " release brake; engage drive wheels
  ENDMETHOD.
  METHOD if_maneuverable~turn_left.
    " move joystick to the left
  ENDMETHOD.
  METHOD if_maneuverable~turn_right.
    " move joystick to the right
  ENDMETHOD.
  METHOD if_maneuverable~stop.
    " disengage drive wheels; apply brake
  ENDMETHOD.
ENDCLASS.

```


## Orchestrator: ZCL_MARINA

``` abap


"-----------------------------------------------------------------------
" Class : ZCL_MARINA
" Role  : Demonstrate polymorphism with IF_MANEUVERABLE
"-----------------------------------------------------------------------
CLASS zcl_marina DEFINITION PUBLIC CREATE PUBLIC.
  PUBLIC SECTION.
    METHODS launch_motor_boat.
    METHODS launch_sail_boat.
    METHODS move_boat_to_land_storage.
  PRIVATE SECTION.
    METHODS maneuver
      IMPORTING i_m TYPE REF TO if_maneuverable.
ENDCLASS.

CLASS zcl_marina IMPLEMENTATION.

  METHOD launch_motor_boat.
    DATA(lo_motor_boat) = NEW zcl_motor_boat( ).
    maneuver( lo_motor_boat ).
  ENDMETHOD.

  METHOD launch_sail_boat.
    DATA(lo_sail_boat) = NEW zcl_sail_boat( ).
    maneuver( lo_sail_boat ).
  ENDMETHOD.

  METHOD move_boat_to_land_storage.
    DATA(lo_boat_mover) = NEW zcl_boat_mover( ).
    maneuver( lo_boat_mover ).
  ENDMETHOD.

  METHOD maneuver.
    i_m->start( ).
    i_m->turn_left( ).
    i_m->turn_right( ).
    i_m->stop( ).
  ENDMETHOD.

ENDCLASS.


```


# Interfaces and Inheritance in ABAP OO

## Why Interfaces?
- **Primary reason**: Achieve the equivalent of **multiple inheritance** in environments that support only **single inheritance**.
- A class can **implement multiple interfaces** without restriction.
- Interfaces allow a class to inherit capabilities from multiple contributors without forming a complex class hierarchy.

---

## Multiple Inheritance vs Interfaces
- Example hierarchy (Figure 7-1):


<img width="863" height="446" alt="image" src="https://github.com/user-attachments/assets/bc10ff6a-1844-4fa3-b511-1e73b2ead193" />

- **Problem**: `dog` needs members from both `canine` and `domesticPet`.
- **Solution**: Make `domesticPet` an interface → `dog` inherits from `canine` and implements `domesticPet`.

---

## Table of Attributes & Behaviors (from Figure/Table 7-2)

| Class        | Attributes                              | Behaviors                  |
|-------------|-----------------------------------------|---------------------------|
| animal      | height, weight, age, alacrity          | eat, sleep, speak        |
| mammal      | furColor                               | nurseOffspring           |
| canine      | furColor                               | run, jump, followScentTrail |
| domesticPet | petName, ownerName, lastVeterinarianVisit | getPetName, setPetName, visitVeterinarian |
| dog         | —                                      | chaseCat, fetch          |
| fox         | —                                      | raidChickenCoop          |

---

## Implementing Multiple Contributors
### Interface: `IF_DOMESTIC_PET`

```abap
INTERFACE if_domestic_pet PUBLIC.
  METHODS get_pet_name RETURNING VALUE(rv_name) TYPE string.
  METHODS set_pet_name IMPORTING iv_name TYPE string.
  METHODS visit_veterinarian.
ENDINTERFACE.
```

``` abap

CLASS zcl_dog DEFINITION PUBLIC INHERITING FROM zcl_canine FINAL CREATE PUBLIC.
  PUBLIC SECTION.
    INTERFACES if_domestic_pet.
  PRIVATE SECTION.
    DATA mv_pet_name TYPE string.
ENDCLASS.

CLASS zcl_dog IMPLEMENTATION.
  METHOD if_domestic_pet~get_pet_name.
    rv_name = mv_pet_name.
  ENDMETHOD.

  METHOD if_domestic_pet~set_pet_name.
    mv_pet_name = iv_name.
  ENDMETHOD.

  METHOD if_domestic_pet~visit_veterinarian.
    " Logic for vet visit
  ENDMETHOD.
ENDCLASS.


```

## Class Coupling & Loose Coupling

### Coupling: Degree to which one class depends on another.
### Loose coupling: Achieved when a class uses an interface reference instead of a concrete class reference.
### Benefits:

-> Flexible design
-> Easier maintenance
-> Promotes high cohesion and low coupling



-> Example: Method Signature with Interface Reference

``` abap

METHOD maneuver IMPORTING i_m TYPE REF TO if_maneuverable.
  i_m->start( ).
  i_m->turn_left( ).
  i_m->turn_right( ).
  i_m->stop( ).
ENDMETHOD.


```
#### maneuver does not care if i_m is motorBoat, sailBoat, or boatMover → loose coupling.

## Cohesion vs Coupling

### High cohesion → class does one thing well → promotes loose coupling.
### Low cohesion → class does too many unrelated things → promotes tight coupling.
### Interfaces help achieve high cohesion + loose coupling.



# ABAP Language Support for Interfaces  

---

## Object-Oriented Extensions for Interfaces (ABAP)

ABAP accommodates **interfaces** in the following ways:

1. **Facilitating the definition of independent interfaces**
2. **Supporting the use of independent interfaces in class definitions**
3. **Supporting aliases within classes for members contributed by interfaces**
4. **Enabling polymorphism through the use of interface reference variables**

> **Note on loose coupling**  
> While loose coupling can also occur when a subclass instance is referenced via a superclass reference, that approach depends on **class inheritance** and is confined to the same **inheritance hierarchy**. **Interfaces** are not limited by such constraints and therefore provide broader flexibility.

---

## Interface Definition Syntax (Single Construct)

Unlike classes (which have separate definition and implementation sections), an interface is defined in **one block**:

```abap
INTERFACE interface_name PUBLIC.
  " Optional: Types visible to implementers
  TYPES: t_example TYPE i.

  " Optional: Constants visible to implementers
  CONSTANTS: c_example TYPE string VALUE 'EXAMPLE'.

  " Method signatures (no implementations here)
  METHODS interface_method_name
    IMPORTING i_param TYPE t_example
    EXPORTING e_param TYPE t_example.
ENDINTERFACE.
```


## Accessing Interface Types and Constants (=>)
Both class and non-class components can access interface types and constants using the component selector =>:
ABAP REPORT z_demo_interface_access.

``` abap


REPORT z_demo_interface_access.

DATA lv_value TYPE interface_name=>type_name.

IF lv_value = interface_name=>constant_name.
  " ... logic using the interface's constant
ENDIF.

```

## Implementing Interface Methods (~)
``` abap

CLASS class_name IMPLEMENTATION.

  METHOD interface_name~method_name.
    " Implementation of the interface method
  ENDMETHOD.

ENDCLASS.


```


## Aliases for Interface Members
To avoid repeated use of the interface_name~ selector, you can introduce aliases in the class definition:

``` abap
CLASS class_name DEFINITION PUBLIC CREATE PUBLIC.
  PUBLIC SECTION.
    INTERFACES interface_name.
    ALIASES alias_name FOR interface_name~method_name. " Short name for the interface method
ENDCLASS.

CLASS class_name IMPLEMENTATION.

  METHOD alias_name.
    " Implementation bound to interface_name~method_name
  ENDMETHOD.

ENDCLASS.

" Client code
DATA(lo_obj) = NEW class_name( ).
lo_obj->alias_name( ).

```

# Quick Reference (Cheat Sheet)

``` abap


" Define interface
INTERFACE if_name PUBLIC.
  TYPES t_kind TYPE i.
  CONSTANTS c_flag TYPE abap_bool VALUE abap_true.
  METHODS do_work IMPORTING i_x TYPE t_kind.
ENDINTERFACE.

" Implement in class
CLASS zcl_impl DEFINITION PUBLIC CREATE PUBLIC.
  PUBLIC SECTION.
    INTERFACES if_name.
    ALIASES work FOR if_name~do_work. " Optional alias
ENDCLASS.

CLASS zcl_impl IMPLEMENTATION.
  METHOD if_name~do_work.
    " Implementation here
  ENDMETHOD.

  " Or implement via alias name (bound to the same interface method)
  METHOD work.
    " Implementation here
  ENDMETHOD.
ENDCLASS.

" Use interface types/constants
DATA lv TYPE if_name=>t_kind.
IF lv IS INITIAL AND if_name=>c_flag = abap_true.
  " ...
ENDIF.

" Polymorphism with interface reference
DATA: lo_if TYPE REF TO if_name,
      lo_cl TYPE REF TO zcl_impl.
CREATE OBJECT lo_cl.
lo_if = lo_cl.
lo_if->do_work( i_x = 1 ).


```


