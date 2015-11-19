# JavaScript Templates for Visual Studio
The templates are also available as a VSIX in the [Visual Studio Gallery](https://visualstudiogallery.msdn.microsoft.com/49cdc7d0-95e7-48dd-8a6a-141cb66e726e)

## Contents
- [BlankTemplate](#BlankTemplate)
- [BlankTemplate (Web Context)](#BlankTemplateWeb)
- [HostedTemplate](#HostedTemplate)
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
The JavScript file is completely empty. It just contains a comment
```JavaScript
// Your code here!
```

I played with using `onload` and `DOMContentLoaded` events, but decided against it&mdash;it's
simpler to keep the script at the bottom of the `<body>` tag. This seems to account for the
largest number of scenarios and is the easiest for developers to understand.

I've also removed the `IIFE`. A developer who knows what they are can easily add it themselves, and it could add
unnecessary confusion for a newer developer.

### CSS
The CSS file is essentially also blank. It just contains a body selector with the ability to uncomment out a line to enable scrolling and zooming in a WWA.
```CSS
body {
  /* Uncomment this to enable scrolling and zooming
  touch-action: manipulation;
  */
}
```
I am considering having this file completely blank and renaming it to `style.css`.

<a name="BlankTemplateWeb" />
## BlankTemplate (Web Context)
This is the same as the above, except with `ms-appx-web:///`

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

The project also contains `msapp-error` pages.

Something I'd like to potentially try out would be potentially having the `StartPage` point to some
type of tutorial or documentation for Hosted Apps.

<a name="WinJSTemplate" />
## WinJS Template
The WinJS template is mostly the same as the old default template. We want to make sure developers understand that it is not necessary to use WinJS in order to develop a JavaScript app on Windows.

### HTML
The `index.html` file has been updated to include the `win-type-body` class on the `<body>` tag. This was one of the breaking changes from `WinJS`.
