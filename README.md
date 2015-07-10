# JavaScript Templates for Visual Studio

## Contents
- [BlankTemplate](#BlankTemplate)
- [HostedTemplate](#HostedTemplate)
- [LifecycleTemplate](#LifecycleTemplate)
- [WinJSTemplate](#WinJSTemplate)

<a name="BlankTemplate" />
## BlankTemplate
The `Blank Template` is about as barebones as it gets. The primary goal of this template
is to make it clear that developing a Windows JavaScript App is no different than
developing a standard WebApp.

### HTML
The HTML file is essentially a plain HTML document:
```html
<!DOCTYPE html>
<html>
<head>
  <meta charset="utf-8" />
  <title>$safeprojectname$</title>
  <link href="css/default.css" rel="stylesheet" />
</head>
<body>
  <div>Content goes here!</div>
  <script src="js/main.js"></script>
</body>
</html>
```

### JS
I opted to keep the JavScript file completely empty. It just contains a comment
```JavaScript
// Your code here!
```

I played with using `onload` and `DOMContentLoaded` events, but decided against it&mdash;it's
simpler to keep the script at the bottom of the `<body>` tag. This seems to account for the
largest number of scenarios and is the easiest for developers to understand.

I've also removed the `IIFE`. A developer who knows what they are can easily add it themselves, and it could add
unnecessary confusion for a newer developer.

### CSS
The CSS file is essentially also blank. It just contains a body selector.
```CSS
body {
}
```
I am considering having this file completely blank and renaming it to `style.css`.

<a name="HostedTemplate" />
## HostedTemplate
The Hosted App format is different enough from a packaged app that having a template for it
does add some value.

### Manifest
This is the biggest reason having a template for Hosted Apps is important. In the `Blank Template`,
the `<uap:ApplicationContentUriRules>` section is not neccessary. However, it is required for
Hosted Apps to work.

Currently, the manifest included in the template includes a remote start page:
```xml
<Application
  Id="App"
  StartPage="https://example.com">
```
and ACURs:
```xml
<uap:ApplicationContentUriRules>
  <uap:Rule Type="include" WindowsRuntimeAccess="all" Match="https://example.com" />
</uap:ApplicationContentUriRules>
```

Something I'd like to potentially try out would be potentially having the `StartPage` point to some
type of tutorial or documentation for Hosted Apps.

### Error Page
I haven't gotten around to adding these, but it would be nice to include the `msapp-error` files. This
would be another differentiating point from normal Packaged Apps.

<a name="LifecycleTemplate" />
## LifeCycleTemplate
This is a more experimental template. The old WinJS template included stuff from the `AppModel` that
could be potentially useful.

That being said, I'm still on the fence as to whether or not it's useful enough to be it's own template.

Currently the template is still under construction, and not particularly functional.

<a name="WinJSTemplate" />
## WinJS Template
I ended up creating an extremely simple WinJS Template. 

### JS
It seems like the whoever came up with the original WinJS templates seems to really like wrapping their
code in `IIFE`'s. While they are good to have, that does not inherently mean they should be included in a template.
```JavaScript
WinJS.UI.processAll().then(function() {
  //Your code here
});
```
Having the function being passed into the WinJS promise already isolates the scope sufficiently, so there isn't a good reason to wrap it into another `IIFE`. In fact, it might be a good idea to remove it from the [WinJS Generator](https://github.com/winjs/generator-winjs) as well.

### HTML
The `index.html` file has been updated to include the `win-type-body` class on the `<body>` tag. This was one of the breaking changes from `WinJS`.
