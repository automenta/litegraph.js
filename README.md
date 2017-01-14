# litegraph.js

A library in Javascript to create graphs in the browser similar to PD. Nodes can be programmed easily and it includes an editor to construct the graphs.

It can be integrated easily in any existing web applications and graphs can be run without the need of the editor.

## Creating a Graph ##

You can create graphs from the editor (and store them in JSON) or directly from code:

```javascript

var graph = new LGraph();
var node = LiteGraph.createNode("basic/const");
var node2 = LiteGraph.createNode("basic/watch");
graph.add( node );
graph.add( node2 );
node.connect(0, node2, 0); //connect node slot 0 to node2 slot 0

graph.runStep(1); //execute one cycle
```

## How to code a new Node type

Here is an example of how to build a node that sums two inputs:

```javascript
//node constructor class
function MyAddNode()
{
  this.addInput("A","number");
  this.addInput("B","number");
  this.addOutput("A+B","number");
}

//name to show
MyAddNode.title = "Sum";

//function to call when the node is executed
MyAddNode.prototype.onExecute = function()
{
  var A = this.getInputData(0);
  if( A === undefined )
    A = 0;
  var B = this.getInputData(1);
  if( B === undefined )
    B = 0;
  this.setOutputData( 0, A + B );
}

//register in the system
LiteGraph.registerNodeType("basic/sum", MyAddNode );

```


## Projects using it

### [webglstudio.org](http://webglstudio.org)

![WebGLStudio](imgs/webglstudio.gif "WebGLStudio")

### [MOI Elephant](http://moiscript.weebly.com/elephant-systegraveme-nodal.html)

![MOI Elephant](imgs/elephant.gif "MOI Elephant")

### [Mynodes.NET](http://www.mynodes.net)

![MyNodes.NET](imgs/mynodes.png "MyNodes.NET")

## Utils
-----

It includes several commands in the utils folder to generate doc, check errors and build minifyed version.

# LiteGraph

Here is a list of useful info when working with LiteGraph

## LGraphNode

LGraphNode is the base class used for all the nodes classes.
To extend the other classes all the methods contained in LGraphNode.prototype are copyed to the classes when registered.

### Node slots

Every node could have several slots, stored in node.inputs and node.outputs.

You can add new slots by calling node.addInput or node.addOutput

The main difference between inputs and outputs is that an input can only have one connection link while outputs could have several.

To get information about an slot you can access node.inputs[ slot_index ]  or node.outputs[ slot_index ]

Slots have the next information:

 * **name**: string with the name of the slot (used also to show in the canvas)
 * **type**: string specifying the data type traveling through this link
 * **link or links**: depending if the slot is input or ouput contains the id of the link or an array of ids
 * **label**: optional, string used to rename the name as shown in the canvas.
 
 To retrieve the data traveling through a link you can call node.getInputData or node.getOutputData


## Feedback
--------

You can write any feedback to javi.agenjo@gmail.com
