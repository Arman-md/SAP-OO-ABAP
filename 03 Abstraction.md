
# ✅ Abstraction in Object-Oriented Programming

## 🔍 What is Abstraction?
- **Definition**:
  - "Considered apart from concrete existence … thought of or stated without reference to a specific instance."
  - In OOP, abstraction means **focusing on essential characteristics** while hiding unnecessary details.

- **Purpose**:
  - Simplifies complex systems by modeling relevant aspects.
  - Helps design flexible systems that adapt to future changes.

---

## 🔍 Real-World Representation
- Objects often correspond to **real-world entities**.
- Example: A `Car` class represents the concept of a car.
- BUT:
  - Not all classes map directly to real-world objects.
  - Some classes exist purely for **design flexibility** (e.g., helper classes, abstract base classes).

---

## 🔍 Key Insights.
- Strict real-world modeling can lead to rigid designs.
- **Abstractions that emerge during design are key to flexibility**.
- Design should anticipate **future requirements**, not just current realities.

---

## 🎨 Abstract Art Analogy
- A cartoon of a car:
  - Shows only **details relevant to the discussion** (e.g., windshield).
  - Represents **any car**, not a specific one.
- Similarly, in OOP:
  - A class provides a **generalized view** of an entity.
  - Hides unnecessary details to keep focus on what matters.

---

### ✅ Key Takeaways
- Abstraction = **generalization + hiding irrelevant details**.
- Enables **simpler, more maintainable, and flexible designs**.
- Not all abstractions map to real-world objects—some exist for **architectural needs**.



# ✅ Abstraction in Object-Oriented Programming (Extended)

## 🔍 Another Analogy: Romance Novel Characters
- Authors provide **only enough details** about characters (hero, villain, damsel) to support the story.
- Readers fill in missing details using imagination.
- Each character = **abstraction**, not a specific person.
- Key idea: **Focus on essentials, hide unnecessary details**.

---

## 🔍 Representing Real-World Entities
- Examples: `Car`, `BankAccount`, `WeatherForecast`.
- Each represented as a **class**:
  - **Car Class**:
    - Attributes: `make`, `model`, `year`, `serial_number`, `speed`, `fuel_quantity`.
    - Behaviors: `start`, `stop`, `turn`, `accelerate`.
  - **BankAccount Class**:
    - Attributes: `account_number`, `balance`, `interest_rate`.
    - Behaviors: `deposit`, `withdraw`, `calculate_interest`.
  - **WeatherForecast Class**:
    - Attributes: `high_temp`, `low_temp`, `precipitation_chance`.
    - Behaviors: `update_forecast`, `display_forecast`.

---

## 🔍 Difference from Procedural Programming
- **Procedural**:
  - Designed to perform specific tasks or processes.
- **Object-Oriented**:
  - Designed to **manage information** about entities.
  - Example:
    - `Car` class manages car-related info only.
    - Does **not** manage unrelated info (e.g., driver’s car ownership history).

---

## 🏭 Real-World Example: Muffler Manufacturer
- Requirement:
  - Track shipping containers between plant and warehouses.
  - Info includes:
    - Container ID
    - Loading/unloading status
    - Transit details (truck/rail, company name)
    - Location
    - Destination warehouse
    - Estimated arrival time
- **Why abstraction matters**:
  - Classes like `ShippingContainer`, `Warehouse`, `TransportMode` can model this scenario.
  - Each class focuses on **its own responsibility**.

---

### ✅ Key Takeaways
- Abstraction = **generalization + essential details only**.
- Classes represent **real-world entities** but hide irrelevant details.
- Enables **flexible, maintainable designs**.
- OOP focuses on **information management**, not just process execution.



# ✅ Procedural vs Object-Oriented Design & Class Cohesion

## 🏭 Example Scenario: Muffler Manufacturer Report
- **Report Requirements**:
  - Track shipping containers between plant and warehouses.
  - Info includes:
    - Container ID
    - Destination warehouse
    - Current location
    - Status (Loading, Unloading, On truck, On rail car)
    - Carrier name
    - ETA

