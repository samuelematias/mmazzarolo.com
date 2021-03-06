---
date: "2018-09-13"
title: "Which One: a React, TypeScript and Mobx game"
tags: [javascript, react, typescript, mobx]
redirect_from:
  - /2018/09/13/which-one-a-react-typescript-and-mobx-game/
---

Today I published yet another small React game, which has been my testing playground for the TypeScript & Mobx combo: [Which One?](https://github.com/mmazzarolo/which-one).

<div align="center">
  <div style="width:420px">
    <img src="/images/logo.png" width="420">
  </div>
</div>

<br />
 
<div class="float-images">
  <div style="width:220px">
    <img src="/images/screenshot-1.png" />
  </div>
  <div style="width:220px">
    <img src="/images/screenshot-2.png" />
  </div>
  <div style="width:220px">
    <img src="/images/screenshot-3.png" />
  </div>
</div>

## Features overview

- Built using [create-react-app-typescript](https://github.com/wmonk/create-react-app-typescript) and [MobX](https://github.com/mobxjs/mobx)
- Can be used as a boilerplate for small React games
- Fully responsive
- PWA-like, works offline
- Card sets can be easily customized and extended

## Known issues

The current version of the project has a few known issues that I haven't had a chance to fix yet:

- On Safari desktop/mobile the audio is not working (see below)
- On Safari mobile there's a touch delay. It goes away if you save the app to the home screen and start it from there (see below)
- On the latest version of Chrome for iOS, for some reasons, the CSS animations are not working smoothly (they were working fine before the Chrome MD redesign)

### Things I learned while building it

#### TypeScript and MobX work really well together

I already had a chance to try the TypeScript & MobX combo in the past but I wasn't able to type the `inject` as I wished.  
In fact, instead of injecting the entire stores, I prefer passing to the `inject` a function (`mapStoresToProps`) that allows me to decouple the component/container from the stores, just like with the Redux `mapStateToProps`.  
This time though I was able to fix it using [this nice little trick](https://github.com/mmazzarolo/which-one/blob/master/src/%40types/mobx-react.d.ts), suggested [here](https://github.com/mobxjs/mobx-react/issues/256), that makes the `inject` works nicely 🎉.

#### Create-react-app-typescript TSLint preset is still too strict

I've been following this [issue](https://github.com/wmonk/create-react-app-typescript/issues/333) since its "discovery" and unfortunately it's still here: the `create-react-app-typescript` TSLint default settings are really _hardcore_ and opinionated so you'll probably find yourself disabling a bunch of rules in `tslint.json` (or use other complex workarounds).  
Hopefully it's going to be fixed soon.

#### Mobile Safari touch delay is here to stay

The touch delay on Safari for iOS is still here as well, and is super annoying when building small React/HTML5 games like this one.  
It should be fixable by playing around with CSS and react-pointable.

#### Safari doesn't allow playing audio without user interactions

Yep, since Safari 11 the Web Audio API requires each audio.play() to be triggered manually (otherwise you'll get a `The request is not allowed by the user agent or the platform in the current context, possibly because the user denied permission.` error).  
There are a few workarounds for the issue but I still haven't had a chance to test them so I just disables the sound effects on Safari.  
See [New Video Policies for iOS](https://webkit.org/blog/6784/new-video-policies-for-ios/) and [Overcoming iOS HTML5 audio limitations](https://www.ibm.com/developerworks/library/wa-ioshtml5/index.html#N1025A)

## Acknowledgments & Disclaimers

Like a few other projects I published in the past, Which One is not intended to be a serious "game", it's just the result of playing around with new technologies.  
This also means that, since I didn't test it thoroughly, it might not work on specific browsers or devices.  
That said, if you have any questions/issues feel free to use the GitHub for sending PRs or starting issue discussions!

All the images and icons used in the project are available on [FlatIcon](https://www.flaticon.com/).
