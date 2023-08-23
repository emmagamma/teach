##### Before continuing, you may want to refresh your knowledge on bash:

---

> [Get more familiar with bash](LEARNBASH.md)

---

# Simplest way to make a Website

We don't need to create an HTML file seperately, since `vi`, `vim`, `nano`, or `subl` will create the file for you if it doesn't already exist. But if you like you can create it first before opening it to modify.

`touch ~/Code/YourProjectDirectory/index.html`

... of course, be sure to replace `YourProjectDirectory` with the name of the directory you've created your project in.

Next we need to open the file. Nano may be the most user friendly for you at first, whereas vi/vim will require looking at a brief tutorial to even figure out how to quit out of a file or how to enter insert mode to edit the contents. so either:

1. `nano ~/Code/YourProjectDirectory/index.html`

2. `vi ~/Code/YourProjectDirectory/index.html` // should be installed on most distros

3. `vim ~/Code/YourProjectDirectory/index.html` // may requiring first installing vim

4. `nvim ~/Code/YourProjectDirectory/index.html` // requires first installing neovim

5. `code ~/Code/YourProjectDirectory/index.html` // requires first [installing VSCode](https://code.visualstudio.com/download) and [additional steps on windows](https://learn.microsoft.com/en-us/windows/wsl/tutorials/wsl-vscode#install-vs-code-and-the-wsl-extension) to make sure the `code` command is available in WSL.

or if you use sublime text, you can follow [this guide](https://www.sublimetext.com/docs/command_line.html) to set it up as a command line tool (you should be able to use the section for ZSH if you have Zshell set up, regardless of host OS) then you'll be able to use this command to open the file with sublime text:

6. `subl ~/Code/YourProjectDirectory/index.html`

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

Now save the file and that's it! we've created our first website... well, kindof. lol

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
    * this just denotes the beginning of an HTML file and that we're using the latest version of HTML.
    * it's a mildly annoying convention but it lets us release updated versions of HTML, currently on v5.3 as of 2021 (I'm writing this in 2023) and there will undoubtedly be other versions in the future, but if we didn't have this tag at the start of every HTML document, you wouldn't be able to specify older versions if you need certain features for backwards compatability reasons or what have you.
2. after that is an <html\> element, which has a closing tag at the end of the file.
    * unlike <!DOCTYPE\> which has no closing tag.
3. the <html\> element should always only contain a <head\> and then a <body\>
4. inside the <head\> is mostly metadata
    * we have a <title\> element which sets the text in the browser tab for that page.
    * as well as <meta\> tags which can contain all sorts of metadata about our site.
    * and the <style\> element for inline CSS styles, although typically we would use a <link\> element instead and link to css defined in a separate file.
5. the <body\> element contains all the elements that will be rendered to the page and show up visibly.
6. the <script\> tag usually has a `src` attribute on it, with the path to the javascript in another file, rather than defining the javascript "inline", meaning inside the HTML file as we did in this example.
7. note that we place the <script\> tag at the end of the body, this is because often times our javascript will take some extra time to load, but we want the styles and contents to display to the user before the javascript has even loaded. If we were to instead place it inside the head, which is still valid/allowed, it would (in most cases) have to load our javascript before rendering the contents of the body and could make our page feel slow. so you can put your javascript elsewhere, but typically you'll want it to go at the end of the body element.
8. the meta tag with `charset="utf-8"` lets anything parsing our file know that we're using unicode characters.
9. the meta tag with `viewport` makes it so that on mobile devices things are scaled properly. most desktop browsers will ignore it completely, but tablets and phones will often respect it.

# Defining JS and CSS in separate files

So the reason we didn't include CSS and JS as separate files in the previous section is because it wouldn't have worked.

By opening the html file directly in chrome, we avoided serving the html file as an asset from an actual server, even if it's just running locally on our own machine. So in order to get file-linking to work properly, those files can't just be stored on our hard drive, they need to be served from a program called a web server. This is usually what people refer to as the 'backend' of an application. The simplest way to serve files over a web server would be with something like python or http-server which both have simple one-line commands you can run to just serve all files within a given folder as assets for a website.

However this is less than ideal, since often times our projects will contain a number of other files we *don't* want to ever serve to clients, and also hopefully this is already obvious to you but it's fine if not, we lack control in this environment. We can't run any custom logic to decide how or when to serve a file or not, and we can't compose data from multiple sources to return a single response or anything else you might normally need a webserver to do.

But just for standing up a small project or testing out a simple website, these options can be quite powerful and convenient:

```python
# with python, in this instance `9001` is the port that the server will be listening for connections to.
python -m SimpleHTTPServer 9001
# after running this command, you can see the page at http://localhost:9001 in your browser of choice.

# or with python3, you may need to run it this way instead:
python3 -m http.server 9001
```

and make sure to run these from within your project directory, otherwise you may wind up serving the wrong folder but that's harmless and should be obvious pretty quickly when you visit the page.

or you can install http-server, if you'd rather not use python, with either brew or your package manager of choice. just follow [the docs for http-server](https://github.com/http-party/http-server) and then you'll be able to use the following command:

```bash
# http-server <path> <options>
http-server ./ -p 9001
# and there are more options available in the link to the docs, above.
```

also by the way, the port 9001 was just an arbitrary choice I made, you can pick any port so long as it's not being used already. there's even the option `-p 0` which will cause http-server to search for an open port and pick the first available one it see's. and don't worry if you don't know which port to go to, the output from the command should show you which port it's running on.