### Example Output (Table 4-1)
| Container ID | Destination      | Current Location | Status       | Carrier           | ETA       |
|-------------|------------------|-----------------|-------------|-------------------|-----------|
| HGF107588   | Linden, NJ       | Linden, NJ      | Unloading   |                   |           |
| YKZ503401   | Linden, NJ       | Altoona, PA     | On rail car | Norfolk Southern  | Tomorrow  |
| BNX969443   | Linden, NJ       | Newark, NJ      | On truck    | RNX Logistics     | Today     |
| BNX969447   | Kansas City, MO  | Indianapolis, IN| On rail car | BNSF              | Tomorrow  |
| BNX963850   | Kansas City, MO  | Kansas City, MO | Unloading   |                   |           |
| YKZ500067   | Kansas City, MO  | Kansas City, MO | On truck    | Harris Transport  | Today     |
| HGF109905   | Hayward, CA      | Salt Lake City, UT| On rail car| BNSF              | Two days  |
| YKZ501991   | Hayward, CA      | Chicago, IL     | On rail car | BNSF              | Four days |
| HGF103556   | Hayward, CA      | Oakland, CA     | On truck    | Western Express   | Today     |
| HGF102002   | Hayward, CA      | Cleveland, OH   | Loading     |                   | Five days |

---

## 🔍 Procedural Approach
- Global table stores **all information** (containers, warehouses, carriers).
- Multiple subroutines handle processing and reporting.
- **Focus**: Processing requirement.
- **Problem**:
  - No clear separation of concerns.
  - Shipping container and truck info mixed in same structure.
  - Harder to maintain and extend.

---

## 🔍 Object-Oriented Approach
- Define **classes** for:
  - `ShippingContainer`
  - `Warehouse`
  - `ManufacturingPlant`
  - `Truck` / `TruckingCompany`
  - `RailCar` / `RailroadCompany`
  - `Report`
- Each class:
  - Represents an **abstraction** of its real-world counterpart.
  - Manages **only relevant information**.
- **Focus**: Data organization and management.
- **Benefits**:
  - High cohesion.
  - Easier maintenance and scalability.

---

## 🔍 Class Cohesion
- **Definition**: Degree to which members of a class are related to each other.
- **High Cohesion**:
  - Class contains only members relevant to its abstraction.
  - Example: `ShippingContainer` → container ID, status, location.
- **Low Cohesion**:
  - Class mixes unrelated members (e.g., container + truck info).
- **Best Practice**:
  - Design classes with **single responsibility** and high cohesion.

---

### ✅ Key Takeaways
- Procedural = **process-centric**, mixes data for multiple entities.
- OOP = **data-centric**, separates responsibilities into classes.
- High cohesion improves **maintainability, readability, and scalability**.
``


# ✅ Abstraction, Cohesion, Reusability & Levels of Abstraction (OOP / ABAP Notes)

## 🔍 Class Cohesion (Shipping Container Example)
- **High cohesion**: All attributes/behaviors relate to the same abstraction.
  - **Attributes**: `container_id`, `color`, `height`, `width`, `depth`, `capacity`, `tare_weight`,
    `max_gross_weight`, `net_weight`, `loaded_quantity`, `security_tag_number`
  - **Behaviors**: `load`, `unload`, `get_gross_weight`, `apply_security_tag`
- **Low cohesion (avoid)**:
  - `trucking_company_name` → belongs to **transport** context, not the container itself.
  - `manufacturer_employee_count_last_year` → unrelated to shipping container domain.

> **Guideline**: Keep class members strictly relevant to the class’s abstraction; move cross‑cutting or context-specific info to their own classes (e.g., `Truck`, `RailCar`, `Carrier`, `Shipment`).

---

## 🔁 Reusable Components (Why OOP Helps)
- Procedural style might be faster for a **single report**, but OOP yields:
  - **Reusability**: The `ShippingContainer` class can be reused for multiple future reports:
    - Damaged/out-of-circulation containers
    - Age & lifespan analytics
    - Transit performance by carrier/mode
  - **Maintainability**: Clear ownership—each class manages its own data and behaviors.
  - **Composability**: New reports simply orchestrate existing abstractions.

> **Outcome**: Build a **library of reusable domain components** that accelerates future reporting/features.

---

## 🧭 Levels of Abstraction (Detail vs. Scope)
- **Concept**: Abstraction level governs the **amount of detail** vs **scope** you see.
- **Inverse relationship**:
  - Higher altitude → **wider scope, less detail**
  - Lower altitude → **narrower scope, more detail**

### Metaphor: Patio at Different Altitudes
| Altitude (feet) | Scope                                | Level of Detail                                             |
|-----------------|--------------------------------------|-------------------------------------------------------------|
| 50,000          | Entire county                         | Cannot discern patios                                       |
| 5,000           | Entire town                           | Patios visible; no color/pattern/material                   |
| 500             | Several houses                        | Patios + color; no pattern/material                         |
| 50              | Whole patio + roof + some yard        | Patio color + pattern; no material                          |
| 5               | Portion of patio                      | Color + pattern + material                                  |

