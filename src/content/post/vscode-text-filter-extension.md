---
publishDate: "19 January 2025"
title: Visual Studio Code - Creating a Custom Text Filter Extension
description: Incredibly powerful feature, the ability to create filters and run secected text through any command line script or program. 
tags: ["vscode", "extensions", "cli", "IDE", "text editor", "javascript"]
coverImage:
    src: "../../assets/newlit-ascii-large.png"
    alt: "newliteracy business card image passed through letterpress then displayed in the terminal "
---

In this post I will describe a way to create an extension which allows the user to receive the selected text as a string passed into a Typescript function, run that string through any command line program receive the response as a string in Typescript then return the value of the string that will replace the selection. The user can define as many such functions as they want and bind them to various keyboard shortcuts.

The first thing we will need is to install [Jeff Hykin's Selection Convert Extension](https://github.com/jeff-hykin/selection-convert.git). 
I'm sure this is not the only extension that will achieve this end, but I found this one and it works. 

I encourage the reader to spend some time looking for other extensions and attempt to arrive at the same result with another. I followed another such guide that reccomended a different extension myself, and I was unable to make it work. Sometimes things are needlessly complex, and I often find myself frustrated with the instructions given by articles like this one written by other people. It is in these times that I stop. Think about the problem I'm trying to solve, ensure that I understand all the moving parts and then try to ensure the solution I've found written is the most streamlined for the problem I'm trying to solved. If it is not, I should have at least gleaned some understanding of the moving parts from what I've read. I'll begin searching the documentation, asking questions to LLMs, and searching stack overflow until I can formulate my own solution. Usually in so doing this, I will learn so many things more things about the technology I'm working with than I had set out to learn. 

Anyway back to the details. Once `Selection Convert` is installed, you need to invoke it by pressing `Ctrl+Shift+P` and then typing `Selection Convert`. You will then see a list of options appear. The first option is `Selection Convert: Convert Selected Text`. Click on it. This will open the file `$HOME/.vscode/selection-convert.js` where the Typescript functions to define each filter will be stored. In this file, you will create a function for each filter you want to create, and then provide those functions as exports. The Selection Convert Module will create additional items under the `Selection Convert: Convert Selected Text` menu for each function exported in `selection-convert.js`.

Let's have a look at an example `selection-convert.js` file:

```js
const { execSync } = require('child_process');

//Filter Export Functions

// -- function for Boxes - gradientbox-----------------------------------------

selectionToParchment = function(text) {
  var result = runFilter(text, 'parchment');
  return result;
}

selectionToHeadline = function(text) {
  var result = runFilter(text, 'headline');
  return result; 
}

// --/ END Filter Export Functions /--

runFilter = function(text, design) {
  var command = "echo \""+text+"\" | boxes -d "+design+" -p h1 -s 80 -i none -n UTF-8"
  var result = "";
  result = execSync(command);
  return result.toString();
}

module.exports = { selectionToHeadline, selectionToParchment };
```

The above file depends on the `boxes` command line tool. You can install it with `npm install -g boxes`. The `boxes` tool is used to convert the selected text into a box. `boxes` provides a number of filters to place the selected text into various frame designs. There are infinitely many possible uses for the framework provided by selection convert. Spend some time reflecting on the power of this one simple extension. Let's review this line by line. 

`const { execSync } = require('child_process');` 

This line is a common way to use the `child_process` module in Node.js. It allows us to run command line tools from within our Typescript code. Notice, I've imported `execSync` that's because the `child_process` module also provides an asynchronous `exec` module but that's not very useful here since we're expected to provide a function that returns a string. The `execSync` is a syncronous version of the `exec` function so it's possible to return a value from a function that will be called by the IDE. If we needed to call an asynchronous function from within the function called by the menu item, we would run into problems as asyncronous functions are generally written by passing a pointer to a function they should call upon completion. That's essentially what `selection-convert.js` is except we've passed the functions we define to the menu-items in VSCode. And we've no way to specify which function to call with the replacement text, we can only replace this text by returning from the function, so we need a syncronous function to get the result from the command line.e

Next we define the a filter function.

```javascript
selectionToParchment = function(text) {
  var result = runFilter(text, 'parchment');
  return result;
}

```

which passes the `text` though `runFilter`

```javascript
runFilter = function(text, design) {
  var command = "echo \""+text+"\" | boxes -d "+design+" -p h1 -s 80 -i none -n UTF-8"
  var result = "";
  result = execSync(command);
  return result.toString();
}
```

In `runFilter` the most important line is `var command = "echo \""+text+"\" | boxes -d "+design+" -p h1 -s 80 -i none -n UTF-8"` where we see an example use of a command line program on the text. Notice in this case, the text must be echoed on the command line then piped through the program. Normally this is done when a program expects a file as input. There are so many text filtering utilities that this extension can be modified to use. Please, I encourage you to share your ideas for possible uses with me, so that I can list them as an addendum to this post.







