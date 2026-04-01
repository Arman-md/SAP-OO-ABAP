
# Communicating Design Through UML 🌐

We are leaving the terrain of basic object-oriented principles and entering the galaxy of **Design Patterns**.  
To navigate this vast expanse, we need **celestial mapping and cosmic diagramming** — this is where **Unified Modeling Language (UML)** comes in.

---

## 🌟 What is UML?

- **Unified Modeling Language (UML)** was created in **1996** by:
  - **James Rumbaugh**
  - **Grady Booch**
  - **Ivar Jacobson**  
  *(a.k.a. The Three Amigos)*  
- They consolidated:
  - **OMT** (Object Modeling Technique)
  - **OOD** (Object-Oriented Design)  
- Adopted in **1997** by the **Object Modeling Group (OMG)** as a **non-proprietary standard** for software engineering.

---

## 📜 Current UML Standard
- **Version:** 2.5 (June 2015)
- Defines **14 types of diagrams**, divided into:
  - **Structural diagrams** (class, component, deployment, etc.)
  - **Behavioral diagrams** (sequence, activity, state machine, etc.)

---

## ✅ Focus for Our Journey
A full UML explanation is beyond scope, so we’ll focus on the **Class Diagram**, which:
- Organizes and depicts **classes and interfaces**
- Shows **attributes, behaviors**
- Illustrates **relationships** between entities

---

## 🧩 Why UML?
- **Visual communication** of design
- Bridges gap between **conceptual design** and **implementation**
- Helps teams **collaborate effectively**


---

## 🌌 Key Takeaways
- UML is our **navigation tool** for exploring advanced design patterns.
- **Class diagrams** will be our primary map for depicting OO structures.
- This is the **flight training** before we reach the stars of **Design Patterns**.

---
<img width="863" height="717" alt="image" src="https://github.com/user-attachments/assets/097ae9f2-e238-4ec6-acdb-df69fd4b8ce0" />

### UML Diagram Types (Hierarchy)
- **Structural**
  - Class Diagram
  - Component Diagram
  - Deployment Diagram
  - Object Diagram
  - Package Diagram
- **Behavioral**
  - Sequence Diagram
  - Activity Diagram
  - State Machine Diagram
  - Use Case Diagram
  - Communication Diagram

---

> **From Objectropolis to the Galaxy of Design Patterns — UML is our star map.**



# UML Class Diagrams 📦

<img width="863" height="160" alt="image" src="https://github.com/user-attachments/assets/e3026291-179f-4e5f-83e6-f40afe95be0b" />


A **UML Class Diagram** represents classes and interfaces using **boxes divided into three sections**:

1. **Top Section**: Class or interface name (centered)
2. **Middle Section**: Attributes
3. **Bottom Section**: Behaviors (methods)

Boxes are connected by **relationship lines** to show associations.

---

## ✅ Box Structure

- **Class Name**: Centered in the top section
- **Interface Name**: Preceded by `<<interface>>`
- **Attributes**:
  - Left-justified
  - Format: `visibility name : type = defaultValue`
- **Behaviors**:
  - Left-justified
  - Format: `visibility methodName(paramName : type) : returnType`
  - `void` indicates no return value
- **Abstract entries**: *Italicized*
- **Camel Case**: Use **lowerCamelCase** for names

---

### Visibility Indicators
- `+` Public  
- `-` Private  
- `#` Protected  
- `~` Package  
- `/` Derived (can combine with others)  
- `_` Static (combine with others)  

---

## 🔗 Relationships Between Classes
Three categories:
1. **Class-Level Relationships**
   - **Generalization**: Solid line + unfilled triangular arrowhead → parent class  
     *(represents “is-a” relationship, inheritance)*
   - **Realization**: Dashed line + unfilled triangular arrowhead → interface  
     *(represents “implements” relationship)*
2. **Instance-Level Relationships**
   - Associations, aggregations, compositions
3. **General Relationships**
   - Dependencies, navigability, etc.

---

<img width="750" height="305" alt="image" src="https://github.com/user-attachments/assets/1bea2c62-e5b9-41de-9c77-dcf703d415f4" />