> **Design takeaway**: Choose the **lowest abstraction** that provides only the required details, but no more.

---

## 🟦 Abstraction Ladder (Shapes Example)
Classes at different abstraction depths:

1. **EnclosedShape** (Highest abstraction; widest scope)
2. **EnclosedShapeWithAngle** (Mid abstraction; narrower scope; more detail)
3. **Rectangle** (Lowest abstraction; narrow scope; most detail)

### Members by Class
| Class                         | Attributes                        | Behaviors              |
|------------------------------|-----------------------------------|------------------------|
| EnclosedShape                | `area`, `perimeter`               | `getArea`, `getPerimeter` |
| EnclosedShapeWithAngle       | `area`, `perimeter`, `smallest_angle` | `getArea`, `getPerimeter`, `getSmallestAngle` |
| Rectangle                    | `area`, `perimeter`, `smallest_angle`, `hypotenuse` | `getArea`, `getPerimeter`, `getSmallestAngle`, `getHypotenuse` |

- **Specialization**: Each lower class **adds detail** (extra attributes/behaviors).
- **Generalization**: Each higher class **removes detail** but supports a broader set of shapes.

### Choosing the Right Abstraction
- Report requirement: **area & perimeter of various shapes** → use **EnclosedShape**
  - It covers **all shapes** and provides **exactly** the required details.
  - Using `Rectangle` would be **over‑specification**; extra details (e.g., hypotenuse) are irrelevant.

---

## 🧩 Procedural vs OOP (Shipping Containers)
- **Procedural**:
  - Global table holds all entities (containers, trucks, carriers) → mixed data; tight coupling.
  - Focus: **process** implementation.
- **OOP**:
  - Distinct classes (`ShippingContainer`, `Warehouse`, `Carrier`, `Truck`, `RailCar`, `Report`) → separation of concerns.
  - Each class manages **only its relevant data & behavior**.
  - Focus: **data modeling** and **management**, enabling reusability.

---

## ✅ Practical Guidelines (for your projects)
- **Model by responsibility**: One class = one abstraction; avoid unrelated fields.
- **Prefer composition over leakage**: Link `ShippingContainer` to `Shipment/Transport` objects rather than storing transport-specific fields inside the container.
- **Pick the minimal sufficient abstraction**: Implement only the details your use case needs.
- **Design for reuse**: Build a domain library; keep reports thin—consume domain objects.

---

## 🔗 ABAP Angle (optional starter)
- **Class split**:
  - `ZCL_SHIPPING_CONTAINER` (high cohesion: physical/container attributes + ops)
  - `ZCL_SHIPMENT` (route, status, ETA, carrier, mode)
  - `ZCL_REPORT_CONTAINERS_IN_USE` (formats and renders data)
- **Benefit**: You can write new reports by reusing the same domain classes without touching their internals.



# ✅ Multiple Instantiations, Abstraction & Encapsulation

## 🔍 Multiple Instantiations
- **Class** = blueprint (abstraction).
- **Object** = concrete instance of a class.
- **Key Points**:
  - A single program can create **virtually unlimited objects** from the same class.
  - Each object shares the same **attributes and behaviors** (as per class definition).
  - Each object has **unique attribute values** → makes abstraction tangible.
- **Terminology**:
  - Abstraction = conceptualization (general).
  - Concretion = instantiation (specific).

### Examples of Abstraction vs Concretion
| Abstraction       | Concretion                  |
|-------------------|-----------------------------|
| General           | Specific                   |
| Potential         | Actual                     |
| Conceptual        | Tangible                   |
| Product mold      | Product                    |
| Cookie cutter     | Cookie                     |
| Car               | My first car               |
| Book              | This copy of this book     |
| Building          | Carnegie Hall              |
| Road              | Pennsylvania Turnpike      |
| River             | Rhine                      |
| Mountain range    | Andes                      |
| Continent         | Antarctica                 |
| Planet            | Jupiter                    |
| Star              | Rigel                      |
| Galaxy            | Andromeda                  |

---

## 🔍 Relationship Between Abstraction & Encapsulation
- **Abstraction**:
  - Allows viewing an object at a **high level**, ignoring unnecessary details.
  - Example: Referring to a "house" instead of "glass, wood, nails".
