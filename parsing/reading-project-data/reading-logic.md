# Reading `logic`
In short, this `logic` file contains all the blocks of a sketchware project.

This file is structured by what I call as "containers". Each containers are separated from each other, every containers starts with a header (which starts with the character `@`), it contains information about the container (like, what activity (or screen) does this container live in and what is this container), then followed by lines of blocks or a specific type of data (depends on the container type) represented as JSON and ends with an extra newline.

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

{"color":-10701022, ... ,"typeName":""} |- Lines of blocks / data depending on the container type
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
   - [Variable container](#variable-container) (ends off with `.java_var`)
   - [List variable container](#list-container) (ends off with `.java_list`)
   - Function / MoreBlock container (ends off with `.java_func`)
   - Component container (ends off with `.java_components`)
   - Event container (ends off with `.java_events`)

 - Event implementation containers

   An event implementation container (EIC for short) is a container that contains blocks which implements an event that is declared in the event container of the current activity. The event which an EIC implements can be seen from its header's container info (after the dot).

   Simple words: An event container declares that an event exists, and EIC basically implements that event with block code

### Variable container
Variable container contains variables defined in the global scope.

A variable is structured like this: `{type}:{name}`. Do note that the type is an number representing a type. Here are all the variable types:

Number | Type
------ | -------
0      | boolean
1      | integer
2      | String  
3      | Map (more specifically, `HashMap<String, Object>` or a map of objects with the key type of String)


An example of a variable container in the wild:
```
@MainActivity.java_var
0:is_bluetooth_on
0:is_wifi_on
2:current_connected_wifi
1:available_wifi_count
1:available_bluetooth_count
```

We parse this as:
```java
boolean is_bluetooth_on;
boolean is_wifi_on;
String current_connected_wifi;
int available_wifi_count;
int available_bluetooth_count;
```

### List container
A list container is basically the same as a variable container, but instead of storing single-value variables, it stores list of their type.

A "list variable" is structured the same as a variable in a variable container: `{type}:{name}`. Do note that the type is a number representing a type. Variable types are the same as well, but the difference that they are lists instead of single-value variables:

Number | Type
------ | -------
0      | List of booleans (`ArrayList<Boolean>`)
1      | List of integers (`ArrayList<Integer>`)
2      | List of Strings (`ArrayList<String>`)
3      | List of Maps (`ArrayList<HashMap<String, Object>>`)

An example of a list container in the wild:
```
@MainActivity.java_list
2:wifi_names
2:bluetooth_devices
```

We parse this as:
```java
ArrayList<String> wifi_names = new ArrayList<>();
ArrayList<String> bluetooth_names = new ArrayList<>();
```
