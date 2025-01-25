---
publishDate: "06 May 2024"
title: Linux Journaling Software for the Command Line (CLI)
description: Take notes about what you learn while developing or admining 
tags: ["journaling", "notes", "cli", "linux"]
coverImage:
    src: "../../assets/docker_logo.png"
    alt: "docker logo"
---


---
## Logfile Viewers
---
## Gnome Logs
## kjournal
## Journal Viewer

---
## Commandline Journaling
---
## TUI Journal
## Bournal
Bournal is a commandline journal editor, it features password protection and an interactive mode, it's a good option if you want to be able to return to older notes and edit them. I've used `jrnl` in the past and find it preferable due to the low overhead adding entries, if you don't mind the overhead required to enter a password and prefer interacting in the shell rather than memorizing command line options. It also features snarky status and error messages,
## noto
## cournal
## bok
## chronicle
chronicle is very simple, it creates a directory at `~/.chronicle` underneath this directory are a series of subdirectories `year/month/day` containing textfiles named hour:minute:second in 24 hour format. This option is low overhead
and in my opinion approaches the usablility of `jrnl`		
## jrnl
`jrnl` is great, it stores your journal in a single text file. You're prompted to provide a location on first run. I chose a location in my synced remote storage directory. simply running the concise `jrnl` opens a new note. `jrnl --list` presents you with a list of journal files. `jrnl --edit` opens the entire file for editing. It's also possible to enter short entries as an argument to `jrnl` like this `jrnl this is an entry`
---
## GUI Journaling
---
## Red Notebook
## Lifeograph
			

