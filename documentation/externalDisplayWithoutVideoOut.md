# Getting an external display to work without an adapter

At the time of this writing, there is no ETA on when the required adapter for driving an external display will be ready. This document is for alternative ways to get an external display running without this adapter.

## scrcpy

[scrcpy](https://github.com/Genymobile/scrcpy) is a tool for displaying, and interacting with, your android phone via your computer via a USB cable.

I've made a more detailed, and chatty [article about it](https://www.randomksandom.com/withoutHDMI/). But here's what you need to know:

### Normal usage

Try this first:

```
scrcpy
```

However on the Gemini, and maybe the Astro, this rotates the display in broken ways. So that leads us onto a number of case-specific work-arounds:

### Default, horizontal orientation

```
scrcpy --lock-video-orientation=0 --crop=2060:1080:0:0
```

### vertical orientation

```
scrcpy --lock-video-orientation=3 --crop=2060:1080:0:0
```

### Apps that mess with the rotation (eg youtube full screen, bVNC)

#### Horizontal

```
scrcpy --lock-video-orientation=1 --crop=540:1080:0:0
```

This has reduced quality, but at least works.

#### Vertical

```
scrcpy --lock-video-orientation=0 --crop=540:1080:0:0
```

This has reduced quality, but at least works.

## Wrapper script

Here is a [wrapper script](https://github.com/ksandom/astroTipsAndTricks/blob/main/documentation/scripts/scrcpyWrapper) to help you:

```
$ ./scripts/scrcpyWrapper --help
Parameter: --help
(No parameters.)  Default. Run scrcpy without options.
gemini            Gemini, horizontally oriented.
gemini-v          Gemini, vertically oriented.
gemini-fh         Gemini, fix horizontal when an app is doing something stupid.
gemini-fv         Gemini, fix vertical when an app is doing something stupid.
```

So to get the normal gemini output, you can do:

```
./scripts/scrcpyWrapper gemini
```
