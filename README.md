# angular-scroll-magic

An angular directive for ScrollMagic, define pins and tweens in markup

## Demo

http://homerjam.github.io/angular-scroll-magic/


## Changelog

* `0.1.0`: __BREAKING__ Directives now using `bindToController` and isolated scope this provides better support for defining params in controllers. You may need to put quotes around strings in your templates.


## Installation

1. Install via npm `npm i -S angular-scroll-magic`

2. Include the necessary files and dependencies (`ScrollMagic`, `GSAP`) on your page or in your build process

2. Add `hj.scrollMagic` to app's module dependencies


## Usage

Turn on indicators to help during development
```js
// In your app config
scrollMagicProvider.addIndicators = true;
```

### smScene
Create a scene, by applying the `sm-scene` directive this determines the timing for the desired behaviour
```html
<div sm-scene="sceneId" duration="500" offset="100" trigger-hook="0.75"></div>
```
* `sm-scene` (string) : scene identifier
* `trigger-element` [(element|selector)] : defaults to the directive element
* `duration` [(integer|string)] : if using a string with a `%` symbol this will be calculated against viewport height
* `offset` [(integer|string)] : if using a string with a `%` symbol this will be calculated against the height of the trigger element (if specified) or document
* `trigger-hook` [(float)] : this determines the position of the trigger point relative to the viewport

### smTween
```html
<div sm-tween="sceneId" duration="1" from-vars="{left: '100%'}" to-vars="{left: '0%'}"></div>
```
* `sm-tween` (string) : the identifier of the scene (trigger) to use
* `duration` (number) : duration of tween relative to length of scene
* `from-vars` [(object)]
* `to-vars|vars` (object) : options used by GSAP such as CSS properties

### smClassToggle
```html
<div sm-class-toggle="sceneId" classes=""></div>
```
* `sm-class-toggle` (string) : the identifier of the scene (trigger) to use
* `classes` (string) : the classes to add/remove

### smPin
```html
<div sm-pin="sceneId"></div>
```
* `sm-pin` (string) : the identifier of the scene (trigger) to use

### ScrollMagicService
Allows access to scenes from your controllers.
```html
<!-- Define scene in your template -->
<div sm-scene="'myScene'"></div>
```
```js
// Add an observer which will trigger on initialisation of the scene
ScrollMagicService.onSceneAdded('myScene', function(scene) {
    // do stuff with `scene`
});

// Or after initialisation
var scene = ScrollMagicService.getScene('myScene');
```

## Gotchas

ScrollMagic doesn't work as expected with Webpack, try using the `script-loader` like so:

```
    import 'script-loader!scrollmagic';
    import 'script-loader!scrollmagic/scrollmagic/uncompressed/plugins/animation.gsap';
    import 'script-loader!scrollmagic/scrollmagic/uncompressed/plugins/debug.addIndicators';

    import angularScrollMagic from 'angular-scroll-magic';
```

Or manually declare dependencies for scrollmagic in your bower.json file:

```
"overrides": {
  "scrollmagic": {
    "main": [
      "scrollmagic/uncompressed/ScrollMagic.js",
      "scrollmagic/uncompressed/plugins/animation.gsap.js",
      "scrollmagic/uncompressed/plugins/animation.velocity.js",
      "scrollmagic/uncompressed/plugins/debug.addIndicators.js",
      "scrollmagic/uncompressed/plugins/jquery.ScrollMagic.js"
    ]
  }
}
```