- **Encapsulation**:
  - Restricts access to internal details.
  - **Steve McConnell’s perspective**:
    - *“Abstraction says you’re allowed to look at an object at a high level of detail.”*
    - *“Encapsulation says you aren’t allowed to look at any other level of detail.”*
  - Encapsulation enforces **information hiding**:
    - What you see is **all you get**.
    - Prevents direct access to internal complexity.

---

### ✅ Key Takeaways
- **Classes** encapsulate attributes and behaviors relevant to their abstraction level.
- **Objects** are concrete representations of abstractions.
- Abstraction simplifies complexity; encapsulation enforces boundaries.
- Together, they form the foundation of **object-oriented programming**.

---


## 💡 Practical ABAP Angle
- **Class Definition**:
  - Represents abstraction (e.g., `ZCL_CAR`).
- **Encapsulation**:
  - Achieved via visibility sections (`PUBLIC`, `PRIVATE`, `PROTECTED`).
- **Instantiation**:
  ```abap
  DATA rental_car TYPE REF TO zcl_car.
  CREATE OBJECT rental_car.



# ✅ ABAP Language Support for Abstraction

## 🔍 How ABAP Supports Abstraction
- **Define representations for real-world entities**:
  - Classes represent abstractions (e.g., `Car`, `BankAccount`, `ShippingContainer`).
- **Establish clear levels of abstraction**:
  - Judicious class naming and member selection.
- **Support multiple instantiations**:
  - Create many objects from the same class blueprint.

---

## 🔍 Class Definition Syntax
```abap
CLASS class_name DEFINITION [options].
  " Visibility sections: PUBLIC, PROTECTED, PRIVATE
ENDCLASS.

```

## ZOOT102C 

``` abap


REPORT zoot102c.

************************************************************************
* Title:
*   Objects 102: Car report using mix of instance and static attribs/meths
*
* Selection text values:
*   PBRAND   - Brand
*   PCOLOR   - Color
*   PHEADING - Starting compass heading
*   PLOCATN  - Starting location
*   PMODEL   - Model
*   PPLATE   - License plate
*   PSPEEDU  - Speed unit
*   PSPEED01 - Sequence of speed increments
*   PSPEED02 - (none)
*   PSPEED03 - (none)
*   PTURN01  - Sequence of turns
*   PTURN02  - (none)
*   PTURN03  - (none)
*   PYEAR    - Year
*
* Text symbol values:
*   (none)
*
* J. McDonough - October 2012
*
* This program will show the current attributes for a vehicle using
* values supplied by the user. An invalid value specified for
* starting compass heading will default to North. An invalid value
* specified for a turn will be ignored.
*
* Other program components:
* GUI Status SELECTION_SCREEN - A copy of GUI status %_00
* of program RSSYSTDB with the following changes:
*
* Application
* Function Text             Icon                  Menu Bar Toolbar Function keys
* --------- --------------- -------------------- --------- ------- -------------
* NEWCAR    Add new car     ICON_CREATE          (none)    item 12 F5 (unused)
*
* Differences with preceding version:
* Class "car" was enhanced to accommodate assigning a serial number
* for the registered car. The attribute retaining the most recently
* used serial number and its processing methods are static, however
* each "car" instance gets and retains its own uniquely assigned
* serial number. A new static constructor initializes the last used
* serial number and it is incremented by 1 each time a new car object
* is created. This illustrates the use of both static and instance
* members (attributes and methods) defined within a single class.
*
* The "report" class also has been changed to include in the ALV
* report a column to represent the serial number attribute of each
* car.
************************************************************************

* Self-contained alias for simple text parameters
TYPES: f4txt TYPE string.

*======================================================================*
*                                                                      *
*  C l a s s   D e f i n i t i o n s                                   *
*                                                                      *
*======================================================================*

*----------------------------------------------------------------------
* Class: navigator definition
*----------------------------------------------------------------------
CLASS navigator DEFINITION FINAL.
  PUBLIC SECTION.
    TYPES:  turn_type    TYPE char1,
            heading_type TYPE char1.

    CONSTANTS: left_turn  TYPE navigator=>turn_type VALUE 'L',
               right_turn TYPE navigator=>turn_type VALUE 'R',
               u_turn     TYPE navigator=>turn_type VALUE 'U'.

    METHODS: change_heading
                IMPORTING turn    TYPE navigator=>turn_type,
             get_heading
                EXPORTING heading TYPE navigator=>heading_type,
             constructor
                IMPORTING heading TYPE navigator=>heading_type.

  PRIVATE SECTION.
    CONSTANTS: compass                 TYPE char4 VALUE 'NESW',
               compass_offset_limit_lo TYPE int4  VALUE 00,
               compass_offset_limit_hi TYPE int4  VALUE 03.
    DATA: heading TYPE navigator=>heading_type.
