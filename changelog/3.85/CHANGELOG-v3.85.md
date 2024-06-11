# Version 3.85.0 - Itsuki - in development

# New Features

* `BaseSoundManager.isPlaying` is a new method that will return a boolean if the given sound key is playing. If you don't provide a key, it will return a boolean if any sound is playing (thanks @samme)
* `WebGLRenderer.dispatchContextLost` is a new internal method that is called when the WebGL context is lost. By default this is bound to the property `WebGLRenderer.contextLostHandler`. If you override the context loss handler, be sure to invoke this method in due course.
* `WebGLRenderer.dispatchContextRestore` is a new internal method that is called when the WebGL context is restored. By default this is bound to the property `WebGLRenderer.contextRestoreHandler`. If you override the context restore handler, be sure to invoke this method in due course.
* `WebGLRenderer.setContextHandlers` is a new internal method with 2 optional parameters: `contextLost` and `contextRestored`. These allow you to overwrite the default `contextLostHandler` and `contextRestoreHandler` handlers.

# WebGL Rendering Updates

* `WebGLTextureWrapper.update` expanded:
  * `source` parameter is now type `?object`, so it can be used for anything that is valid in the constructor.
  * New `format` parameter can update the texture format.

# Updates

* Calling `Timeline.pause` will now pause any currently active Tweens that the Timeline had started (thanks @monteiz)
* Calling `Timeline.resume` will now resume any currently paused Tweens that the Timeline had started (thanks @monteiz)
* Calling `Timeline.clear` and `Timeline.destroy` will now destroy any currently active Tweens that the Timeline had created. Previously, active tweens would continue to play to completion (thanks @monteiz)
* `TimelineEvent` has a new property called `tweenInstance`. If the Timeline event has a tween that has been activated, this will hold a reference to it.
* If you create a BitmapText with an invalid key it will now throw a runtime error. Previously it just issued a console warning and then crashed (thanks @samme)
* The console warnings when Audio files are missing/incorrect have been improved (thanks @samme)
* The `requestVideoFrame` polyfill has been updated to the latest release, which should resolve some SSR framework issues. Fix #6776 (thanks @lantictac)

# Bug Fixes

* The `activePointers` game config option is now the correct amount of touch input pointers set. Fix #6783 (thanks @samme)
* The method `TextureManager.checkKey` will now return `false` if the key is not a string, which fixes issues where a texture could be created if a key was given that was already in use (thanks Will Macfarlane).
* Added all of the missing Loader Config values (such as `imageLoadType`) to LoaderConfig, so they now appear in the TypeScript defs.
* The `EXPAND` scale mode had a bug that prevented it from using the world bounds cameras, cutting rendering short. Fix #6767 (thanks @Calcue-dev @rexrainbow)
* Calling `getPipelineName()` on a Game Object would cause a runtime error if running under Canvas. It now simply returns `null`. Fix #6799 (thanks @samme)
* Calling the Arcade Body `setPushable(false)` method for `circle` bodies prevents the bodies from being pushed. Fix #5617 (thanks @kainage)

## Input Bug Fixes

* The method `pointer.leftButtonReleased` will now return `true` when multiple mouse buttons are being pressed.
* The method `pointer.rightButtonReleased` will now return `true` when multiple mouse buttons are being pressed.
* The method `pointer.middleButtonReleased` will now return `true` when multiple mouse buttons are being pressed.
* The method `pointer.backButtonReleased` will now return `true` when multiple mouse buttons are being pressed.
* The method `pointer.forwardButtonReleased` will now return `true` when multiple mouse buttons are being pressed. Fix #6027 (thanks @michalfialadev)

## Examples, Documentation, Beta Testing and TypeScript

Thanks to the following for helping with the Phaser Examples, Beta Testing, Docs, and TypeScript definitions, either by reporting errors, fixing them, or helping author the docs:

@lgtome
@samme
@AlbertMontagutCasero
@rexrainbow

# Deprecation Warning for the next release

The _next release_ of Phaser will make the following API-breaking changes:

* We are removing `Phaser.Struct.Map` and replacing it with a regular JS `Map` instance. This means methods like `contains` and `setAll` will be gone.
* We are removing `Phaser.Struct.Set` and replacing it with a regular JS `Set` instance. This means methods like `iterateLocal` will be gone.
* The `Create.GenerateTexture`, all of the Create Palettes and the `create` folder will be removed.
* The `phaser-ie9.js` entry-point will be removed along with all associated polyfills.