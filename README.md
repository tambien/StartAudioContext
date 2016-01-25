StartAudioContext starts the Web Audio API AudioContext on an explicit user action. 

According to the [Apple's documentation](https://developer.apple.com/library/safari/documentation/AudioVideo/Conceptual/Using_HTML5_Audio_Video/PlayingandSynthesizingSounds/PlayingandSynthesizingSounds.html): 
> On iOS, the Web Audio API requires sounds to be triggered from an explicit user action, such as a tap. Calling noteOn() from an onload event will not play sound.

To get around this StartAudioContext triggers a silent Oscillator when a non-dragged `touchend` or `mouseup` event occurs on the given elements. After one of these explicit user actions, the AudioContext is started and ready to make some noise. 

## Installation

Install in any of these ways:

* download the [min]() or [full]() JS file. 
* `npm install startaudiocontext`
* `bower install startaudiocontext`

## API

The `on` method can accept an Element, String, NodeList, jQuery element or an Array of any of those.

### `.on({Element})`

Bind the tap listener to the given HTML Element. 

```javascript
var el = document.createElement("div");
StartAudioContext.on(el);
```
### `.on({String})`

Pass in a query selector to bind to all of the matching HTML Elements

```javascript
StartAudioContext.on("button");
```

### `.on({NodeList})`

Pass in the NodeList returned by `querySelectorAll`. 

```javascript
var allButtons = document.querySelectorAll("button");
StartAudioContext.on(allButtons);
```

### `.on({jQuery})`

You can pass in a jQuery element. 

```javascript
StartAudioContext.on($("button"));
```

### `.on({Array})`

You can pass in an Array combining any of the above. Make sure you're array is not self-referential, or it'll go into an infinite, recursive loop. 

```javascript
StartAudioContext.on([el, $("button"), ".className");
```

### `setContext({AudioContext})`

Set the AudioContext. If the context is set, a valid `touchend` event will trigger a silent Oscillator node and start the AudioContext. 

```javascript
var audioContext = new AudioContext();
StartAudioContext.setContext(audioContext);
```

### `isStarted()`

Returns `true` if the given AudioContext is running. See [`AudioContext.state`](https://developer.mozilla.org/en-US/docs/Web/API/AudioContext/state).

```javascript
StartAudioContext.isStarted();
```

### `onTap({Function})`

Set your own callback when a non-dragging tap has occurred on any of the element. This method is only invoked on the **first** tap; subsequent taps will not invoke this callback. 


```javascript
StartAudioContext.onTap(function(){
	//tapped for the very first time
});
```

### Chaining

All of the methods (except `isStarted`) are chainable. 

```javascript
StartAudioContext
	.setContext(ctx)
	.on("button")
	.on(element)
	.onTap(function(){
		//tap
	});
```

## MIT License

Copyright 2016 Yotam Mann