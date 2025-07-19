---
publishDate: "18 Jul 2025"
title: Another AstroJS Adminsitration Tutorial
description: I didn't feel my first attempt at the subject was accessible enough
tags: ["cms","ssg"]
---

# astro administration part 1 

This tutorial should serve as a companion to the one here [Operation of a Blog Built with AstroJS Static Site Generator](https://newliteracy.online/posts/basic-operation-astro-static-site-generator-blog/) which upon reading I felt was incomplete.

there are a bunch of themes listed on [https://astro.build/themes](https://astro.build/themes), but so far, I think that [Astro Paper](https://github.com/satnaing/astro-paper) is the best. Feel free to try installing a few once you've completed this tutorial. 

![kitty](/images/astro-pt-2/kitty.png?7)
![it has kittens](/images/astro-pt-2/kitty-kitten.png?9)
1. Open terminal emulator. My personal favorite is Kitty, but you can use the system default if you don't want to install anything. Open the launcher and start typing "terminal" or "console", you'll find one.

The following apply to every terminal emulator I've used. 
   
- `ctrl-shift-t` opens a new terminal tab, most `ctrl` commands must be combined with shift because the cli has its own set of `ctrl+` commands. For instance, `ctrl-c` in the cli will kill the foreground running process, overriding the default "copy". In the terminal, add `shift` to the default shortcuts `ctrl-shift-c` copies text, `ctrl-shift-v` likewise to paste... 
  
- You can also just select text and press the mouse wheel to paste from that separate clipboard
    

2. cd into a directory where you want to put your development projects   

```
mkdir Development
cd ~/Development/
```
![mkdir ~/Development](/images/astro-pt-2/cli-step-2a.png)

3. make a directory for your astro sites 

```
mkdir my-astro-sites
```
and  cd into it

```
cd my-astro-sites
```

![cd into my-astro-sites](/images/astro-pt-2/cli-step-3a.png)

![open astro paper project page on github](/images/astro-pt-2/github-step-1.png)

4. back in the browser at  [Astro Paper](https://github.com/satnaing/astro-paper). go to the **code** button: click it... 

![click code button on github project page](/images/astro-pt-2/github-step-2.png)

...and right click on **download zip** copy the link address. Then go back into the command line interface console window.

![wget command to download theme](/images/astro-pt-2/github-step-3.png)

5. Download the link you copied using `wget` or `aria2c`

```
wget https://github.com/satnaing/astro-paper/archive/refs/heads/main.zip
```

or

```
aria2c  https://github.com/satnaing/astro-paper/archive/refs/heads/main.zip
```

![unzip downloaded package](/images/astro-pt-2/cli-step-5.png)

6. depending on which downloader you used you'll either have a file named `main.zip` or `astro-paper-main.zip`. unzip it using `unzip` 

```
unzip main.zip
```


7. move (rename) the unzipped directory to something better descriptive
```
mv main my-new-astro-site
```

8. cd into it

```
cd my-new-astro-site
```


9. now, you'll use a program called `npm` which is the **node package manager** this is the primary command you'll use when developing with nodeJS, it handles setting up development and production environments by downloading dependencies, running the development server, and running the scripts involved in packaging assets (this can be all kinds of things from minifying css, running sass/scss css compilers, converting typescript to javascript, builing static sites) for use in production. You'll notice cli programs that do many different things like **npm** will have a <command> as their first argument. 

```
npm <command> <options> 
```

![npm](/images/astro-pt-2/npm-commands.png)


Such programs will often have a separate `--help` screen and `man` page for each command. 


| `man npm install` | `man npm` |
| --- | --- |
| ![npm](/images/astro-pt-2/man-npm-install.png) | ![npm](/images/astro-pt-2/man-npm.png) |


we're going to use the subcommand  `install` here to install the dependencies for the astro theme you downloaded. (an astro theme is really more like a distribution of astro since it contains the complete set of files necessary to create an astro site project)

```
npm install
```

![npm install](/images/astro-pt-2/cli-step-7.png)


that will take a little while. once it's done, you're going to run another `npm` subcommand. this one will be specified by the astro project. and you can find in in the file `package.json`. take a moment to look at `package.json` 

now run `npm run dev`

![npm run dev](/images/astro-pt-2/cli-step-8.png)

```
npm run dev
```

if it completes without error you should be presented with a url you can view your site on. leave `npm run dev` running and any edits you make to the code will be automatically updated on this test server 

10. Now you'll want to open the IDE to edit your site's files, add content etc. The program **vscodium** is a fork of **VSCode** which is one of the more widely used IDEs (for good reason, it's good software).

![open vscoduim](/images/astro-pt-2/open-vscodium.png)

11. Find your project in the explorer pane (default is to the left)

![find your project in vscodium](/images/astro-pt-2/your-project-in-vscodium.png)

12. Expand your project's directory structure. Most of what you'll edit will be under `./src/`, but there are a few configuration files at the project root that you'll want to be aware of what they're for to edit as well .

![your project files in vscodium explore pane](/images/astro-pt-2/your-project-files.png)

13. In this version of astro paper, new blogs are added under 

```
src/data/blog
```

take a look at the files that are already there

some assets (images etc) are stored under 
```
./public/assets
```

and others are stored under

```
./src/assets/
```

the difference depends on whether the paths get run through javascript at any point, if not, you must place them in `public` which automatically everything under that directory is copied to the `dist` directory on production build. (when building the site for production, you'll run `npm run build` and [read my tutorial about how to admin an astro site on newliteracy.online](https://newliteracy.online/posts/basic-operation-astro-static-site-generator-blog/)  the entire site will be built under ./dist, try it and have a look for yourself. )

```
npm run build
```

```
cd dist

ls -al
```

see

also remember you can access the files from the cli, from vscodium or any file explorer program like dolphin

![files in dolphin](/images/astro-pt-2/in-dolphin.png)

remember you can navigate up in the directory tree here with 'alt+arrow up'

ok, now 
1) try editing the configuration files necessary to make this site your own. and 

2) add a few blog entries that you have chatGPT write for you

read [Operation of a Blog Built with AstroJS Static Site Generator](https://newliteracy.online/posts/basic-operation-astro-static-site-generator-blog/) if you haven't already, it has more information about this process for you.

