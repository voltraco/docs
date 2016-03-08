
# Developers

Plugins can be developed using [`nodejs`](https://nodejs.org).

We kept things pretty simple and unrestricted. Here's an example:

## Example

Here we can listen for stuff that gets dropped onto the player.
The programming interface is exposed though a series of events.

```javascript
module.exports = function(events) {
  events.on('drop', event => {
    console.log(event)
  })
}
```

# Events

## Controls

### controls:load
Load a song into the player. For example, 
`events.emit('controls:load', '/path/to/file.mp3')`.

### controls:pause
Pause the loaded media.

### controls:play
Play the loaded media.

### controls:visualizer:enable
Enable the visualizer (also shows the screen).

### controls:visualizer:disable
Disable the visualizer (also hides the screen).

### controls:visualizer:enable
Enable the visualizer (also shows the screen).

### controls:visualizer:disable
Disable the visualizer (also hides the screen).

## Screens

### queue:show
Show the queue.

### queue:hide
Hide the queue.

### :hide
Hide all closable screens.

## Data

### controls:visualizer:data
When the vizualizer is enabled, there will be a
stream of data that can be listened for. The stream
contains both `time domain data` and `frequency data`
on each emit. For example, an object will look like
this...

```js
{
  byteFrequencyData: [...], // Uint8Array
  byteTimeDomainData: [...] // Uint8Array
}
```

