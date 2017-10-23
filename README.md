# STOMT JavaScript-SDK [![Stomt API](https://img.shields.io/badge/stomt-v2.10.X-brightgreen.svg)](https://rest.stomt.com/)

<a href="http://maxklenk.github.io/angular-sample-app/" title="sample application">
<img alt="Easy Integration" align="right" width="380" src="screenshot-form.png"/>
</a>

* [Demo](#demo)
* [Installation](#installation)
  * [addTab](#documentation---addtab)
  * [addFeed](#documentation---addfeed)
  * [addCreate](#documentation---addcreate)
  * [Events](#documentation---events)
* [Webview / Iframe](#webview--iframe)
* [Contribution](#contribution)

Our SDK allows you to add the feedback solution [www.stomt.com](https://www.stomt.com/) to your websites or any other HTML/JavaScript based applications. The SDK currently allows you to add a button to your website, which when used open a STOMT creation form. In the form customers can choose if they want to speak a wish or praise your site and then enter their thoughts. All submitted ideas can then be manages on the STOMT website, where they can be discussed, voted and finally come true. 

To connect your site to STOMT, [create a project page on stomt](https://www.stomt.com/createTarget) first.

## Demo

View the live demo [here](https://stomt.github.io/stomt-javascript-sdk/). The projects [source](https://github.com/stomt/stomt-javascript-sdk/tree/master/docs) can be found on GitHub, it itegrates the sdk dynamically in the [index.html](https://github.com/stomt/stomt-javascript-sdk/blob/master/docs/index.html#L99) file.


## Installation

To install the STOMT JavaScript-SDK you only have to add the following lines to the bottom of you html file and adjust the "targetId" at the bottom of the script to your business profiles username. 

```html
<div id="stomt_feed"></div> <!-- if you want to include a feed -->
<div id="stomt_create"></div> <!-- if you want to include a feed -->
<script>
  // Include the STOMT JavaScript SDK
  (function(w, d, n, r, t, s){
    w.Stomt = w.Stomt||[];
    t = d.createElement(n);
    s = d.getElementsByTagName(n)[0];
    t.async=1;
    t.src=r;
    s.parentNode.insertBefore(t,s);
  })(window, document, 'script', 'https://www.stomt.com/widget.js');
  
  // ADJUST THE 'PAGENAME' to your businesses username 
  // -> https://www.stomt.com/my-business -> my-business
  Stomt.push(['addTab', {targetId: 'PAGENAME'}]);
  Stomt.push(['addFeed', {targetId: 'PAGENAME'}]);
  Stomt.push(['addCreate', {targetId: 'PAGENAME'}]);
</script>
```
Copy & paste, done! You have further options to customize the widget. See the documentation part below.

## Documentation - addTab

The current version allows you to add a Feedback button to your page:
```JavaScript
Stomt.push(['addTab', options]);
```

### showTab

You can use the `showTab(options)` method to show the widget if it is hidden.
```JavaScript
Stomt.push(['showTab', options]);
// or if you are sure the JS finished loading
Stomt.showTab(options);
```

### hideTab

You can use the `hideTab()` method to hide the widget.
```JavaScript
Stomt.push(['hideTag']);
// or if you are sure the JS finished loading
Stomt.hideTab();
```

### toggleTab

You can use the `toggleTab(options)` method to toggle the widget.
```JavaScript
Stomt.push(['toggleTab']);
// or if you are sure the JS finished loading
Stomt.toggleTab();
```

### updateTabFile

You can use the `updateTabFile()` method to set a new file for the Tab Widget. The next times a STOMT is created this file is attached.
```JavaScript
Stomt.updateTabFile(file);
```

### options.targetId

The `options` object has to contain a `targetId`. The `targetId` is your pages identifier you can copy it from the pages url (https://www.stomt.com/stomt-javascript-sdk -> stomt-javascript-sdk). All stomts created using the JavaScript-SDK will be addressed to this page:
```JavaScript
Stomt.push(['addTab', {targetId: 'stomt-javascript-sdk'}]);
```

### options.position

Optionally you can set the `position` of the button, the default position is `right`. If required you can align the button to the left side by passing `position: 'left'`:
```JavaScript
Stomt.push(['addTab', {targetId: 'stomt-javascript-sdk', position: 'left'}]);
```


<a href="http://maxklenk.github.io/angular-sample-app/" title="sample application">
<img alt="Easy Integration" align="right" width="380" src="screenshot-success.png"/>
</a>


### options.label

The default label of the button is `Feedback`, you can change that by passing another `label`:
```JavaScript
Stomt.push(['addTab', {targetId: 'stomt-javascript-sdk', label: 'Speak your wish!'}]);
```

### options.colorText

To change the colors used for the widget button you have three options to configure.
The first one is `colorText`, it allows you to change the text color (default: `#FFFFFF`):
```JavaScript
Stomt.push(['addTab', {targetId: 'stomt-javascript-sdk', colorText: '#FFFFFF'}]);
```

### options.colorBackground

The `colorBackground` option allows you to change the background color of the button (default: `#0091C9`):
```JavaScript
Stomt.push(['addTab', {targetId: 'stomt-javascript-sdk', colorBackground: '#0091C9'}]);
```


### options.colorHover

The `colorHover` option allows you to change the background color of the button when the user hovers it (default: `#04729E`):
```JavaScript
Stomt.push(['addTab', {targetId: 'stomt-javascript-sdk', colorHover: '#04729E'}]);
```

### options.file

By attaching a JSON object with the properties `name` (String) and `data` (Object) to the property `file`, data can be attached to STOMTs that are submitted from the Tab Widget:
```JavaScript
Stomt.push(['addTab', {targetId: 'stomt-javascript-sdk', file: {name: 'fileName.file', data: Object}}]);
```
Include the file extension in the file name to ensure that it is treated correctly after download.

### options.showClose

Via the `showClose` property, you can specify whether the Close Icon in the Tab Widget should be shown or not (default: `true`):
```JavaScript
Stomt.push(['addTab', {targetId: 'stomt-javascript-sdk', showClose: false}]);
```

### options.preload

By setting the property `preload` to `true`, you can tell the Widget to preload the Tab iframe in the background (default: `false`). This reduces the loading delay when showing the Tab for the first time.
```JavaScript
Stomt.push(['addTab', {targetId: 'stomt-javascript-sdk', preload: true}]);
```
  

### Custom CSS

The feedback button can be styled and positioned using the css class `.stomt-button`.

For example: 

```css
/* round button in the bottom right corner */
.stomt-button {
  height: auto;
  border-radius: 50%;
  right: 50px;
  bottom: 50px;
  color: transparent;

  transform: none;
  float: none;
  padding: 0;
}

/* overwrite the content with a custom icon */
.stomt-button:before {
  font-family: "my-icon-font";
  line-height: 1;
  display: inline-block;
  content: "my-custom-icon";
  color: #ffffff;
  font-size: 40px;
  padding: 5px;
}
```

To add custom styling to the widget itself please add a `<style>` tag to the page containing the STOMT widget. This tag will be put inside the iframe to overwrite the default styling.

To allow us to read the tag please add the attribute `stomt-widget` to the `<style>` tag: `<style stomt-widget>`. To be sure that your styles overwrite the default styling please use `!important`.

An example for custom styles can be found below:

```html
<style stomt-widget>
  /* customize wish/like bubble color */
  /* NOTE: please adjust the font color when changing the background-color */
  .stomt-create-bubble--wish {
    background-color: blue !important;
    border-color: blue !important;
    color: white !important;
  }
  .stomt-create-bubble--like {
    background-color: green !important;
    border-color: green !important;
    color: white !important;
  }

  /* customize target bubble */
  /* NOTE: please adjust the font color when changing the background-color */
  .stomt-create-target-bubble {
    background-color: darkgray !important;
    border-color: darkgray !important;
    color: white !important;
  }

  /* customize widget background color*/
  /* NOTE: when changing the background color you might have to adjust header and footer colors*/
  .stomtApp body {
    background: white !important;
  }

  /* customize header color */
  .feed-headline-small {
    color: black !important;
  }

  .widget-footer {
    background: white !important;
  }

  /* customize footer color */
  .widget-footer a {
    color: black !important;
  }

  /* customize submit button color */
  /* NOTE: please adjust the font color when changing the background-color */
  .stomt-form-submit {
    background-color: green !important;
    color: white !important;
  }
  .stomt-form-submit--disabled {
    background-color: darkgray !important;
  }
</style>
```


## Documentation - addFeed

The current version allows you to add a STOMT feed somewhere on your page:
```JavaScript
Stomt.push(['addFeed', options]);
```

### options.targetId (required)

The `options` object has to contain a `targetId`. The `targetId` is your pages identifier you can copy it from the pages url (https://www.stomt.com/stomt-javascript-sdk -> stomt-javascript-sdk).
The Feed will show stomts addressed to this page:
```JavaScript
Stomt.push(['addFeed', {targetId: 'stomt-javascript-sdk'}]);
```

### options.elementId (default: `stomt_feed`)
You can define where you want to show the feed on your page. Simply add an empty element with an id: `<div id="stomt_feed"></div>`,  `stomt_feed` is the default id, if you want to use another id you can use this option and pass your custom elementId.

```JavaScript
Stomt.push(['addFeed', {targetId: 'stomt-javascript-sdk', elementId: 'custom-element'}]);
```

### options.callDE
The custom german call-to-action that will be displayed at the top of your feed.

```JavaScript
Stomt.push(['addFeed', {targetId: 'stomt-javascript-sdk', callDE: 'Sags mir'}]);
```

### options.callEN
The custom english call-to-action that will be displayed at the top of your feed.

```JavaScript
Stomt.push(['addFeed', {targetId: 'stomt-javascript-sdk', callEN: 'Tell me'}]);
```

### options.lang
Force the default language of the user interface and the stomt creation form.
```JavaScript
Stomt.push(['addFeed', {targetId: 'stomt-javascript-sdk', lang: 'de'}]);
```

### options.creation (default: true)
Hide the creation form by setting `creation` to `false`.

```JavaScript
Stomt.push(['addFeed', {targetId: 'stomt-javascript-sdk', creation: false}]);
```

### options.q
Filter the feed for a specific keyword.

```JavaScript
Stomt.push(['addFeed', {targetId: 'stomt-javascript-sdk', q: 'improve'}]);
```

### options.has
Filter the feed for specific stomts, e.g.
* `reaction` - with a reaction
* `!reaction` - without a reaction

```JavaScript
Stomt.push(['addFeed', {targetId: 'stomt-javascript-sdk', has: 'reaction'}]);
```

### options.label
Only show stomts with a specific label attached.

```JavaScript
Stomt.push(['addFeed', {targetId: 'stomt-javascript-sdk', label: 'discuss'}]);
```

### options.from
Only show stomts created by a specific user.

```JavaScript
Stomt.push(['addFeed', {targetId: 'stomt-javascript-sdk', from: 'userID'}]);
```

### options.is
Filter what kind of stomts you want to show, e.g. `wish`,`like`

```JavaScript
Stomt.push(['addFeed', {targetId: 'stomt-javascript-sdk', is: 'wish'}]);
```

### options.resize
Resize the iframe height automatically when the content changes. Set this option to `false` to disable resizing.

```JavaScript
Stomt.push(['addFeed', {targetId: 'stomt-javascript-sdk', resize: false}]);
```

### options.limit
Choose how may stomts should be displayed maximal. (default: no limit)

```JavaScript
Stomt.push(['addFeed', {targetId: 'stomt-javascript-sdk', limit: 50}]);
```


### options.initial
Choose how may stomts should be requested. (default: `15`)

```JavaScript
Stomt.push(['addFeed', {targetId: 'stomt-javascript-sdk', initial: 20}]);
```


### Custom CSS

The stomt feed can be styled and positioned using the css class `.stomt-feed-iframe`.

For example: 

```css
.stomt-feed-iframe {
  /* use max-width instead of width to ensure that the feed is visible on mobile devices */
  max-width: 600px;
  /* use min-height to define how many stomts should be visible without scrolling (850px ~ 3 stomts)*/
  min-height: 850px;
}
```

To change the content inside the iframe use the same method as described above in [addTab - Custom CSS](#custom-css).


## Documentation - addCreate

The current version allows you to add a STOMT creation form somewhere on your page, it searched for an element with the id `stomt_create` and adds the creation form in this element:
```JavaScript
Stomt.push(['addCreate', options]);
```

### showCreate

You can use the `showCreate(options)` method to show the widget if it is hidden or if it has been added with the `preload` flag.
```JavaScript
Stomt.push(['showCreate', options]);
// or if you are sure the JS finished loading
Stomt.showCreate(options);
```

### hideCreate

You can use the `hideCreate()` method to hide the widget.
```JavaScript
Stomt.push(['hideCreate', options]);
// or if you are sure the JS finished loading
Stomt.hideCreate(options);
```

### updateCreateFile

You can use the `updateCreateFile()` method to set a new file for the Create Widget. The next times a STOMT is created this file is attached.
```JavaScript
Stomt.updateCreateFile(file);
```

### options.targetId (required)

The `options` object has to contain a `targetId`. The `targetId` is your pages identifier you can copy it from the pages url (https://www.stomt.com/stomt-javascript-sdk -> stomt-javascript-sdk).
The Feed will show stomts addressed to this page:
```JavaScript
Stomt.push(['addCreate', {targetId: 'stomt-javascript-sdk'}]);
```

### options.elementId (default: `stomt_create`)
You can define where you want to show the feed on your page. Simply add an empty element with an id: `<div id="stomt_create"></div>`,  `stomt_create` is the default id, if you want to use another id you can use this option and pass your custom elementId.

```JavaScript
Stomt.push(['addCreate', {targetId: 'stomt-javascript-sdk', elementId: 'custom-element'}]);
```

### options.lang
Force the default language of the user interface and the stomt creation form.
```JavaScript
Stomt.push(['addCreate', {targetId: 'stomt-javascript-sdk', lang: 'de'}]);
```

### options.file

By attaching a JSON object with the properties `name` (String) and `data` (Object) to the property `file`, data can be attached to STOMTs that are submitted from the Create Widget:
```JavaScript
Stomt.push(['addCreate', {targetId: 'stomt-javascript-sdk', file: {name: 'fileName.file', data: Object}}]);
```
Include the file extension in the file name to ensure that it is treated correctly after download.

### options.preload

By setting the property `preload` to `true`, you can tell the Widget to preload the Create iframe in the background (default: `false`). This reduces the loading delay when showing the Widget for the first time. 

Important: When using the `preload` flag, the iframe will not be shown initially. You have to explicitly show it via `Stomt.showCreate`.
```JavaScript
Stomt.push(['addCreate', {targetId: 'stomt-javascript-sdk', preload: true}]);
```
  

### Custom CSS

To change the content inside the iframe use the same method as described above in [addTab - Custom CSS](#custom-css).

## Documentation - events

You can register Event Listeners to react on user interactions with the widget by calling `registerWidgetListener`. Registered Callbacks can be removed via the `removeWidgetListener` method.
```JavaScript
function callback (data) {
  ...
}

Stomt.push(['registerWidgetListener', 'eventType', callback]);
// or if you are sure the JS finished loading
Stomt.registerWidgetListener('eventType', callback);
// to remove the callback
Stomt.removeWidgetListener('eventType', callback)
```

Available events are:
- for the Feed Widget: 
    - `stomtFeed-resize`: listen to resize events of the iframe. Only works when the `resize` flag is set to true.
- for the Tab Widget:
    - `stomtTab-hide`/`stomtTab-show`: is fired when the visibility of the Tab Widget changes.
- for the Create Widget:
    - `stomtCreate-hide`/`stomtCreate-show`: is fired when the visibility of the Create Widget changes.
- for all Widgets:
    - `widgetType` + `-stomtCreated`: is fired when a user submitted a STOMT. The event data handed to the callback contains the created STOMT and the SDK the event originated from.
    - `widgetType` + `-subscribed`: is fired when a user subscribed your target via the Widget. The event data handed to the callback contains the email or phone number used to subscribe and the SDK the event originated from.

## WebView / Iframe

Instead of using the Javascript snippet you can access the feed page directly in a WebView or Iframe. (For many platforms we did this step for you already and you can grab one of our [SDKs](http://stomt.web/dev).


To embed the form use this url: [https://www.stomt.com/widget](https://www.stomt.com/widget)

To embed the feed use this url: [https://www.stomt.com/feedwidget](https://www.stomt.com/feedwidget)

You can attach all the parameters introduced before (`options.targetId`, ...) to customize the feed for your project:

e.g. `https://www.stomt.com/widget?targetId=stomt&callEN=Tell+us+what+you+miss`




## Contribution

We would love to see you contributing with your ideas to the STOMT JavaScript-SDK. Please addess all your wishes to the [STOMT SDK (JS) on STOMT](https://www.stomt.com/stomt-javascript-sdk). 

## Authors

* [Max Klenk](https://github.com/maxklenk)

## More about STOMT

* On the web [www.stomt.com](https://www.stomt.com)
* [STOMT for iOS](http://stomt.co/ios)
* [STOMT for Android](http://stomt.co/android)
* [STOMT for Unreal Engine](http://stomt.co/unreal)
* [STOMT for Unity 3D Engine](http://stomt.co/unity)
