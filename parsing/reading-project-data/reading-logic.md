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
   - [Event list container](#event-list-container) (ends off with `.java_events`)

 - Block containers

   A block container is a container that contains blocks which implements an event / moreblock that is declared in the event container (for events) / func container (for moreblocks) of the current activity / screen. The event / moreblock which this container implements can be seen from its header's container info (`@ActivityName.java_{}`).

   Simple words: An block container implements an event / moreblock

### Variable container
Variable container contains variables defined in the global scope of the current activity / screen.

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
A MoreBlock container contains all the information of every moreblocks that exists in the current activity / screen. Do note that its implementation / blocks are stored in a block container (that points to the moreblock defined here).

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
A component container contains all the components that exists in the current activity / screen, for example: Dialog, Intent, TextToSpeech, etc.

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

### Event list container
Quite self-explanatory, an event list container contains a list of events that are implemented in the current screen.

The items of this container is laid out the same as the component container. It's just a list of JSON in lines.

The JSON fields of an event list container:
| Type    | Name         | Description
| ------- | ------------ | -----------
| String  | `eventName`  | The name of the event
| Integer | `eventType`  | The type of the event (1: view event (ex: onClick), 2: component event (ex: onResponse), 3: activity event (ex: onResume))
| String  | `targetId`   | The target we want the event to be attached on. If this event is a view event, this will point to a view id. If this event is a component event, this will point to a component event. But, if this event is an activity event, this field is set the same as the event name (I don't know why)
| Integer | `targetType` | The component type of the target. Will be 0 if this event is not a component type.

An example event list container in the wild:
```
@MainActivity.java_events
{"eventName":"onClick","eventType":1,"targetId":"other_button","targetType":0}
{"eventName":"onCheckedChange","eventType":1,"targetId":"switch_theme","targetType":13}
{"eventName":"onResponse","eventType":2,"targetId":"ping_test","targetType":17}
{"eventName":"onErrorResponse","eventType":2,"targetId":"ping_test","targetType":17}
{"eventName":"onClick","eventType":1,"targetId":"my_button","targetType":0}
{"eventName":"onResume","eventType":3,"targetId":"onResume","targetType":0}
{"eventName":"onBackPressed","eventType":3,"targetId":"onBackPressed","targetType":0}
```