ENDCLASS.                    " navigator definition

*----------------------------------------------------------------------
* Class: car definition
*----------------------------------------------------------------------
CLASS car DEFINITION FINAL.
  PUBLIC SECTION.
    TYPES: brand_type        TYPE f4txt,
           color_type        TYPE f4txt,
           location_type     TYPE f4txt,
           model_type        TYPE f4txt,
           license_plate_type TYPE f4txt,
           speed_type        TYPE int4,
           speed_unit_type   TYPE char3,
           year_type         TYPE num4,
           serial_type       TYPE num4.

    CLASS-METHODS: class_constructor.

    METHODS: accelerate
                IMPORTING acceleration TYPE car=>speed_type,
             change_heading
                IMPORTING turn         TYPE navigator=>turn_type,
             get_characteristics
                EXPORTING serial_number TYPE car=>serial_type
                          license_plate TYPE car=>license_plate_type
                          brand         TYPE car=>brand_type
                          model         TYPE car=>model_type
                          year          TYPE car=>year_type
                          color         TYPE car=>color_type
                          location      TYPE car=>location_type
                          speed_unit    TYPE car=>speed_unit_type,
             get_heading
                EXPORTING heading       TYPE navigator=>heading_type,
             get_speed
                EXPORTING speed         TYPE car=>speed_type,
             constructor
                IMPORTING license_plate TYPE car=>license_plate_type
                          brand         TYPE car=>brand_type
                          model         TYPE car=>model_type
                          year          TYPE car=>year_type
                          color         TYPE car=>color_type
                          location      TYPE car=>location_type
                          speed_unit    TYPE car=>speed_unit_type
                          heading       TYPE navigator=>heading_type.

  PRIVATE SECTION.
    CLASS-DATA: last_serial_value TYPE car=>serial_type.

    DATA: license_plate  TYPE car=>license_plate_type,
          brand          TYPE car=>brand_type,
          model          TYPE car=>model_type,
          year           TYPE car=>year_type,
          color          TYPE car=>color_type,
          location       TYPE car=>location_type,
          speed          TYPE car=>speed_type,
          speed_unit     TYPE car=>speed_unit_type,
          serial_number  TYPE car=>serial_type,
          navigation_unit TYPE REF TO navigator.

    CLASS-METHODS: get_serial_number
                     EXPORTING serial_number TYPE car=>serial_type.
ENDCLASS.                    " car definition

*----------------------------------------------------------------------
* Class: report definition
*----------------------------------------------------------------------
CLASS report DEFINITION ABSTRACT FINAL CREATE PRIVATE.
  PUBLIC SECTION.
    CONSTANTS: execute                      TYPE syucomm VALUE 'ONLI',
               add_new_car                  TYPE syucomm VALUE 'NEWCAR',
               selection_screen_status_name TYPE sypfkey VALUE 'SELECTION_SCREEN'.

    CLASS-METHODS: register_car_entry
                     IMPORTING license_plate TYPE car=>license_plate_type
                               brand         TYPE car=>brand_type
                               year          TYPE car=>year_type
                               model         TYPE car=>model_type
                               color         TYPE car=>color_type
                               location      TYPE car=>location_type
                               heading       TYPE navigator=>heading_type
                               turn01        TYPE navigator=>turn_type
                               turn02        TYPE navigator=>turn_type
                               turn03        TYPE navigator=>turn_type
                               speed01       TYPE car=>speed_type
                               speed02       TYPE car=>speed_type
                               speed03       TYPE car=>speed_type
                               speed_unit    TYPE car=>speed_unit_type,
                   show_report.

  PRIVATE SECTION.
    TYPES: BEGIN OF output_row,                       "#EC *
             serial_number TYPE car=>serial_type,
             license_plate TYPE car=>license_plate_type,
             brand         TYPE car=>brand_type,
             model         TYPE car=>model_type,
             year          TYPE car=>year_type,
             color         TYPE car=>color_type,
             location      TYPE car=>location_type,
             heading       TYPE navigator=>heading_type,
             speed         TYPE car=>speed_type,
             speed_unit    TYPE car=>speed_unit_type,
           END OF output_row,
           output_list TYPE STANDARD TABLE OF report=>output_row.

    CLASS-DATA: output_stack TYPE report=>output_list,
                car_stack    TYPE STANDARD TABLE OF REF TO car.

    CLASS-METHODS: build_report,
                   present_report,
                   set_column_titles
                     IMPORTING alv_grid TYPE REF TO cl_salv_table.
