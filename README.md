BackgroundFetch
==============================

Cross-platform background-fetch for Cordova / PhoneGap ([Tutorial](http://www.doubleencore.com/2013/09/ios-7-background-fetch/)


Follows the [Cordova Plugin spec](https://github.com/apache/cordova-plugman/blob/master/plugin_spec.md), so that it works with [Plugman](https://github.com/apache/cordova-plugman).

This plugin leverages Cordova/PhoneGap's [require/define functionality used for plugins](http://simonmacdonald.blogspot.ca/2012/08/so-you-wanna-write-phonegap-200-android.html). 

## Using the plugin ##
The plugin creates the object `window.plugins.backgroundFetch` with the methods `configure(success, fail, option)`, `start(success, fail)` and `stop(success, fail). 

## Installing the plugin ##

1.Download the repo using GIT or just a ZIP from Github.

2.Add the plugin to your project (from the root of your project):

```
   phonegap plugin add https://github.com/christocracy/cordova-plugin-background-fetch.git
```

3.**Black-magic**:  since PhoneGap has no power to modify AppDelegate.m, we have to patch it with a hook-script.  Copy the following script into your project's `./cordova/hooks` folder:

```
    $ cp plugins/org.transistorsoft.cordova.background-fetch/hooks/after_platform_add/background_fetch.sh .cordova/hooks/after_platform_add/
    $ chmod +x .cordova/hooks/after_platform_add/background_fetch.sh
```

## Example ##

A full example could be:
```
   onDeviceReady: function() {
        var Fetcher = window.plugins.backgroundFetch;
        
        // Your background-fetch handler.
        var fetchCallback = function() {
            console.log('BackgroundFetch initiated');

            // perform your ajax request to server here
            setTimeout(function() {
                Fetcher.finish();   // <-- N.B. You MUST called #finish so that native-side can invoke the required completion-handler
            }, 1000);
        }
        Fetcher.configure(fetchCallback);
    }


```

## iOS

** TODO chris ##

## Android

** TODO Brian ##

## Licence ##

The MIT License

Copyright (c) 2013 Chris Scott and Brian Samson

Permission is hereby granted, free of charge, to any person obtaining a copy
of this software and associated documentation files (the "Software"), to deal
in the Software without restriction, including without limitation the rights
to use, copy, modify, merge, publish, distribute, sublicense, and/or sell
copies of the Software, and to permit persons to whom the Software is
furnished to do so, subject to the following conditions:

The above copyright notice and this permission notice shall be included in
all copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR
IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY,
FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE
AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER
LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM,
OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN
THE SOFTWARE.
