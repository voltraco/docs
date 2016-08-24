# Developers

Plugins can be developed using [`nodejs`](https://nodejs.org).

We kept things pretty simple and unrestricted. Here's an example:

## Example

The programming interface is exposed though a series of events. Both the
`DOM` and `Node.js` APIs are available from within the plugin. For a more
complete example see [`this`](https://github.com/voltraco/voltra-plugin-example).

```javascript
module.exports = function(events) {
  events.on('drop', event => {
    console.log(event)
  })
}
```

# Events

## Add music events
### add:show
If emitted, shows the add music screen.

### add:hide
If emitted, hides the add music screen.

### add:update
Emitted when the add music screen is updated.

## Tracks and Albums
### track:delete
Emitted when a track is to be deleted. Expects a track object.

### album:delete
Emitted when an album is to be deleted. Expects a track object.

### album:show
If emitted, shows the album screen.

### album:hide
If emitted, hides the album screen.

### albums:sort
If emitted, sets the sort criteria for the albums view.

### albums:update
If emitted, invalidates the albums cache, fetches all albums and displays them.

## Artists

### artists:show
If emitted, displays the artists screen.

### artists:update
If emitted, invalidates the artists cache, fetches all artists and displays
them.

## Player controls

### controls:play
If emitted, will toggle the playing state.

### controls:stop
If emitted, the player will immediately stop playing.

### controls:paused
Emitted when the player is paused.

### controls:playing
Emitted when the player has started playing.

### controls:back
If emitted, causes the previous item in the queue history to play.

### controls:next
If emitted, causes the next item in the queue to play.

### controls:show
Shows the player controls at the bottom of the window.

### controls:visualizer:data
When the vizualizer is enabled, there will be a stream of data that can be
listened for. The stream contains both `time domain data` and `frequency data`
on each emit. For example, an object will look like this...

```js
{
  byteFrequencyData: [...], // Uint8Array
  byteTimeDomainData: [...] // Uint8Array
}
```

### controls:visualizer:disable
Stop data from being emitted.

### controls:visualizer:enable
Start emitting data if there is media playing.

## Playlist

### playlist:add
When emitted, adds a track to a playlist. Expects a `track object`.

### playlist:hide
Hide the currently displayed playlist.

### playlist:show
Show a playlist. Expects an options object that contains `options.id`, the id
of the playlist.

### playlist:play
Play a playlist. Expects an options object that contains `options.id`, the id
of the playlist.

### playlist:refresh
Emitted when there are changes to a playlist.

### playlist:remove
If emitted, removes a playlist. The first argument should be an options
object that contains `options.id`, the id of the playlist.

## Playlists
### playlists:create
If emitted, creates a new playlist. Accepts an options object containing a
`track object`.

### playlists:remove
If emitted, removes a playlist. Expects an options object containing
`options.id` where the id of the playlist is specified.

### playlists:show
If emitted, shows all of the playlists.

### playlists:sort
If emitted, invokes sort on the playlist view. Expects an options object
where the boolean values `options.date` and `options.reverse` determine the
order.

### playlists:update
Should be emitted when there are changes to a playlist.

## Profile

### profile:show
If emitted, will show the user profile.

### profile:update
Should be emitted when there are changes to the user's profile data. For
instance, track count, playlist count, etc.

### profile:sync:update
Emitted when there is cloud sync progress.

## Queue

### queue:show
If emitted, the queue will be displayed.

### queue:hide
If emitted, the queue will be hidden.

### queue:remove
If emitted, an item will be removed from the queue. Expects a `track object`.

## Search

### search:show
If emitted, shows the search input.

### search:focus
If emitted, displays the search input and focuses on the input.

### search:hide
If emitted, the search input and results will be hidden.

### search:input
Emitted when there is a keypress on the search input.

### search:toggle
Toggles the display of the search input and results.

## Tag Editor

### tageditor:show
If emitted, displays the tag editor. Expects either a `track` or `album object`.

### tageditor:hide
If emitted, hides the tag editor, changes made by the user will not be saved.

## File Watcher

### watch:start
If emitted, starts an instance of the file watcher. Expects an options object
with `options.dir` pointing to the directory to be watched.

### watch:quit
If emitted, quits the current instance of the file watcher. Only one instance
of the file watcher will run at once.

### watch:restart
Restarts the file watcher.

### check-for-updates
If emitted, checks for updates. Expects an options object.
If `options.prompted` is true, it will prompt the user through the process
with a set of dialogs.

## General application events

### auth
Emmitted when the user authenticates. The first parameter will be an object
containing the user profile.

### auth:show
If emitted, prompts the user to authenticate.

### drop
Emitted when something is dropped onto the player. If parsable, a url or file
path will be provided as the first parameter.

### quit
Exists, saves state of application and backs up user data.

### exit
Immediately exit the application.

### error
Emitted when there is an error. The first parameter will be an object
with `params.title` and `options.message` and the usual error objet properties.

### section:show
Emitted when any section is displayed. The first parameter is an object
with `params.name` being the section that has been displayed.

### feedback:show
If emitted, the feedback dialog will be displayed.

### maximize
If emitted, the window will be maximized.

### minimize
If emitted the window will be minimized.

### restore
If emitted the window will be restored to the last position and size that the
user set.