ENDCLASS.                    " report definition

*======================================================================*
*                                                                      *
*  C l a s s   I m p l e m e n t a t i o n s                           *
*                                                                      *
*======================================================================*

*----------------------------------------------------------------------
* Class: navigator implementation
*----------------------------------------------------------------------
CLASS navigator IMPLEMENTATION.

  METHOD change_heading.
    DATA: compass_offset TYPE int4.

    " Any turn value other than a valid navigator turn will be ignored:
    CHECK turn EQ navigator=>left_turn
       OR turn EQ navigator=>right_turn
       OR turn EQ navigator=>u_turn.

    " Convert current heading to string offset:
    FIND me->heading IN navigator=>compass MATCH OFFSET compass_offset.

    " Adjust string offset based on turn
    CASE turn.
      WHEN navigator=>left_turn.
        SUBTRACT 01 FROM compass_offset.
      WHEN navigator=>right_turn.
        ADD 01 TO compass_offset.
      WHEN navigator=>u_turn.
        ADD 02 TO compass_offset.
    ENDCASE.

    " Adjust numeric value to accommodate underflow or overflow:
    IF compass_offset LT navigator=>compass_offset_limit_lo.
      ADD 04 TO compass_offset.
    ENDIF.
    IF compass_offset GT navigator=>compass_offset_limit_hi.
      SUBTRACT 04 FROM compass_offset.
    ENDIF.

    " Reset heading:
    me->heading = navigator=>compass+compass_offset(01).
  ENDMETHOD.

  METHOD get_heading.
    heading = me->heading.
  ENDMETHOD.

  METHOD constructor.
    " Any heading value other than a valid compass heading defaults to first:
    IF navigator=>compass CA heading.
      me->heading = heading.
    ELSE.
      me->heading = navigator=>compass+00(01).
    ENDIF.
  ENDMETHOD.
ENDCLASS.                    " navigator implementation

*----------------------------------------------------------------------
* Class: car implementation
*----------------------------------------------------------------------
CLASS car IMPLEMENTATION.

  METHOD accelerate.
    ADD acceleration TO me->speed.
  ENDMETHOD.

  METHOD change_heading.
    CALL METHOD me->navigation_unit->change_heading
      EXPORTING
        turn = turn.
  ENDMETHOD.

  METHOD get_characteristics.
    serial_number = me->serial_number.
    license_plate = me->license_plate.
    brand         = me->brand.
    model         = me->model.
    year          = me->year.
    color         = me->color.
    location      = me->location.
    speed_unit    = me->speed_unit.
  ENDMETHOD.

  METHOD get_heading.
    CALL METHOD me->navigation_unit->get_heading
      IMPORTING
        heading = heading.
  ENDMETHOD.

  METHOD get_speed.
    speed = me->speed.
  ENDMETHOD.

  METHOD constructor.
    " Assign unique serial to this instance
    CALL METHOD car=>get_serial_number
      IMPORTING
        serial_number = me->serial_number.

    me->license_plate = license_plate.
    me->brand         = brand.
    me->model         = model.
    me->year          = year.
    me->color         = color.
    me->location      = location.
    me->speed_unit    = speed_unit.

    " Create a navigator object for this car:
    CREATE OBJECT me->navigation_unit
      EXPORTING
        heading = heading.
  ENDMETHOD.

  METHOD class_constructor.
    car=>last_serial_value = 1000.  " default starting point
  ENDMETHOD.

  METHOD get_serial_number.
    ADD 01 TO car=>last_serial_value.
    serial_number = car=>last_serial_value.
  ENDMETHOD.
ENDCLASS.                    " car implementation

