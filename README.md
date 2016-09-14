StartAudioContext starts the Web Audio API's AudioContext on an explicit user action. 

According to the [Apple's documentation](https://developer.apple.com/library/safari/documentation/AudioVideo/Conceptual/Using_HTML5_Audio_Video/PlayingandSynthesizingSounds/PlayingandSynthesizingSounds.html): 
> On iOS, the Web Audio API requires sounds to be triggered from an explicit user action, such as a tap. Calling noteOn() from an onload event will not play sound.

StartAudioContext listens for the first non-dragged `touchend` or `mouseup` event on any of the given elements, then triggers a silent AudioBuffer which will start the AudioContext if it isn't already started.

## Installation

Choose one:

* [download the js](https://raw.githubusercontent.com/tambien/StartAudioContext/master/StartAudioContext.js)
* `npm install startaudiocontext`
* `bower install startaudiocontext`

## Basic

```javascript
//pass in the audio context
var context = new AudioContext();

//on iOS, the context will be started on the first valid user action on the #playButton element
StartAudioContext(context, "#playButton")
```

## API

`StartAudioContext(AudioContext, (Elements), (Callback)) => Promise`

#### AudioContext

StartAudioContext will monitor the passed in AudioContext and resolve the promise and/or invoke the passed in callback when the `AudioContext.state === 'running'`. 

#### Elements

The second argument can be an Element, Selector String, NodeList, jQuery Element or an Array of any of those. An event listener is bound to any of the passed in elements which will listen for a valid touch events to trigger a silent AudioBuffer which will start the AudioContext.

```javascript
StartAudioContext(audioContext, '#button', function(){
	//audio context is started
})
```

#### Callback

The third argument is the callback to invoke when the AudioContext has started.

#### => Promise

StartAudioContext returns a promise which is resolved when the AudioContext state is 'running'. 

```javascript
StartAudioContext(audioContext).then(function(){
	//context is started	
})
```

## MIT License

Copyright 2016 Yotam Mann