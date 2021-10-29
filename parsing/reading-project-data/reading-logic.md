# Reading `logic`
In short, this `logic` file contains all the blocks of a sketchware project.

This file is structured by what I call as "containers". Each containers are separated from each other by double newlines, every containers starts off with a header that starts with the character `@` that contains information about the container (like, what activity (or screen) does this container live in and what is this container), then followed by lines of blocks or data represented as JSON and ends with an extra newline.

Example container in the wild:
```
@MainActivity.java_button_onClick
{"color":-10701022,"id":"10","nextBlock":-1,"opCode":"addSourceDirectly","parameters":["Toast.makeToast(this, "Hello World!", Toast.LENGTH_LONG)"],"spec":"add source directly %s.inputOnly","subStack1":-1,"subStack2":-1,"type":" ","typeName":""}
```

Structure of a container:
```
@MainActivity.java_button_onClick
---------------------------------
              |
     The container's header

{"color":-10701022, ... ,"typeName":""} |- Lines of blocks 
...                                     |
...                                     |
```

Structure of a header:
```
Header indicator          This is what I call as the "container info"
|                               |
v             -------------------
@MainActivity.java_button_onClick
 ------------^
 |           |
 |       Separator
 |
 On what activity is this container bound to
```

(We will discuss more about the block later)

## Types of containers
There are two types of containers, activity containers, and event implementation containers.

 - Activity containers

   An activity container is a container that CAN ONLY BE ONE in each activities, but they are optional.

   There are 5 types of activity containers:
   - Variable container (ends off with `.java_var`)
   - List variable container (ends off with `.java_list`)
   - Function / MoreBlock container (ends off with `.java_func`)
   - Component container (ends off with `.java_components`)
   - Event container (ends off with `.java_events`)

 - Event implementation containers

   An event implementation container is a container that contains blocks which implements an event that is declared in the event container of the current activity. The event which an event implementation container implements can be seen from its header's container info (after the dot).