*----------------------------------------------------------------------
* Class: report implementation
*----------------------------------------------------------------------
CLASS report IMPLEMENTATION.

  METHOD build_report.
    DATA: output_entry    LIKE LINE OF report=>output_stack,
          car_entry       TYPE REF TO car.

    " Create output entries from all car objects
    LOOP AT report=>car_stack INTO car_entry.

      CALL METHOD car_entry->get_characteristics
        IMPORTING
          serial_number = output_entry-serial_number
          license_plate = output_entry-license_plate
          brand         = output_entry-brand
          model         = output_entry-model
          year          = output_entry-year
          color         = output_entry-color
          location      = output_entry-location
          speed_unit    = output_entry-speed_unit.

      CALL METHOD car_entry->get_heading
        IMPORTING
          heading = output_entry-heading.

      CALL METHOD car_entry->get_speed
        IMPORTING
          speed = output_entry-speed.

      APPEND output_entry TO report=>output_stack.
    ENDLOOP.
  ENDMETHOD.

  METHOD present_report.
    DATA: alv_grid TYPE REF TO cl_salv_table.

    " Create ALV grid:
    TRY.
        CALL METHOD cl_salv_table=>factory
          IMPORTING
            r_salv_table = alv_grid
          CHANGING
            t_table      = report=>output_stack.
      CATCH cx_salb_msg.
        MESSAGE e398(00) WITH 'Failure to create alv grid object' " #EC *
                             space
                             space
                             space.
    ENDTRY.

    " Set column titles:
    CALL METHOD report=>set_column_titles
      EXPORTING
        alv_grid = alv_grid.

    " Display ALV grid:
    CALL METHOD alv_grid->display.
  ENDMETHOD.

  METHOD register_car_entry.
    DATA: car_entry TYPE REF TO car.

    " Create a new object for tracking this car:
    CREATE OBJECT car_entry
      EXPORTING
        license_plate = license_plate
        brand         = brand
        model         = model
        year          = year
        color         = color
        location      = location
        speed_unit    = speed_unit
        heading       = heading.

    " Put this new car object in the car objects table:
    APPEND car_entry TO report=>car_stack.

    " Apply user-specified accelerations (three steps):
    CALL METHOD car_entry->accelerate
      EXPORTING acceleration = speed01.
    CALL METHOD car_entry->accelerate
      EXPORTING acceleration = speed02.
    CALL METHOD car_entry->accelerate
      EXPORTING acceleration = speed03.

    " Apply user-specified turns (three steps):
    CALL METHOD car_entry->change_heading
      EXPORTING turn = turn01.
    CALL METHOD car_entry->change_heading
      EXPORTING turn = turn02.
    CALL METHOD car_entry->change_heading
      EXPORTING turn = turn03.

    " Notify user that we have registered a car entry:
    MESSAGE s398(00) WITH 'Entry registered for'  " #EC *
                        license_plate
                        space
                        space.
  ENDMETHOD.

  METHOD set_column_titles.
    CONSTANTS: column_name_serial_number    TYPE lvc_fname VALUE 'SERIAL_NUMBER',
               column_title_serial_number   TYPE string    VALUE `Serial`,
               column_name_license_plate    TYPE lvc_fname VALUE 'LICENSE_PLATE',
               column_title_license_plate   TYPE string    VALUE `License plate`,
               column_name_brand            TYPE lvc_fname VALUE 'BRAND',
               column_title_brand           TYPE string    VALUE `Brand`,
               column_name_model            TYPE lvc_fname VALUE 'MODEL',
               column_title_model           TYPE string    VALUE `Model`,
               column_name_year             TYPE lvc_fname VALUE 'YEAR',
               column_title_year            TYPE string    VALUE `Year`,
               column_name_color            TYPE lvc_fname VALUE 'COLOR',
               column_title_color           TYPE string    VALUE `Color`,
               column_name_location         TYPE lvc_fname VALUE 'LOCATION',
               column_title_location        TYPE string    VALUE `Location`,
               column_name_heading          TYPE lvc_fname VALUE 'HEADING',
               column_title_heading         TYPE string    VALUE `Heading`,
               column_name_speed            TYPE lvc_fname VALUE 'SPEED',
               column_title_speed           TYPE string    VALUE `Speed`,
               column_name_speed_unit       TYPE lvc_fname VALUE 'SPEED_UNIT',
               column_title_speed_unit      TYPE string    VALUE `Unit`,
               minimum_column_width         TYPE int4      VALUE 08.

    DATA: grid_columns           TYPE REF TO cl_salv_columns_table,
          grid_column_stack      TYPE salv_t_column_ref,
          grid_column_entry      LIKE LINE OF grid_column_stack,
          grid_column_title_short TYPE scrtext_s,
          grid_column_width       TYPE lvc_outlen.

    " Set ALV grid column titles:
    CALL METHOD alv_grid->get_columns
      RECEIVING
        value = grid_columns.
    CALL METHOD grid_columns->get
      RECEIVING
        value = grid_column_stack.

    LOOP AT grid_column_stack INTO grid_column_entry.
      CLEAR grid_column_width.
      CASE grid_column_entry-columnname.
        WHEN column_name_serial_number.
          grid_column_title_short = column_title_serial_number.
        WHEN column_name_license_plate.
          grid_column_title_short = column_title_license_plate.
        WHEN column_name_brand.
          grid_column_title_short = column_title_brand.
        WHEN column_name_model.
          grid_column_title_short = column_title_model.
        WHEN column_name_year.
          grid_column_title_short = column_title_year.
        WHEN column_name_color.
          grid_column_title_short = column_title_color.
        WHEN column_name_location.
          grid_column_title_short = column_title_location.
        WHEN column_name_heading.
          grid_column_title_short = column_title_heading.
          grid_column_width       = minimum_column_width.
        WHEN column_name_speed.
          grid_column_title_short = column_title_speed.
          grid_column_width       = minimum_column_width.
        WHEN column_name_speed_unit.
          grid_column_title_short = column_title_speed_unit.
          grid_column_width       = minimum_column_width.
        WHEN OTHERS.
          CLEAR grid_column_title_short.
      ENDCASE.

      CALL METHOD grid_column_entry-r_column->set_short_text
        EXPORTING
          value = grid_column_title_short.

      IF grid_column_width GT 0.
        CALL METHOD grid_column_entry-r_column->set_output_length
          EXPORTING
            value = grid_column_width.
      ENDIF.
    ENDLOOP.
  ENDMETHOD.

  METHOD show_report.
    CALL METHOD: report=>build_report,
                  report=>present_report.
  ENDMETHOD.
