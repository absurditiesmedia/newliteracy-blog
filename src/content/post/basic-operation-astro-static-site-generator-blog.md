---
publishDate: "23 January 2025"
title: Operation of a Blog Built wirh AstroJS Static Site Generator
description: AstroJS is a powerful means of digital publishing that with a small amount of study can provide a more powerful means of digital publishing than wordpress
tags: ["AstroJS", "digital publishing", "static site generator", "blogging", "markdown"]
coverImage:
    src: "../../assets/intro-digital-publishing-with-static-site-generator-cloudflare-pages.png"
    alt: "AstroJS, nodeJS, and GIT logos on a blue background"
---

Once configured, an AstroJS website only involves a small amount of technical skill. It should be entirely possible for someone with minimal experience with the command line, html and CSS to maintain a website. I will attempt to outline the parts that require continuous maintenance.

## Checking out and running a development instance

The first thing to do when working on an AstroJS website is to either clone the repository of the site you'll be working on, or if you're starting a new site from a theme, you can download or fork the repository of one of the theme found on the [Astro Themes Website](https://astro.build/themes/). If you forked and existing theme, you're all set. Alternatively if you just downloaded the theme, you'll need to create a repository on github or gitlab, and initialize a new repository from the project root by running `git init`. For the purposes of this write up, I'll assume you've already completed this step. I'll write an article outlining this proocess at a leter date, but I'm sure you can find instructions for this elsewhere on the web.

This site was built using astroJS and the following is the abbreviated structure of the project. 

Let's take a look at an abbreviated listing of the files in an astroJS site and go over the important moving parts:

```bash
[project root]
├── astro.config.ts
├── LICENSE
├── netlify.toml
├── package.json
├── package-lock.json
├── pnpm-lock.yaml
├── postcss.config.js
├── public
│   ├── android-chrome-192x192.png
│   ├── android-chrome-512x512.png
│   ├── apple-touch-icon.pnge
│   ├── favicon-16x16.png
│   ├── favicon-32x32.png
│   ├── favicon.ico
│   ├── images
│   │   └── crypto-wallets
│   │       ├── atomic_private_keys_list.png
│   │       ├── atomic_recv_eth_screen.png
│   │       ├── bitcoin-address.png
|   |       ...
│   │       └──exodus_sendeth_screen.png
│   ├── icon.svg
│   ├── images
│   ├── manifest.webmanifest
│   ├── robots.txt
│   ├── site.webmanifest
│   └── social-card.png
├── README.md
├── src
│   ├── assets
│   │   ├── docker_logo.png
│   │   ├── jses6_logo.png
│   │   ├── kubernetes_logo.png
│   │   ├── newlit-ascii-large.png
|   |   ... 
│   │   └── visualstudio_logo.png
│   ├── components
│   │   ├── BaseHead.astro
│   │   ├── blog
│   │   │   ├── Hero.astro
│   │   │   ├── PostPreview.astro
│   │   │   ├── TOC.astro
│   │   │   ├── TOCHeading.astro
│   │   │   └── webmentions
│   │   │       ├── Comments.astro
│   │   │       ├── index.astro
│   │   │       └── Likes.astro
│   │   ├── FormattedDate.astro
│   │   ├── layout
│   │   │   ├── Footer.astro
│   │   │   └── Header.astro
│   │   ├── Paginator.astro
│   │   ├── Search.astro
│   │   ├── SkipLink.astro
│   │   ├── SocialList.astro
│   │   ├── ThemeProvider.astro
│   │   └── ThemeToggle.astro
│   ├── content
│   │   ├── config.ts
│   │   └── post
│   │       ├── basic-operation-astro-static-site-generator-blog.md
|   |       ...
│   │       ├── where-why-use-kubernetes.md
│   │       └── why-use-docker.md
│   ├── data
│   │   └── post.ts
│   ├── env.d.ts
│   ├── layouts
│   │   ├── Base.astro
│   │   └── BlogPost.astro
│   ├── pages
│   │   ├── 404.astro
│   │   ├── about.astro
│   │   ├── index.astro
│   │   ├── og-image
│   │   │   └── [slug].png.ts
│   │   ├── posts
│   │   │   ├── [...page].astro
│   │   │   └── [slug].astro
│   │   ├── rss.xml.ts
│   │   └── tags
│   │       ├── index.astro
│   │       └── [tag]e
│   │           └── [...page].astro
│   ├── site.config.ts
│   ├── styles
│   │   └── global.css
│   ├── types.ts
│   └── utils
│       ├── date.ts
│       ├── domElement.ts
│       ├── generateToc.ts
│       ├── index.ts
│       ├── remark-reading-time.ts
│       └── webmentions.ts
├── tailwind.config.ts
└── tsconfig.json
```

## Configuration Files

Starting from the top,`astro.config.ts` primarily stores a collection of values related to the site. It is descriptively named config because this is where all the configuration takes place. Things like the `site:` which specifies the base url of the site. In this case it's `https://newliteracy.online`, this file also contains settings for the modules used to preprocess css and image files to make them production ready. There are all kinds of functionality that nodeJS modules can provide, such as optimizing media assets for delivery over the web, decreasing the size of css and javascript files and much more that go way beyond the scope of this article and are not *necessary* to understand to get a site up and running. `postcss.config.js` also stores such information. What is in these files can vary widely between themes, it's best to at least glance at their content, but you don't **need** to, nor should you expect to, understand everything that's going on here. 

`package.json`, `package-lock.json` and `pnpm-lock.yaml` specify the node modules that are dependencies in this project. When you check out an AstroJS site, or any other project built on NodeJS for that matter.

## Building and starting the development server

 the first thing you will do is run: 

```bash
npm install
```
or in some cases 

```bash
pnpm install
```

these are just two different implementations of node package managers. Feel free to read about the differences, but at this point it's safe to operate under the assumption that they do basically the same thing, which is to download the dependencies of the project so that you end up with a working development instance. Now you can run

```bash
npm run dev
```
or 

```bash
pnpm run dev
```

This will start the development server. You'll see something like:

```bash
❯ npm run dev

> astro-cactus@4.5.0 dev
> astro dev

 astro  v4.5.16 ready in 1238 ms

┃ Local    http://localhost:4321/
┃ Network  use --host to expose

13:47:07 watching for file changes...
```
informing you that you can view the current state of your site at `http://localhost:4321/ any changes you make to the files will be automatically reloaded and immediately reflected in your browser and the terminal.

## Public Files
The files under the directory `/public` will be accessible from the root of your site. They are served as-is with not preprocessing done to them. If you add images or other media, they can be linked from within your pages or templates directly. For example, try this link [https://newliteracy.online/android-chrome-192x192.png](https://newliteracy.online/android-chrome-192x192.png). Notice that the file `android-chrome-192x192.png` is directly within the `public/` directory. Now try [https://newliteracy.online/images/crypto-wallets/bitcoin-address.png](https://newliteracy.online/images/crypto-wallets/bitcoin-address.png) and notice that the file `bitcoin-address.png` is in the `public/images/crypto-wallets/` directory. Another way of describing this is to say that the files in `public/` are mapped to the **webroot** of the site.

## Site structure: Templates and Components


Now that we've reviewed how to check-out, install, and run the development server. Let's take a look at the files that you'll be working with to modify the site. These can all be found under `src` named for **source**. 

### The assets/ directory

There's a directory called `assets/` where images and other media are stored. You might be wondering why there's a second direcory for this in addition to the `public` directory. Without going into a lot of detail, I'll just note that there exist functionality within node modules to run various operations on these files before making them ready to be served to the client. This could be any number of things, such as minifying css, running images through optimizations, overlaying text on top of the images. These operations are limited only by the developers imagination and the technology that exists at present. Belive me, there are many use cases in which having the ability to run server side modifications on assets is incredibly useful. 

### The components/ and layouts/ directories

Files under `components/` generally have the extension `.astro` which means they can contain Javascript for dynamic rendering. Take a look at the names of the files. They represent, you guessed it, components of the page. `BaseHead.astro` in spite of sharing a name with an prejorative for an individual who has a problematic relationship with freebase cocaine, contains the content that will appear inside the `<head></head>` html tag, it contians variables that will be replaced with different values on each page. A subdirectory `components/blog/` contains the individual parts of the pages that display the listing of blog entries and pages such as the one you're reading right now. 

The subdirectories here are simply a means of providing some level of organization to the components. And they can be arranged and split into different parts in a way that's entirey up to the developer. What works best is something only experience with these types of sites can provide. And there have been and will be many debates on the topic of how to best segment and organize template files for years to come. Many of them occuring within the mind of individual developers. Don't feel bad if you have a difficult time determining what works best. I don't think anyone really knows the answer to that question, and if they claim to. They probably haven't got a lot of experience. d

### The content/ directory

If you're a blogger, content adminsitrator, or novice web developer, this is the section that you'll want to pay the most attention to. 


#### Markdown and HTML (Markup)

Inside the `content/posts/ directory, you'll find primarily a collection of **Markdown** files. **Mardown** is a simplified mark**up** language. (get it, mark**down**). 

Markup languages date back to the days when typesetters had to place individual characters into rows on a print plate to produce a single printed page. (Can you even imagine the tediousness of such a job? I certainly don't want to and even more so I don't envy my predeccessors in the world of publishing) In those days, editors would provide a page of *marked-up* text. Individual parts would be surrounded by tags specifying where text should be bold, italic, a heading and so forth. HTML adds even more abilities such as the hyperlink which allows for quick reference to another document, much like an **in-text citation** to a source referenced by the document. 

Take a moment to reflect on how powerful a creation this is. If you've ever written a research paper, particularly a literature review where you followed such citations to other research on a topic, I'm sure you see the value in having the ability to simply click a link instead of venturing out to the library to search for and retrevie another reference document. 

Back to markdown. HTML markup specifies a very extensive set of tags. But, in the body of an article, you'll most likely only use a very few. probably: 
 - the **hyperlink:** `<a hrer=""></a>`, 
 - bold and italic `<strong></strong>` and `<em></em>`  
 - image embed `<img src=""></img>`, 
 - various headings `<h1></h1>,<h2></h2>...<h5></h5>` 
 - an ordered and unordered list `<ul><li></li>...</ul>` and `<ol><li></li>...</ol>`
 - maybe a table `<table><tr><td></td>...</tr>...</table>` 

Mardown provides a simplified syntax for all of these. They are all documented in this guide: [Markdown Cheatsheet](https://github.com/adam-p/markdown-here/wiki/Markdown-Cheatsheet) a far less daunting list than you'll find in the list of [HTML elements](https://developer.mozilla.org/en-US/docs/Web/HTML/Element) 


#### Anatomy of a Blog Post

Inside the `content/posts` directory, you'll find a collection of markdown files. They should be names with the keywords used in the title leaving out words like 'the', 'and', 'but', 'to' and so forth as the filename will be used to build the url of the page, and search engines prefer these be as short as possible but also descriptive of what will be on the page. Pay attention to the names of the pages in the URL bar on this site. I try to be cognizant of this when I name files. 


##### Metadata

It's also important to note that these files are not just markdown, they contain a section of metadata at the top before which is delimited by three dashes. This tells the markdown parser where the metadata ends and the page content begins. Which fields are required and which are optional is determined by the the settings for the theme. You'll notice a file at the root of the `content/` directory called `config.ts` this contains the definitions for each content type. On this site there is only the one `post`. Let's take a look at the definition:

```
const post = defineCollection({
	schema: ({ image }) =>
		z.object({
			coverImage: z
				.object({
					alt: z.string(),
					src: image(),
				})
				.optional(),
			description: z.string().min(50).max(160),
			draft: z.boolean().default(false),
			ogImage: z.string().optional(),
			publishDate: z
				.string()
				.or(z.date())
				.transform((val) => new Date(val)),
			tags: z.array(z.string()).default([]).transform(removeDupsAndLowerCase),
			title: z.string().max(60),
			updatedDate: z
				.string()
				.optional()
				.transform((str) => (str ? new Date(str) : undefined)),
		}),
	type: "content",
});
```

it looks daunting, but it really is not. What it says here is that the metadata has an optional `coverImage` which is made up of two values (hence the nesting) `alt` and `src` so it's expected that an image and it's alt text will be supplied here. At the end you'll see an `.optional()` that means that a post is not required to have a hero image. 

Next it specifies that a `description` between 50 and 160 characters long be supplied. There is no optional specification so that means this value must be present and with a length per the specifications, if any of those are not met, AstroJS will throw an error and the page will not display. 

Next a boolean (true or false) `draft` is specified with a default value of false. If left out, Astro will assume the post is ready to be published on the production site. And it will be included on pages with listings of posts, if set to false, it will be hidden from those as well as any RSS feeds or sitemaps. 

Next, an `ogImage` this is the image that is displayed when someone links a page on social media. This theme contains a preprocessing script that generates an image with the title of the article, but as you can see we're given the option to override this.

Next, a `publishDate` is specified with a default value of the current date. This is used to determine the date displayed on the article and it's sort order on pages or components where posts are listed.

Then we have `tags` this definition specifies that an array of string be supplied, in english that means something like this ["this", "is", "a", "list", "of", "tags"]. **Array** is another way of saying **list**. The definition here also specifies that everything supplied here be converted to lowercase. A good idea as when the list of articles gets sufficiently large, the author is bound to have made a post with a tag like, "JavaScript" and another with a tag like "javascript" which otherwide would be split into two tags when clearly the intent was for them to be the same.

Finally a required `title` with a max length of 60 characters and an optional `updatedDate` with a default value of the current date are specified.

##### Content
Following the `---` three dashes after the metadata you'll find the content of the post. This is quite simple and I recommend referencing the [Markdown Cheat Sheet](https://github.com/adam-p/markdown-here/wiki/Markdown-Cheatsheet) to guide what you'll put here. Unlike HTML you can create paragraph and line breaks just like you would in a normal word processor. You can add images that you saved to `public/`, though it is advisable you run them through a tinifier like the one at [TinyPng](https://tinypng.com/) (which also handles jpeg, avif, webp) to reduce their file size. If you plan to embed video and you're using cloudflare pages as a means of hosting your content, keep in mind that with that service there is a maximum file size limit of 25MB. For large media files, you have the option of uploading them to a site like youtube, or paying a small fee for a file storage bucket service like backblaze to host your files. The latter will put no restrictions on your content and is so inexpensive that it's most likely the preferable option. However, that all depends on whether you're trying to promote a youtube channel or not. Theses are all things to take into consideration when making decisions regarding the publication of your original content. 

### The pages/ directory
The pages diretory contains static pages that appear on your site, usually the home page, maybe an about page or a contact page. Things of that nature. They differ only slightly from blog posts in most cases, but typically mdx or astro files are used to allowd for the inclusion of components directly. This is also where you might find complex landing pages with a lot of different elements. Notice that `posts/` is mirrored within this directory. That's because this is where the dynamic elements of the the blog are defined. The filename even has a placeholder for the url that's generated based on the filename of the blog post markdown files. Inside these files, you'll find where the metadata is placed throughout the content. If you're just beginning, you really don't need to touch these or completely understand what's going on here. It's worth a look, but if you don't understand, don't sweat it. There are developrs out there with years of experience that won't be able to comprehend all the moving parts here on first or second glance. This stuff isn't supposed to be simple. It's my intent with this article to point out what **IS** made simple by this system, so you can focus on that and make things.

### Other files of note
- `rss.xml.ts`: this file specifies the metadata fields and how they map to the xml tags used in generating an [RSS feed](https://rss.com/blog/how-do-rss-feeds-work/)
- `site.config.ts`: more configuration settings for the site. 
- `utils/` directory: javascript functions for use in preprocessing of whatever data. Things like functions to format dates, or take a date and convert it to something novel like *w days, x weeks, y months and z years ago* you never know how you might need to change some piece of data around. 

## Publishing your changes. 
So you've edited a bunch of files. You've examined your changes thouroghly on your local machine. You've even gotten a second or third set of eyes on it because you become blind to mistakes once you've been working on something for a long time. You definitely want to have **someone else** double check your work. Now you want to share it all with the world. In order to do that you'll need to understand the basics of [version control](https://en.wikipedia.org/wiki/Version_control) and you might as well learn [**GIT**](https://git-scm.com/) specifically since that the one everyone uses now. I'm sure you've heard of [github.com](https://github.com). To be honest, at this point I'd probably be suprised if a boomer didn't know what github was if it came up in conversation. It's really not that difficult. Think about it like a really fancy undo list, where the history is documented and doesn't go away when you close the program. There's also forks, branches, merges, rebasing, conflict resolution and all manner of other things to make you overwhelmed, but you **REALLY** only need to understand how to **clone** a **repository**, how to **commit** your changes, and how to **push** them to the **origin**. If there's more than one person working on your site, you'll also need to know that you'll want to run an **update** before you do anything. 

(but this is what **branching** and **merging** are made to help with... see all the stuff about verion control that makes you overwhelmed... really all the stuff in tech that makes you overwhelmed... all of those things were created to make like easier. So think of it like that when you don't want to learn a new thing. It's 100% there to make it easier to do things.) 

Ok, so when you got your project you ran

```bash
git clone (repository URL a.k.a the **origin** )
```

which put the project into a directory with the same name as the repository. 

then you edited some files...

and if you run

```bash
git status
```

it will indicate that you changed some files and it will also list any new files you created as untracked. 

You can also run

```bash
git diff
```
to see a detailed list of all the changes you made

you can also supply a filename as argument to the `git diff` command to see only the changes to that file.

it should also be pointed out that you can run

```bash
git --help
``` 
to get a list of all the git commands and

```bash
git <command> --help

``
such as 
```bash
git status --help
git diff --help
git add --help
git clone --help
git commit --help
git push --help
git branch --help
git merge --help
git rebase --help
git pull --help
git push --help
```

or

```bash
man git
```
which will provide a detailed manual page with additional man page sections referenced toward the end

```bash
man git-commit
```

has a section like
```
SEE ALSO
       git-add(1), git-rm(1), git-mv(1), git-merge(1), git-commit-tree(1)
```
these are worth reading, but you don't really need to understand this stuff just yet. Just putting it out there for your possible interest. 


Let's focus on what you **need** to understand. 

Ok, so you've seen you diff. And everything looks good. Let's go ahead and add all of the untracked and modified files to be staged for commit. 

`git status` will list the files with their paths relative to your current location in the directory structure, so you can just copy/paste them as they are listed as arguments to git add. You can call `git add` once for each file, you can provide a list of files, or you can just supply the path to a common root directory containing all of the files. 

if you return to the project root and type

```bash
git add *
```
every file, untracked or modified will be added to the commit list/staging area. and when you run

```bash
git status
```
this will be reflected in the output. 

I reccomend that you copy in the path of each file so that you pay attention to which files you changed. It's good to review which changes you made and make note of what you did. It's proper form to provide an adequate description of what your changes were in the message you specifiy with `git commit` it should be something like this:

```bash
git commit -m "created 2 new articles, added new images"
```

and it's even better that you should separate functionally different things into separate commits. You probably would not want to include a change like this along with your addition of new articles.

```bash
git commit -m "fixed an error in the dateParser() function in .... ..."
```

since those two changes are unrelated and it's easy to rollback individual commits, its not so easy to pick out a specific change from within a commit containing several.

Anyway... now you've commited your change, but **git** is what is known as a distributed version control system. There's no central repository, you can specify a copy of the repository as **origin** and that's usually what is done, but when you make a commit, this is only committed to your local copy of the repository. (older version control systems did not store a local copy). Nowadays we have one more step. And that is to run

```bash
git push
```
which will push all your changes to the url specified as the **origin**. you can make as many commits as you like before pushing, so it's adviseable to orgainize them. Later on we can get into the merits of branching, but for now this should be a sufficient introduction to a whole bunch of concepts. 

Congratulations, you can now operate a website and many of the moving parts. If you are able to comprehend this guide, when the job market improves there should be plenty of jobs that pay anywhere from $25-$45/hr that you're now qualified to perform. You're welcome. Keep me in mind when you're shopping for that BMW, moneybags. **BTC: bc1qy2tqwljvv85uppxmlmnxmqlpc7dpaqe87h2ywm**