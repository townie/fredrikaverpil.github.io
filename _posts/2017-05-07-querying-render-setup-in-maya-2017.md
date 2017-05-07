---
layout: post
title: Querying Render Setup in Maya 2017
tags: [python, maya]
---

Here's a bunch of ways you can query render layers in Maya 2017.

<!--more-->


## MEL

```
$renderLayerNames = `renderSetup -q -renderLayers`;
```


## Python


### Render layer names

```python
import maya.cmds as cmds

render_layer_names = cmds.renderSetup(q=True, renderLayers=True)
```

### Render layer names and their renderability

```python
import maya.app.renderSetup.model.renderSetup as renderSetup

render_setup = renderSetup.instance()
render_layers = render_setup.getRenderLayers()

for render_layer in render_layers:
    render_layer_name = render_layer.name()
    is_renderable = render_layer.isRenderable()
    print(render_layer_name, is_renderable)
```


## Exploring Render Setup functions

It seems Autodesk did not create a Render Setup documentation. If you run the following, you're going to get all the callable functions of `render_setup`:

```python
import maya.app.renderSetup.model.renderSetup as renderSetup

render_setup = renderSetup.instance()

for member in dir(render_setup):
    function = getattr(render_setup, member)
    if callable(function):
        print(member)
```

This is what I get with Maya 2017 Update 3:

```
__class__
__delattr__
__format__
__getattribute__
__hash__
__init__
__new__
__reduce__
__reduce_ex__
__repr__
__setattr__
__sizeof__
__str__
__subclasshook__
__weakref__
_afterDuplicate
_afterLoadReferenceCB
_afterOpenCB
_afterUnloadReferenceCB
_beforeDuplicate
_beforeLoadReferenceCB
_beforeSaveSceneCB
_beforeUnloadReferenceCB
_cleanObservers
_decodeChildren
_decodeProperties
_encodeProperties
_getBackAttr
_getFrontAttr
_getListItemsAttr
_getNotesPlug
_hasNotesPlug
_notifyActiveLayerObservers
_onMayaNodeAddedCB
_onNodeRemoved
_preRenderLayerDelete
_switchToLayerFileIO
acceptImport
addActiveLayerObserver
addAttribute
addExternalContentForFileAttr
addListObserver
ancestors
appendChild
appendRenderLayer
attachChild
attachRenderLayer
attributeAffects
clearAll
clearListObservers
compute
connectionBroken
connectionMade
copyInternalData
createRenderLayer
creator
decode
dependsOn
detachChild
detachRenderLayer
dispose
doNotWrite
encode
forceCache
getBack
getChildren
getDefaultRenderLayer
getExternalContent
getFilesToArchive
getFront
getInternalValueInContext
getNotes
getRenderLayer
getRenderLayers
getVisibleRenderLayer
hasActiveLayerObserver
inheritAttributesFrom
initListItems
initializer
internalArrayCount
isAbstractClass
isAcceptableChild
isPassiveOutput
itemAdded
itemRemoved
legalConnection
legalDisconnection
name
parent
passThroughToMany
passThroughToOne
postConstructor
removeActiveLayerObserver
removeListObserver
setBack
setDependentsDirty
setDoNotWrite
setExternalContent
setExternalContentForFileAttr
setFront
setInternalValueInContext
setMPSafe
setNotes
shouldSave
switchToLayer
switchToLayerUsingLegacyName
thisMObject
type
typeId
typeName
```

By accessing `__doc__` of each member, we can access its docstring which could potentially help explain how the function works. Also, the built-in [`help()`](https://docs.python.org/2/library/functions.html#help) Python function could shed some additional light...

The following prints all functions and any documentation in markdown which can be copy-pasted to a gist for (some) readability.

```python
import maya.app.renderSetup.model.renderSetup as renderSetup

render_setup = renderSetup.instance()  
callable_functions = {}

for member in dir(render_setup):
    function = getattr(render_setup, member)
    if callable(function):
        function_name = member
        callable_functions[function_name] = function

# Index
print('## Index')
for function_name in sorted(callable_functions):
        if not function_name.startswith('_'):
            print('<a href="#' + function_name + '">`' + function_name + '`</a>')

# Functions
print('# Callable')
for function_name, function in sorted(callable_functions.items()):
    if not function_name.startswith('_'):
        print('## `' + function_name + '`')

        print('**`' + function_name + '.__doc__`**')
        print('```')
        print(function.__doc__)
        print('```')
                
        print('**`help(' + function_name + ')`**')
        print('```')
        print(help(function))
        print('```')       
        
        print('\n<br><br>\n')
```

This is what I get with Maya 2017 Update 3:

[https://gist.github.com/fredrikaverpil/510d661e4467ef4acaa0004e29c30213](https://gist.github.com/fredrikaverpil/510d661e4467ef4acaa0004e29c30213)



## Exploring Render layer functions

Just like how we look inside of the render setup object, we can look into a render layer object and find out what functions are available.

I'll try to add this to this blog post and create another gist in a couple of days.


### What tricks are you using?

Please use the comments below to share any findings! :)
