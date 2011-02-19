--- 
layout: docs 
title: Event 
categories: [Documentation]
---

Module: Event {#Event}
===========================

Provides the [Events](event.html) object to bind events to the canvas to interact with 3D objects. 
The first parameter of each event callback function is an event wrapper object that contains as properties:

* event - (*element*) The native event.
* x - (*number*) The x position of the mouse pointer when the event was triggered.
* y - (*number*) The y position of the mouse pointer when the event was triggered.
* stop - (*function*) A method that can be called to stop the propagation of the event.
* wheel - (*number*) Only on the mousewheel event. A number specifying the delta for the mouse scroll.
* isRightClick - (*boolean*) Whether is right or left click.
* code - (*number*) Available onKeyDown only. The key code number.
* key - (*string*) Available onKeyDown only. The key pressed as a string. Can also be `enter`, `up`, `down`, `left`, `right`, `backspace`, `space`, `delete` and `esc`.
* shift - (*boolean*) Available onKeyDown only. Whether the shift key is pressed.
* control - (*booleanr*) Available onKeyDown only. Whether the control key is pressed.
* alt - (*boolean*) Available onKeyDown only. Whether the alt key is pressed.
* meta - (*boolean*) Available onKeyDown only. Whether the meta key is pressed.


Events Method: create {#Events:create}
----------------------------------------------------

Creates a set of events for the given domElement that can be handled through a callback.

### Syntax:

    PhiloGL.Events.create(domElement, options);	

### Arguments:

1. domElement  - (*element*) A domElement. Generally a canvas element.
5. options - (*object*) An object containing the following options:

### Options:

* cachePosition - (*boolean*, optional) Whether to cache the current position of the canvas or calculate it each time in the event loop. Default's `true`.
* cacheSize - (*boolean*, optional) Whether to cache the size of the canvas or calculate it each time in the event loop. Default's `true`.
* relative - (*boolean*, optional) Whether to calculate the mouse position as relative to the canvas position or absolute. Default's `true`.
* centerOrigin - (*boolean*, optional) Whether to set the center (0, 0) coordinate to the center of the canvas or to the top-left corner. Default's `true`.
* disableContextMenu - (*boolean*, optional) Disable the context menu (generally shown when the canvas is right clicked). Default's `true`.
* bind - (*mixed*, optional) bind the *thisArg* in the callbacks to the specified object.
* onClick - (*function*, optional) Handles the onClick event.
* onRightClick - (*function*, optional) Handles the onRightClick event.
* onDragStart - (*function*, optional) Handles the onDragStart event.
* onDragMove - (*function*, optional) Handles the onDragMove event.
* onDragEnd - (*function*, optional) Handles the onDragEnd event.
* onDragCancel - (*function*, optional) Handles the onDragCancel event.
* onTouchStart - (*function*, optional) Handles the onTouchStart event.
* onTouchMove - (*function*, optional) Handles the onTouchMove event.
* onTouchEnd - (*function*, optional) Handles the onTouchEnd event.
* onTouchCancel - (*function*, optional) Handles the onTouchCancel event.
* onMouseMove - (*function*, optional) Handles the onMouseMove event.
* onMouseEnter - (*function*, optional) Handles the onMouseEnter event.
* onMouseLeave - (*function*, optional) Handles the onMouseLeave event.
* onMouseWheel - (*function*, optional) Handles the onMouseWheel event.
* onKeyDown - (*function*, optional) Handles the onKeyDown event.
* onKeyUp - (*function*, optional) Handles the onKeyUp event.

### Notes:

Even though the *Events* object is accessible via the PhiloGL function the events are often set in the PhiloGL constructor. For more information about 
the PhiloGL constructor check the [Core](core.html) Script.

### Examples:

Setting rotation and zoom to a moon object with drag and drop and mousewheel events.

{% highlight js %}
    var pos, camera, moon, canvas;
    
    //create and assign variables to objects...

    PhiloGL.Events.create(canvas, {
      onDragStart: function(e) {
        pos = {
          x: e.x,
          y: e.y
        };
      },
      onDragMove: function(e) {
        var z = camera.position.z,
            sign = Math.abs(z) / z;

        moon.rotation.y += -(pos.x - e.x) / 100;
        moon.rotation.x += sign * (pos.y - e.y) / 100;
        moon.update();
        pos.x = e.x;
        pos.y = e.y;
      },
      onMouseWheel: function(e) {
        e.stop();
        camera.position.z += e.wheel;
        camera.update();
      }
  });  
{% endhighlight %}