ENDCLASS.                    " report implementation

*======================================================================*
*                                                                      *
*  S c r e e n   C o m p o n e n t s                                   *
*                                                                      *
*======================================================================*

*----------------------------------------------------------------------
* Selection screen definition
*----------------------------------------------------------------------
SELECTION-SCREEN: BEGIN OF BLOCK block_a WITH FRAME.
PARAMETERS: pplate   TYPE car=>license_plate_type,
            pbrand   TYPE car=>brand_type,
            pmodel   TYPE car=>model_type,
            pyear    TYPE car=>year_type,
            pcolor   TYPE car=>color_type,
            plocatn  TYPE car=>location_type,
            pheading TYPE navigator=>heading_type,
            pturn01  TYPE navigator=>turn_type,
            pturn02  TYPE navigator=>turn_type,
            pturn03  TYPE navigator=>turn_type,
            pspeedu  TYPE car=>speed_unit_type,
            pspeed01 TYPE car=>speed_type,
            pspeed02 TYPE car=>speed_type,
            pspeed03 TYPE car=>speed_type.
SELECTION-SCREEN: END OF BLOCK block_a.

*======================================================================*
*                                                                      *
*  C l a s s i c   P r o c e d u r a l   E v e n t s                   *
*                                                                      *
*======================================================================*

*----------------------------------------------------------------------
* Event: initialization
*----------------------------------------------------------------------
INITIALIZATION.
  SET PF-STATUS report=>selection_screen_status_name.

*----------------------------------------------------------------------
* Event: at selection-screen
*----------------------------------------------------------------------
AT SELECTION-SCREEN.
  CHECK sy-ucomm EQ report=>execute
     OR sy-ucomm EQ report=>add_new_car.

  CASE sy-ucomm.
    WHEN report=>add_new_car.
      CALL METHOD report=>register_car_entry
        EXPORTING
          license_plate = pplate
          brand         = pbrand
          model         = pmodel
          year          = pyear
          color         = pcolor
          location      = plocatn
          heading       = pheading
          turn01        = pturn01
          turn02        = pturn02
          turn03        = pturn03
          speed01       = pspeed01
          speed02       = pspeed02
          speed03       = pspeed03
          speed_unit    = pspeedu.
      " Implicitly returns to the initial selection screen.

    WHEN OTHERS.
      " No action; Execute will trigger start-of-selection.
  ENDCASE.

*----------------------------------------------------------------------
* Event: start-of-selection
*----------------------------------------------------------------------
START-OF-SELECTION.

*----------------------------------------------------------------------
* Event: end-of-selection
*----------------------------------------------------------------------
END-OF-SELECTION.
  CALL METHOD report=>show_report.


```


