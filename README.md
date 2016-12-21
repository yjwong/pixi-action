# pixi-action

> **pixi-action** is a plugin for Pixi.js v3.0.8 or higher to create actions and animations easily. API inspired by cocos2d-x. Online demo [here](http://git.hust.cc/pixi-action/).

[![npm](https://img.shields.io/npm/v/pixi-action.svg?style=flat-square)](https://www.npmjs.com/package/pixi-action) [![npm](https://img.shields.io/npm/dt/pixi-action.svg?style=flat-square)](https://www.npmjs.com/package/pixi-action) [![npm](https://img.shields.io/npm/l/pixi-action.svg?style=flat-square)](https://www.npmjs.com/package/pixi-action)


## 1. Install

> **npm install pixi-action**

`require` it, or import it with `script` tag, all is OK.


## 2. Usage

Code just like below.

```js
var renderer = new PIXI.autoDetectRenderer(800,600);
document.body.appendChild(renderer.view);
var stage = new PIXI.Container();

var sprite1 = new Sprite(resources['res/img/animal.png'].texture);

var action_move = PIXI.action.MoveTo(500, 400, 2);

var animation = PIXI.actionManager.runAction(cat, action_moveto);
animation.on('end', function(elapsed) {
  console.log('action end.');
});

function animate() {
  window.requestAnimationFrame(animate);
  renderer.render(stage);
  PIXI.actionManager.update(); // update actions
}
animate();
```


## 3. How it works

This plugin add a new namespace named **`action`** to the PIXI namespace, and the action namespace has 2 new classes, **ActionManager** and **Action**, and create an instance for ActionManager in PIXI.actionManager, but all you need is add `PIXI.actionManager.update()` in your requestAnimationFrame. You can pass as params for `PIXI.actionManager.update(delta)` your own delta time, if you don't pass anything it will be calculated internally. 

For max accuracy calculating the delta time you can use the [AnimationLoop](https://github.com/Nazariglez/pixi-animationloop/) plugin.

When a action is started, or ended, it will fire events named `start` / `end`.


### 4. Using AnimationLoop

```js
var renderer = new PIXI.autoDetectRenderer(800,600);
document.body.appendChild(renderer.view);

var animationLoop = new PIXI.AnimationLoop(renderer);

//Add a postrender or prerender event to add the timer.update in the raf.
animationLoop.on('postrender', function() {
  PIXI.actionManager.update(this.delta); //Pass as param the delta time to PIXI.timerManager.update
});

animationLoop.start();
```


## 5. Events

TimerManager extends from [PIXI.utils.EventEmitter](https://github.com/primus/eventemitter3), and emit some events: start, end, repeat, update and stop. More info: [Node.js Events](https://nodejs.org/api/events.html#events_emitter_emit_event_arg1_arg2)

- **start - callback(elapsedTime)**: Fired when the action starts.
- **end - callback(elapsedTime)**: Fired when the action is ended.


## 6. Actions & Animations

Now **pixi-action** supported actions / animations below. You can just combine them for complex actions.

 - [x] **ActionMove**

> PIXI.action.MoveTo(x, y, time);
> PIXI.action.MoveBy(x, y, time);

 - [ ] **ActionScale**

> PIXI.action.ScaleTo(scale_x, scale_y, time);
> PIXI.action.ScaleBy(scale_x, scale_y, time);

 - [ ] **ActionRotate**

> PIXI.action.RotateTo(angle, time);
> PIXI.action.RotateBy(angle, time);

 - [ ] **ActionSkew**

> PIXI.action.SkewTo(skew, time);
> PIXI.action.SkewBy(skew, time);

 - [ ] **ActionBlink**

> PIXI.action.Blink(count, time);

 - [ ] **ActionFade**

> PIXI.action.FadeIn(time);
> PIXI.action.FadeOut(time);

 - [ ] **ActionJump**

> PIXI.action.JumpTo(x, y, time);
> PIXI.action.JumpBy(x, y, time);

 - [ ] **ActionTint**

> PIXI.action.TintTo();
> PIXI.action.TintBy();

 - [ ] **ActionSequence**

> PIXI.action.Sequence(action1[, action2[, ...]]);

 - [ ] **ActionRepeat**

> PIXI.action.Repeat(action, count);

 - [ ] **repeatForever**

> PIXI.action.Repeat(action);


## 7. API

 - **PIXI.actionManager.runAction(object, action)**: run action on an object, return an animation, can `on` the events.
 - **new PIXI.action.*(args)**: create an action.
  

## LICENSE

MIT@[hustcc](https://github/com/hustcc). Welcome to **`Submit Pull Request`**.