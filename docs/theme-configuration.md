---
title: Scripts
date: 2022-03-17
slug: scripts

---
## Scripts

Scripts in the [console](https://console.tabahi.tech/#scripts) are executed in a javascript container in order to process computations on the console cloud. Scripts only support basic javascript functions, `node`class functions to parse data to and from devices, and `script` class functions for debugging purposes.

### Arguments

While executing a script, arguments aren't required unless some device-specific interface is needed. Alternatively, arguments can be strings of data themselves thus skipping any need for fetching data from device databases.

```javascript
if(args)
{
  	if(args.abc) script.log(args.abc);
    if(args.NT)
    {
        print(args.NT);
      	script.log(args.NT);
    }
    else print("No NT argument given");
    //to test, pass arguments as:
    //where NT is the NODE_TOKEN as argument
}
```

### Script Logs

Script logs are for debugging purposes and can only be viewed on the console when the Debug button is pressed. In comparison, `print()`prints the data as the externally viewable output of the script.

```javascript
script.log(new Date() + "\t Test script");//log time and date of run
script.log("Args: ", args); //show the arguments passed to this script

print("This is published on run");
```

### Interfacing with Devices

Scripts can read, set variables, and get single or multiple data rows from the device database using `NODE_TOKEN` or `NT`. Scripts can help to perform the switching of variables after analyzing rows of data because small devices can't hold a lot of data in their memory.

```javascript

//get the NODE_TOKEN from the argumenets:
var NT = args.NT;

let variables = await node.getVariables(NT);
script.log("Variables:"); script.log(variables);

//setting a boolean variable
await node.setVariable(NT, 'heater', 'b', new_heater);

//setting an integer variable
await node.setVariable(NT, 'init', 'i', 100);

//setting a float variable (constant)
await node.setVariable(NT, 'init', 'f', 100, 1); //1:constant, 0: not-constant

//setting multiple variables:
await node.setVariables(NT, [{name:"var1", type:"i", value:10, constant:0}, {name:"var2", type:"f", value:20.6, constant:1}]);

//Get latest data row from last 0.5 hour:
let data = await node.getData(NT, 'latest', 0.5);
script.log("Data:"); script.log(data);

//Get multiple data rows from last 3 hours:
let data_rows = await node.getData(NT, 'multiple', 3);
script.log("Data:"); script.log(data_rows);

//add a new data row:
await pushData(NT, {"air": 0.5, "surfacer": 3.2});
```