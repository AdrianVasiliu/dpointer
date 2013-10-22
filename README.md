#Pointer/Events [![Build Status](https://travis-ci.org/ibm-dojo/dtreemap.png?branch=master)](https://travis-ci.org/ibm-dojo/pointer)
This [repository][SPE_pointer] proposes a unified and consistent javascript events API which aims to abstract touch/pointer/mouse events across various devices/OS. 

This API is a shim of the [W3C Pointer Events specification][W3C_pointer] and adds features that are out of scope of the current specification.

- Generates **Pointer Events** according to the current specification..
- Use attribute `data-touch-action` to set touch action on HTML elements; generates `touch-action` and `ms-touch-action` CSS properties when supported by the browser.
- Support **Pointer Capture** with mouse and touch events.
- Normalize **click** (Tap) events, **double click** (double Tap) events, and event **button/buttons/which** values.

##Supported environements
The API has been successfully tested on the following environments.
###Mobile

- Android 4.1.1+ (Stock browser and Chrome)
- BlackBerry 10+
- iOS 6.1.3+
- WindowsPhone 8

###Desktop
- **Pointer Events are always generated when using a mouse on a supported desktop browser**. 
- Multi touch (the ability to get multiple pointers) depends on how the browser handles "finger/pen" user actions. The general rule is:
	- **If your browser supports only mouse events, you will get Pointer Events mapped on mouse events.** For instance, IE9 may be used with a touch screen but you would get only one pointer at a time because pointer events are mapped on mouse events. 
	- **If your browser supports native touch events, you will get Pointer Events mapped on native touch events.** For instance, on Chrome which handles native touch events you will get multiple pointers because pointer events are mapped on touch events.

####Multi touch support
- Chrome
- IE10+

####Mouse support (and single touch when possible)
- IE9
- FireFox 24 (multi touch expected starting release 26)

## Dependencies
This project can be integrated into any AMD capable javascript application. 

##Usage
1. Require the module `pointer/events`
2. Set the attribute `data-touch-action` as appropriate
2. Start listening to Pointer Events: 
`pointerdown, pointerup, pointercancel, pointermove,`
`pointerover, pointerout, pointerenter, pointerleave, gotpointercapture and lostpointercapture`.

###Samples/tests
To run the tests/samples you need to set [requirejs] and [domReady] as a sibbling of the pointer events module like this:

	<root>/pointer/events/events.js
	<root>/requirejs/require.js
	<root>/domReady/domReady.js

##Limitations
- Touch action values `pan-x` and `pan-y` have the same effect as `none`.
- `event.button` returns `0` instead of `-1` on mouse move when no buttons are pressed.
	- Pointer Events specification defines a new set of values for `event.button` and `event.buttons`: Mouse move with no buttons pressed should generate `event.button=-1`. It is not possible to force `-1` on `event.button` on browsers because they use unsigned int as internal representation of `event.button`. Setting -1 gives inconsistent results (some browsers return 0, other 65535...).
- Pen properties (pressure/tiltx,y/height/width...) are not implemented. Properties are defined with default values. The API has not been tested with pens.

## Status
- No official release, **work in progress**.

## Contributing
- Use, tests and contributions are welcome: see [contributing]
- This API was developped with **Dojo 2.0** in mind, as a possible replacement of the current Dojo touch API. For more details see [ticket #17192][T_17192]

## Licensing
This project is distributed by the Dojo Foundation and licensed under the "New" [BSD License]. All contributions require a [Dojo Foundation CLA].

## Credits
* Sebastien Pereira (IBM CCLA)

[SPE_pointer]: https://github.com/seb-pereira/pointer
[W3C_pointer]: http://www.w3.org/TR/pointerevents
[T_17192]: https://bugs.dojotoolkit.org/ticket/17192
[contributing]: CONTRIBUTING.md
[BSD License]: https://github.com/dojo/dojo/blob/master/LICENSE#L13-L41
[Dojo Foundation CLA]: http://dojofoundation.org/about/claForm
[requirejs]: https://github.com/jrburke/requirejs
[domReady]: https://github.com/requirejs/domReady