## 🖼 Example: Car Class & simpleNavigation Interface



# UML Instance-Level Relationships 🔗

Instance-level relationships (links) depict how **objects** relate to one another.  
There are **three main types**, each stronger than the previous:

---

## ✅ Types of Instance-Level Relationships

### 1. **Association** — “relates to”
- Represents a general connection between two entities.
- **Variations**:
  - **Unidirectional**: One entity knows about the other.  
    Example: `vehicleRegistrationAgency → vehicle`
    - Represented by a **solid line with an arrowhead** pointing to the entity that does **NOT** know the other.
  - **Bidirectional**: Both entities know each other.  
    Example: `patient ↔ physician`
    - Represented by a **solid line** (no arrowhead).
  - **Reflexive**: A class relates to itself.  
    Example: `employee ↔ manager` (both are employees)
    - Represented by a **solid line looping back to the same class box**.

---



### 2. **Aggregation** — “has a”
- Represents a **whole-part** relationship where the whole **contains** parts.
- **Independent lifecycle**: When the whole is destroyed, parts **remain alive**.
- Example: `Pond has Ducks` → Ducks fly away if pond is drained.
- **Notation**: Solid line with **unfilled diamond** at the end pointing to the **aggregator**.

---

### 3. **Composition** — “owns a”
- Represents a **strong whole-part** relationship.
- **Dependent lifecycle**: When the whole is destroyed, parts are **destroyed too**.
- Example: `Car owns Carburetor` → Destroy car → carburetor destroyed.
- **Notation**: Solid line with **filled diamond** at the end pointing to the **composer**.

---

## 🔍 Aggregation vs Composition
| Aspect        | Aggregation (“has a”) | Composition (“owns a”) |
|--------------|------------------------|-------------------------|
| Lifecycle    | Independent           | Dependent              |
| Example      | Pond → Duck           | Car → Carburetor       |
| UML Symbol   | ◇ (unfilled diamond)  | ◆ (filled diamond)     |

---

<img width="750" height="580" alt="image" src="https://github.com/user-attachments/assets/9ce1ba5c-3e35-4c4d-88d3-608c13d203ff" />


## 🔢 Cardinality (Multiplicity)
Indicates **how many instances** can participate in the relationship:
- `0..1` → Zero or one
- `1` → Exactly one
- `0..*` → Zero or more
- `1..*` → One or more
- Explicit ranges: `0..4`, `5`, `5..9`, `6..*`

**Examples**:
- Car → Engine: `1` to `1` (composition)
- Car → Supercharger: `1` to `0..1` (optional composition)
- ParkingLot → Car: `1` to `0..*` (aggregation)

---

## 🖼 UML PlantUML Examples

### Association (Unidirectional)
```plantuml
@startuml
class Vehicle
class VehicleRegistrationAgency
VehicleRegistrationAgency --> Vehicle : registers
@enduml
```


# UML General Relationships 🔗

A **general relationship** in UML is called a **Dependency**.  
It represents a connection where **one entity depends on another entity (the supplier)** for its implementation.

---

## ✅ Dependency Relationship
- **Meaning**: “depends on”
- **Examples of dependency types**:
  - `<<uses>>`
  - `<<calls>>`
  - `<<instantiates>>`
- **Notation**:
  - **Dashed line** with an **open arrowhead** pointing to the **supplier**
  - Dependency type is shown in **guillemets** (`<< >>`) next to the line

---

### UML Representation


<img width="751" height="152" alt="image" src="https://github.com/user-attachments/assets/58e20d02-261c-42f9-ac8f-405d8e97ed32" />



# UML Class Diagram Example: Fox & Dog 🦊🐶

This example demonstrates how to represent classes, attributes, behaviors, and relationships using **UML Class Diagrams**.

---

## ✅ Description of Classes

### **Fox Class**
- **Attributes**:
  - `- alacrity : String`
  - `- color : String`
- **Behaviors**:
  - `+ jump(otherInstance : Object) : void`
  - `+ setAlacrity(alacrity : String) : void`
  - `+ setColor(color : String) : void`

---

