
# SlimerJS

SlimerJS is a XulRunner application that can be launched with Firefox, allowing
to execute an external javascript script which can manipulate web content.

Its goal is to provide a tool like [PhantomJs](http://phantomjs.org/), with the
same API, except that it runs Gecko instead of Webkit, and it is not headless
(but you can still use xvfb to have a headless SlimerJS).

You could then use other tools like [CasperJS](http://casperjs.org)...

For the moment, you can only run simple scripts that can use few functions from the **system** module, the **fs** module and the **webpage** module.

Follow us on twitter: [@slimerjs](https://twitter.com/slimerjs)

# Install

- Install Firefox 17 or higher
- For Windows users: install [Cygwin](http://www.cygwin.com/) or any other unix
  environment with a true console ;-). A .bat is not povided yet.
- [download the source code of SlimerJS](https://github.com/laurentj/slimerjs/archive/master.zip) if you didn't it yet
- Open a terminal
- Set the environment variable SLIMERJSLAUNCHER, which should contain the full
  path to the firefox binary :
   - On linux: ```export SLIMERJSLAUNCHER=/usr/bin/firefox```
   - On windows, with cygwin, something like that: ```export SLIMERJSLAUNCHER="/cygdrive/c/program files/mozilla firefox/firefox.exe"```
   - On MacOS: ```export SLIMERJSLAUNCHER=/Applications/Firefox.app/Contents/MacOS/firefox```
- You can set this variable in your .bashrc or .profile of course.


# Launching SlimerJS

Open a terminal and go to the bin directory of SlimerJS. Then launch:

```
    slimerjs myscript.js
```

The given script myscripts.js is then executed in a window. If your script is
short, you probably won't see this window.

You can for example launch some tests:

```
    slimerjs ../test/initial-tests.js
```

# Content of a script

It should contain javascript instructions. The script is executed in the context of a
blank page. Here are objects you can play with:

- the [window object](https://developer.mozilla.org/en-US/docs/DOM/window) of the blank page and all of its functions
- the [document object](https://developer.mozilla.org/en-US/docs/DOM/document) of the blank page
- a console object, similar with the [DOM Console object](https://developer.mozilla.org/en-US/docs/DOM/console),
  providing these methods: debug, log, info, warn, error, trace, clear, dir, dirxml, group, groupEnd
- a slimer object (and a phantom object that is a reference to slimer for compatibility): it
  will provide the [API of PhantomJS 1.7](https://github.com/ariya/phantomjs/wiki/API-Reference),
  but all of its properties and methods are not implemented
- a require function to load CommonJS modules
- You can load and use the **system** module
- You can load and use the **fs** module although its implementation is not finished
- You can load and use the **webpage** module although its implementation is not finished

You can read the [compatibility table](API.md) to know the implementation progress.

In the future, there will be all features of [PhantomJS](https://github.com/ariya/phantomjs/wiki/Quick-Start).

Note that you must execute ```slimer.exit()``` or ```phantom.exit()``` to terminate the application, else
the window of SlimerJS won't be closed.

# Roadmap

For a first stable release:
- implementation of the API of PhantomJS

After this release, I'll try to hack XulRunner to run headless windows (very difficult I guess :-) )

# FAQ

- Why is it not Headless?
  - Gecko, the rendering engine of Firefox, cannot render web content without a window.
    See [Mozilla bug 446591](https://bugzilla.mozilla.org/show_bug.cgi?id=446591). however you could
    launch SlimerJS with xvfb.
- Why is it called "SlimerJs"?
   - Slimer is the name of a ghost in the movie "GhostBusters". As you may now, the Firefox source code uses
    many references from this movie, and since PhantomJS, CasperJs and other related tools, is a matter of ghost...


