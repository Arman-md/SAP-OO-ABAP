# Intro- 
Singleton design pattern is one of the creational design pattern which ensures that the class has only one instance and provides global point of access to this object/instance.

# It solves mainly two problems–

Ensures that the class has only one instance
Provides global point of access to the instance
Usually when we want to create an object/instance of a class, then we can use Create Object / 
New operator to create a newly fresh instance of the class and we can create as many objects we want. But why is some cases we need to have to only instance of the class and not many?

# The uses cases may be- to access some shared resource.

A single database connection object can be shared by multiple objects in different part of the program.
A single Error/Log Manager object can write the messages in an application rather that creating multiple log manager objects.

# Implementations of the Singleton Class-

–>To prevent other objects from using the new operator with the Singleton class, make the constructor private.

–>Define a private static attribute in the “single instance” class and define a public static accessor method in the class. This method calls the private constructor to create an object and saves it in a static field.

–> Clients/Code may only use the accessor method to access the singleton class instance.

# ABAP Pseudocode-

``` abap
CLASS CL_LOG_MANAGER DEFINITION PUBLIC FINAL CREATE PRIVATE.
PUBLIC SECTION.
CLASS-METHODS get_instance RETURNING VALUE(ro_log) TYPE REF TO CL_LOG_MANAGER .
PRIVATESECTION.
CLASS-DATA go_log TYPE REF TO CL_LOG_MANAGER.
METHODS constructor.
PROTECTEDSECTION.
ENDCLASS.

CLASS CL_LOG_MANAGER IMPLEMENTATION.


METHOD get_instance.
IF go_log IS INITIAL. go_log = NEW #( ). ENDIF.
ro_log = go_log.
ENDMETHOD.

METHODconstructor.
“ Someinitialization
ENDMETHOD.

```

<img width="768" height="279" alt="image" src="https://github.com/user-attachments/assets/c0cdb996-3443-42df-bec3-55f340ef9140" />

ENDCLASS.

