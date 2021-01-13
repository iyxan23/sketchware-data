# Sketchware Opcodes
Valid Block OpCodes of Original Sketchware

### What are `logic_opcodes`?
`logic_opcodes` is basically a list of block opcodes, it can be found / read by decrypting the `data/logic` file of the project with the key "opCode", example:
```
@MainActivity.java_onCreate_initializeLogic
{"color":-10701022,"id":"12","nextBlock":10,"opCode":"addSourceDirectly","parameters":["// test"],"spec":"add source directly %s.inputOnly","subStack1":-1,"subStack2":-1,"type":" ","typeName":""}
{"color":-7711273,"id":"10","nextBlock":13,"opCode":"definedFunc","parameters":["cat /proc/cpuinfo"],"spec":"execute_shell %s.command","subStack1":-1,"subStack2":-1,"type":" ","typeName":""}
```

### What are `view_types`?
`view_types` is a list of view types, yeah explanations, it can be found by decrypting the `data/view` file of the project with the key "type", example:
```
{"adSize":"","adUnitId":"","alpha":1.0,"checked":0,"choiceMode":0,"clickable":1,"customView":"","dividerHeight":1,"enabled":1,"firstDayOfWeek":1,"id":"vscroll1","image":{"rotate":0,"scaleType":"CENTER"},"indeterminate":"false","index":0,"layout":{"backgroundColor":16777215,"gravity":0,"height":-2,"layoutGravity":0,"marginBottom":8,"marginLeft":0,"marginRight":0,"marginTop":0,"orientation":-1,"paddingBottom":0,"paddingLeft":0,"paddingRight":0,"paddingTop":0,"weight":1,"weightSum":0,"width":-1},"max":100,"parent":"root","parentType":0,"preId":"vscroll1","preIndex":0,"preParentType":0,"progress":0,"progressStyle":"?android:progressBarStyle","scaleX":1.0,"scaleY":1.0,"spinnerMode":1,"text":{"hint":"","hintColor":-10453621,"imeOption":0,"inputType":1,"line":0,"singleLine":0,"text":"","textColor":-16777216,"textFont":"default_font","textSize":12,"textType":0},"translationX":0.0,"translationY":0.0,"type":12}
```
