##### Before continuing, you may want to refresh your knowledge on bash:

---

> [Get more familiar with bash](LEARNBASH.md)

---

# Simplest way to make a Website

We don't need to create an HTML file seperately, since `vi`, `vim`, `nano`, or `subl` will create the file for you if it doesn't already exist. But if you like you can create it first before opening it to modify.

`touch ~/Code/YourProjectDirectory/index.html`

Next we need to open the file. Nano may be the most user friendly for you at first, whereas vi/vim will require looking at a brief tutorial to even figure out how to quit out of a file or how to enter insert mode to edit the contents.

`nano ~/Code/YourProjectDirectory/index.html`

`vi ~/Code/YourProjectDirectory/index.html` // should be installed on most distros

`vim ~/Code/YourProjectDirectory/index.html` // may requiring first installing vim

or if you use sublime text, you can follow [this guide](https://www.sublimetext.com/docs/command_line.html) to set it up as a command line tool.

then, you'll be able to use this command to open the file with sublime text:

`subl ~/Code/YourProjectDirectory/index.html`

---

> you can use nano, vi or vim, sublime text, VS Code, notepad, or any other text editor.

> Preferably though, not notepad lol.

---

But however you open it, modify the file's contents to be:

```html
<!DOCTYPE html>
<html>
<head>
  <meta charset="utf-8">
  <meta name="viewport" content="width=device-width, initial-scale=1">
  <title>a simple website</title>
</head>
<body>
  <main>Gweeting, Earfwings!</main>
</body>
</html>
```

And that's it, we've created our first website... well, kindof. lol

It's not hosted anywhere, so nobody else will be able to view it, but we can simply open this file with our web browser of choice now and it will render a web page. Here's how you would open it in chrome whether you're on linux, macOS, or windows with WSL enabled:

`open -a "Google Chrome" ./index.html`

or if you're in another directory, provide the absolute path:

`open -a "Google Chrome" ~/Code/YourProjectDirectory/index.html`

Any additional HTML we put in the body will show up when we refresh, and we can even include CSS and javascript directly inline, like this:

```html
<!DOCTYPE html>
<html>
<head>
  <meta charset="utf-8">
  <meta name="viewport" content="width=device-width, initial-scale=1">
  <title>a simple website</title>
  <style type="text/css">
    h1 { color: red; }
  </style>
</head>
<body>
  <main>
    <h1>Gweeting, Earfwings!</h1>
    this text is normal, but the text above is red
  </main>
  <script type="text/javascript">
    // open your browsers dev tools
    // either by right clicking and selecting "inspect element"
    // or by pressing Cmd + Alt + i, or for windows: Ctrl + Alt + i
    // the message should be visible in the console
    console.log("javascript is working");
  </script>
</body>
</html>
```

So as you can see here, we've added a <style\> element and a <script\> element, as well as adding an h1 element to the main that's inside the body. Don't worry if you don't quite know yet what all of those things mean, we'll go more in depth on HTML elements later.

For now, the important things to note are that:

1. we have to start every HTML document with a <!DOCTYPE html\> element.
    * this just denotes the beginning of an HTML file
2. after that is an <html\> element, which has a closing tag at the end of the file.
    * unlike <!DOCTYPE\> which has no closing tag.
3. the <html\> element should always only contain a <head\> and then a <body\>
4. inside the <head\> is mostly metadata
    * we have a <title\> element which sets the text in the browser tab for that page.
    * as well as <meta\> tags which can contain all sorts of metadata about our site.
    * and the <style\> element, although typically we would use a <link\> element instead with the css defined in a separate file.
5. the <body\> element contains all the elements that will be rendered to the page and show up visibly.
6. the <script\> tag usually has a `src` attribute on it, with the path to the javascript in another file, rather than defining the javascript "inline", meaning inside the HTML file.
7. note that we place the <script\> tag at the end of the body, this is because often times our javascript will take some extra time to load, but we want the styles and contents to display to the user before the javascript has even loaded. If we were to instead place it inside the head, which is valid, it would (in most cases) have to load our javascript before rendering the contents of the body.
8. the meta tag with `charset="utf-8"` lets anything parsing our file know that we're using unicode characters.
9. the meta tag with `viewport` makes it so that on mobile devices things are scaled properly.

# Defining JS and CSS in separate files

...
