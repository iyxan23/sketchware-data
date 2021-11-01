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
   - [Function / MoreBlock container](#moreblock-container) (ends off with `.java_func`)
   - [Component container](#component-container) (ends off with `.java_components`)
   - Event container (ends off with `.java_events`)

 - Block containers

   A block container is a container that contains blocks which implements an event / moreblock that is declared in the event container (for events) / moreblock / func container (for moreblocks) of the current activity. The event / moreblock which this container implements can be seen from its header's container info (`@ActivityName.{}`).

   Simple words: An event container declares that an event exists, and this type of containers basically implements that event with block code and same goes for moreblocks.

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

### MoreBlock container
A MoreBlock container contains all the information of every moreblocks that is included in the project. Do note that its implementation / blocks are stored in a block container (that points to the moreblock defined here).

A moreblock item is basically structured like this: `{name}:{spec}`, quite similar to a variable / list variable.

If you don't know, a spec is a **spec**ification of a block, [read this document for more information](../reading-spec.md)

An example of a moreblock container in the wild:
```
@MainActivity.java_func
setStatusBarColor:setStatusBarColor %s.color
setActionBarColor:setActionBarColor %s.color

@MainActivity.java_setStatusBarColor_moreBlock
{"color":-10701022, ... "typeName":""}
...
...

@MainActivity.java_setActionBarColor_moreBlock
{"color":-10701022, ... "typeName":""}
...
...
```

We parse this as:
```
void setStatusBarColor(String color) {
    // ... [insert implementation from the block container that implements this moreblock]
}

void setActionColor(String color) {
    // ... [insert implementation from the block container that implements this moreblock]
}
```

### Component container
A component container contains all the components that are indcluded in the project, for example: Dialog, Intent, TextToSpeech, etc.

The items of this container are basically JSON objects that represents every components that is included in the project.

The JSON fields of the items of a component container:
| Type    | Name          | Description |
| ------- | ------------- | ----------- |
| String  | `componentId` | The component name given by the user |
| String  | `param1`      | Contains information depending on the component type, see [this document](../../data/component-types.md) for more details |
| String  | `param2`      | Contains information depending on the component type, see [this document](../../data/component-types.md) for more details |
| String  | `param3`      | Contains information depending on the component type, see [this document](../../data/component-types.md) for more details |
| Integer | `type`        | The type of the current component, all component types can be seen [on this document](../../data/component-types.md) |

An example component container in the wild:
```
@MainActivity.java_components
{"componentId":"intent","param1":"","param2":"","param3":"","type":1}
{"componentId":"sp","param1":"file","param2":"","param3":"","type":2}
{"componentId":"dialog","param1":"file","param2":"","param3":"","type":7}
```

Expected result:
```
Intent intent;
SharedPreferences sp;
AlertDialog.Dialog dialog;

// somewhere in initialization
sp = getSharedPreferences("file", Context.MODE_PRIVATE);
```
