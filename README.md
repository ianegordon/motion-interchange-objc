# Motion Interchange

[![Build Status](https://travis-ci.org/material-motion/motion-timing-objc.svg?branch=develop)](https://travis-ci.org/material-motion/motion-timing-objc)
[![codecov](https://codecov.io/gh/material-motion/motion-timing-objc/branch/develop/graph/badge.svg)](https://codecov.io/gh/material-motion/motion-timing-objc)
[![CocoaPods Compatible](https://img.shields.io/cocoapods/v/MotionInterchange.svg)](https://cocoapods.org/pods/MotionInterchange)
[![Platform](https://img.shields.io/cocoapods/p/MotionInterchange.svg)](http://cocoadocs.org/docsets/MotionInterchange)
[![Docs](https://img.shields.io/cocoapods/metrics/doc-percent/MotionInterchange.svg)](http://cocoadocs.org/docsets/MotionInterchange)

## Installation

### Installation with CocoaPods

> CocoaPods is a dependency manager for Objective-C and Swift libraries. CocoaPods automates the
> process of using third-party libraries in your projects. See
> [the Getting Started guide](https://guides.cocoapods.org/using/getting-started.html) for more
> information. You can install it with the following command:
>
>     gem install cocoapods

Add `MotionInterchange` to your `Podfile`:

    pod 'MotionInterchange'

Then run the following command:

    pod install

### Usage

Import the framework:

    @import MotionInterchange;

You will now have access to all of the APIs.

## Example apps/unit tests

Check out a local copy of the repo to access the Catalog application by running the following
commands:

    git clone https://github.com/material-motion/motion-timing-objc.git
    cd motion-timing-objc
    pod install
    open MotionInterchange.xcworkspace

## Guides

1. [Architecture](#architecture)
2. [How to create a cubic bezier animation](#how-to-create-a-cubic-bezier-animation)
3. [How to create a spring animation](#how-to-create-a-spring-animation)
4. [How to define a motion spec](#how-to-define-a-motion-spec)

### Architecture

This library defines a format for representing motion in Objective-C and Swift applications. The
primary data type, `MotionTiming`, allows you to describe the duration, delay, timing curve, and
repetition for an animation.

### How to define a cubic bezier animation

In Objective-C:

```objc
MDMMotionTiming timing = (MDMMotionTiming){
  .delay = 0.150,
  .duration = 0.225,
  .curve = _MDMBezier(0.4f, 0.0f, 0.2f, 1.0f)
}
```

### How to define a spring animation

In Objective-C:

```objc
MDMMotionTiming timing = (MDMMotionTiming){
  .curve = _MDMSpring(1, 100, 10)
}
```

### How to define a motion spec

Motion timing structs can be used to represent complex multi-element and multi-property motion
specifications. An example of a common complex motion spec is a transition which has both an
expansion and a collapse variant:

```objc
struct MDCMaskedTransitionMotionTiming {
  MDMMotionTiming contentFade;
  MDMMotionTiming floodBackgroundColor;
  MDMMotionTiming maskTransformation;
  MDMMotionTiming horizontalMovement;
  MDMMotionTiming verticalMovement;
  MDMMotionTiming scrimFade;
};
typedef struct MDCMaskedTransitionMotionTiming MDCMaskedTransitionMotionTiming;

struct MDCMaskedTransitionMotionSpec {
  MDCMaskedTransitionMotionTiming expansion;
  MDCMaskedTransitionMotionTiming collapse;
  BOOL shouldSlideWhenCollapsed;
  BOOL isCentered;
};
typedef struct MDCMaskedTransitionMotionSpec MDCMaskedTransitionMotionSpec;
```

We can then use this motion spec to implement our animations in a transition like so:

```objc
MDCMaskedTransitionMotionTiming timing = isExpanding ? spec.expansion : spec.collapse;

// Can now use timing's properties to associate animations with views.
```

## Contributing

We welcome contributions!

Check out our [upcoming milestones](https://github.com/material-motion/motion-timing-objc/milestones).

Learn more about [our team](https://material-motion.github.io/material-motion/team/),
[our community](https://material-motion.github.io/material-motion/team/community/), and
our [contributor essentials](https://material-motion.github.io/material-motion/team/essentials/).

## License

Licensed under the Apache 2.0 license. See LICENSE for details.
