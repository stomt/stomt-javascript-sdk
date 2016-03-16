# stomt JavaScript-SDK [![Stomt API](https://img.shields.io/badge/stomt-v2.1.X-brightgreen.svg)](https://rest.stomt.com/)

<a href="http://maxklenk.github.io/angular-sample-app/" title="sample application">
<img alt="Easy Integration" align="right" width="380" src="screenshot-form.png"/>
</a>

Our SDK allows you to add the feedback solution [www.stomt.com](https://www.stomt.com/) to your websites or any other HTML/JavaScript based applications. The SDK currently allows you to add a button to your website, which when used open a stomt creation form. In the form customers can choose if they want to speak a wish or praise your site and then enter their thoughts. All submitted ideas can then be manages on the stomt website, where they can be discussed, voted and finally come true. 

To connect your site to stomt, [create a project page on stomt](https://www.stomt.com/createTarget) first.

## Demo

View the live demo [here](http://maxklenk.github.io/angular-sample-app/). The projects [source](https://github.com/maxklenk/angular-sample-app) can be found on GitHub, it itegrates the sdk dynamically in the [index.html](https://github.com/maxklenk/angular-sample-app/blob/master/app/index.html#L58) file.


## Installation

To install the stomt JavaScript-SDK you have only to add the following lines to the bottom of you html file:

```html
<script>
  // Include the Stomt JavaScript SDK
  (function(w, d, n, r, t, s){
    w.Stomt = w.Stomt||[];
    t = d.createElement(n);
    s = d.getElementsByTagName(n)[0];
    t.async=1;
    t.src=r;
    s.parentNode.insertBefore(t,s);
  })(window, document, 'script', '//www.stomt.com/widget.js');
  
  // Add a button to the website which opens a creation modal
  // -> the targetID is your pages identifier you can copy it from the pages url
  //    https://www.stomt.com/stomt-javascript-sdk -> stomt-javascript-sdk
  //
  Stomt.push(['addTab', {targetId: 'stomt-javascript-sdk'}]);
</script>
```



## Documentation

The current version allows you to add a Feedback button to your page:
```JavaScript
Stomt.push(['addTab', options]);
```

### options.targetId

The `options` object has to contain a `targetId`. The `targetId` is your pages identifier you can copy it from the pages url (https://www.stomt.com/stomt-javascript-sdk -> stomt-javascript-sdk). All stomts created using the JavaScript-SDK will be addessed to this page:
```JavaScript
Stomt.push(['addTab', {targetId: 'stomt-javascript-sdk'}]);
```

### options.position

Optionally you can set the `position` of the button, the default possition is `right`. If required you can align the button to the left side by passing `position: 'left'`:
```JavaScript
Stomt.push(['addTab', {targetId: 'stomt-javascript-sdk', position: 'left'}]);
```

<a href="http://maxklenk.github.io/angular-sample-app/" title="sample application">
<img alt="Easy Integration" align="right" width="380" src="screenshot-success.png"/>
</a>


## Contribution

We would love to see you contributing with your ideas to the stomt JavaScript-SDK. Please addess all your wishes to the [stomt SDK (JS) on stomt](https://www.stomt.com/stomt-javascript-sdk). 

## Authors

* [Max Klenk](https://github.com/maxklenk)
