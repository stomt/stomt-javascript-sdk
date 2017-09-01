# STOMT JavaScript-SDK [![Stomt API](https://img.shields.io/badge/stomt-v2.1.X-brightgreen.svg)](https://rest.stomt.com/)

<a href="http://maxklenk.github.io/angular-sample-app/" title="sample application">
<img alt="Easy Integration" align="right" width="380" src="screenshot-form.png"/>
</a>

* [Demo](#demo)
* [Installation](#installation)
  * [addTab](#documentation---addtab)
  * [addFeed](#documentation---addfeed)
  * [addCreate](#documentation---addcreate)
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


## Documentation - addCreate

The current version allows you to add a STOMT feed somewhere on your page, it searched for an element with the id `stomt_create` and adds the creation form in this element:
```JavaScript
Stomt.push(['addCreate', options]);
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


## WebView / Iframe

Instead of using the Javascript snippet you can access the feed page directly in a WebView or Iframe. (For many platforms we did this step for you already and you can grab one of our [SDKs](http://stomt.web/dev).

To embed the feed use this url: [https://www.stomt.com/widget-feed](https://www.stomt.com/widget-feed)

You can attach all the parameters introduced before (`options.targetId`, ...) to customize the feed for your project:

e.g. `https://www.stomt.com/widget-feed?targetId=stomt&callEN=Tell+us+what+you+miss`




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