### **Dog Class**
- **Attributes**:
  - `- alacrity : String`
  - `- registrationNumber : num`
  - `_ - lastUsedRegistrationNumber : num` *(static private)*
- **Behaviors**:
  - `_ - getNextRegistrationNumber() : num` *(static private)*
  - `+ setAlacrity(alacrity : String) : void`
  - `+ setRegistrationNumber() : void`

---

## 🔗 Relationship
- **General Relationship (Dependency)**:
  - **Fox depends on Dog** (`<<uses>>`)
  - Fox needs a Dog instance to perform `jump()`
  - Represented by a **dashed line with open arrowhead** pointing to **Dog**

---

<img width="863" height="185" alt="image" src="https://github.com/user-attachments/assets/a5393760-5b27-4d55-a145-be1d08ef2d63" />


## 🖼 UML Diagram (PlantUML)

```plantuml
@startuml
class Fox {
  - alacrity : String
  - color : String
  + jump(otherInstance : Object) : void
  + setAlacrity(alacrity : String) : void
  + setColor(color : String) : void
}

class Dog {
  - alacrity : String
  - registrationNumber : num
  _ - lastUsedRegistrationNumber : num
  _ - getNextRegistrationNumber() : num
  + setAlacrity(alacrity : String) : void
  + setRegistrationNumber() : void
}

Fox ..> Dog : <<uses>>
@enduml


```


<img width="863" height="467" alt="image" src="https://github.com/user-attachments/assets/1504750b-edf3-4e94-9b89-3ac9728a5c27" />


# UML Class Diagram Example: Report, Vehicle & Navigation System 🚗🛰️

This UML diagram illustrates **abstract classes**, **interfaces**, **concrete classes**, and their relationships.

---

## ✅ Class Definitions
1. **report**  
   - **Static Abstract Class** → Name in *italic*  
   - Owns instances of `vehicle` classes  
2. **vehicle**  
   - **Abstract Class** → Name in *italic*  
   - Parent of `car` and `truck`  
   - Owns instances of classes implementing `simple_navigation`  
3. **car**  
   - **Concrete Class** → Name in regular font  
   - Inherits from `vehicle`  
4. **truck**  
   - **Concrete Class** → Name in regular font  
   - Inherits from `vehicle`  
5. **<<interface>> simple_navigation**  
   - Interface → Name in *italic* with `<<interface>>` banner  
   - Defines abstract methods for navigation  
6. **navigator**  
   - Concrete class implementing `simple_navigation`  
7. **gps**  
   - Concrete class implementing `simple_navigation`  
8. **dead_reckoning**  
   - Concrete class implementing `simple_navigation`  

---

## 🔗 Relationships
- **Implements (Realization)**:  
  - `navigator`, `gps`, `dead_reckoning` → `simple_navigation`  
  - Represented by **dashed line with unfilled triangular arrowhead** pointing to interface  
- **Inheritance (Generalization)**:  
  - `car`, `truck` → `vehicle`  
  - Represented by **solid line with unfilled triangular arrowhead** pointing to parent  
- **Composition (“owns a”)**:  
  - `report` → `vehicle`  
    - Cardinality: `report (1)` → `vehicle (0..*)`  
  - `vehicle` → `simple_navigation`  
    - Cardinality: `vehicle (1)` → `simple_navigation (1)`  
  - Represented by **solid line with filled diamond arrowhead** pointing to owning class  

---

## 🔢 Cardinality
- `report` → `vehicle`: `1` to `0..*`  
- `vehicle` → `simple_navigation`: `1` to `1`  

---

## 🖼 UML Diagram (PlantUML)

```plantuml
@startuml
' Abstract and static classes in italic
abstract class report <<static>> {
}

abstract class vehicle {
}

class car {
}

class truck {
}

interface simple_navigation {
}

class navigator {
}

class gps {
}

class dead_reckoning {
}

' Relationships
report *-- "0..*" vehicle : owns
vehicle *-- "1" simple_navigation : owns
vehicle <|-- car
vehicle <|-- truck
navigator ..|> simple_navigation
gps ..|> simple_navigation
dead_reckoning ..|> simple_navigation
@enduml
``

```

