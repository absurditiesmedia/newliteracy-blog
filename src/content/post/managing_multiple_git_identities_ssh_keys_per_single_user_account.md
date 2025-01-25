---
publishDate: "24 January 2025"
title: Managing Multiple Git Identities Per Single User Account
description: It's not uncommon to need to work a variety of projects using different github identities. There are a number of ways to handle this.
tags: ["git", "github", "ssh", "development"]

---

If you need to work make changes to code under different identities, there are a few different ways you can approach this. The first solution I saw on many webpages was way too clunky for my taste. It involved a modification to your `/.ssh/config` file for each repository. I feel like this is a setting that's associated with the specific cloned repository, so why not use the settings associated with that. 

It turns out this is the easiest solution. 

If you're not familiar, when first configuring git, you're prompted to configure you name and email. In the `--global` scope like so:

```bash
git config --global user.name "Your Name"
git config --global user.email "your@email.com"
```

Well this can also be done without the `--global` option on a per repository basis. 

So `cd` into the repository you wish to configure.

You can run the following command to see the current configuration:

```bash
#local 
git config list

#global 
git config list --global
```

now you can set any configuration option you like on a per repository basis. I feel like the best solution to a specific problem is one that, upon learning it, you gain utility beyond the specific thing you were trying to do. This is one of those cases. 

So what settings must be overridden to associate a cloned repository with a specific identity?

In order to do this you'll need to set the `user.name`, `user.email` and to associate with a specific ssh key, you'll use the `core.sshCommand` setting.

So run the following and you'll be good to go:

```bash
git config user.name "Your Name"
git config user.email "<email address>"
git config core.sshCommand "ssh -i ~/.ssh/<your ssh key>"
```

And that's it. Very simple. 