✅ 1. Understanding Ownership in Your UML
A. report *-- "0..*" vehicle

This is a composition (shown by the filled diamond *--).
Meaning:

A report owns vehicles.
A vehicle cannot exist without the report that owns it.
Cardinality "0..*" means:

A report can have zero or many vehicles.



```

➡️ Simple explanation:
If a report is deleted, all the vehicles inside it also disappear.

B. vehicle *-- "1" simple_navigation

Also a composition.
Meaning:

A vehicle owns exactly one simple_navigation object.
That navigation subsystem is a part of the vehicle.
Without the vehicle, the navigation system doesn’t exist.



➡️ Simple explanation:
Every vehicle must have one internal navigation system, and that navigation system cannot live on its own outside the vehicle.

✅ 2. Inheritance (Generalization)

vehicle <|-- car
vehicle <|-- truck

- `car` and `truck` **inherit** from `vehicle`.
- Meaning:
  - Both are *special types* of vehicles.

➡️ **Simple explanation:**  
A car **is a** vehicle.  
A truck **is a** vehicle.

---

# ✅ **3. Interface Realization**

### ```
navigator ..|> simple_navigation
gps ..|> simple_navigation
dead_reckoning ..|> simple_navigation


All three classes implement the simple_navigation interface.
Meaning:

navigator, gps, and dead_reckoning provide navigation functionality defined by simple_navigation.



➡️ Simple explanation:
They all follow the same navigation contract, but provide their own way of doing navigation.

✅ 4. Summary of Relationship Types in Your UML
Composition (*--)

Strongest form of ownership.
Part–whole relationship.
Lifetimes are linked: part dies with whole.

In your diagram:

report → vehicles
vehicle → simple_navigation (one)


Generalization (<|--)

Inheritance / "is-a" relationship.

In your diagram:

car is a vehicle
truck is a vehicle


Interface Realization (..|>)

Class implements an interface.

In your diagram:

navigator, gps, dead_reckoning implement simple_navigation.

```
# UML Summary ✅

In this chapter, we explored the **Unified Modeling Language (UML)** and its role in communicating design.

---

## 🧠 Key Learnings

### 1. **Origins of UML**
- Created in **1996** by **James Rumbaugh**, **Grady Booch**, and **Ivar Jacobson** (The Three Amigos).
- Unified **OMT** (Object Modeling Technique) and **OOD** (Object-Oriented Design).
- Adopted in **1997** by the **Object Modeling Group (OMG)**.

---

### 2. **Class Diagram Basics**
- Represents a **class** as a **box with three sections**:
  - **Top**: Class name (italic for abstract, `<<interface>>` for interfaces)
  - **Middle**: Attributes
  - **Bottom**: Behaviors (methods)
- **Notation**:
  - Lower **camelCase** for names
  - Visibility indicators:
    - `+` Public
    - `-` Private
    - `#` Protected
    - `~` Package
    - `_` Static
    - `/` Derived
- Abstract entries → *italic font*

---

### 3. **Relationship Categories**
- **Class-Level Relationships**:
  - **Generalization** (`is-a`): Solid line + unfilled triangle → inheritance
  - **Realization** (`implements`): Dashed line + unfilled triangle → interface implementation
- **Instance-Level Relationships**:
  - **Association** (`relates to`): Solid line (uni/bidirectional/reflexive)
  - **Aggregation** (`has a`): Solid line + unfilled diamond → independent lifecycle
  - **Composition** (`owns a`): Solid line + filled diamond → dependent lifecycle
  - **Cardinality**: `1`, `0..*`, `1..*`, or explicit ranges (`0..4`, `5..9`)
- **General Relationships**:
  - **Dependency** (`depends on`): Dashed line + open arrowhead → supplier
  - Annotated with `<<uses>>`, `<<calls>>`, `<<instantiates>>`

---

## ✅ Why UML Matters
- Provides a **visual language** for object-oriented design.
- Bridges the gap between **conceptual design** and **implementation**.
- Essential for **design patterns**, **architecture**, and **team collaboration**.

---

> UML is the **blueprint** for object-oriented systems, enabling clear communication of structure and behavior.
