---
layout: project_entry
year: 2015
title: Website Mark 2
top_image_link: "/projects/website_mark_2/pics/website_mark_2.png"
tagline: simple, scalable, and not-too-shabby looking
---

# {{ page.title }}

<center>
<img src="{{page.top_image_link}}"
vspace="15px">
</center>

***
Gone are the days where posting projects was a hard-coded html hassle--and may they never return!
In rebooting this website, I wanted a workflow that was simple for adding content, easy to maintain, and scalable over the years.

After chewing through some of the internet, I settled on [Jekyll](https://jekyllrb.com/)
***

## Keeping it Simple
Wordpress is great for quickly adding content, but the need for constant updates and comment moderation seemed a bit too much for my tastes.
I found Jekyll among the slew of open source tools for writing static pages, and I loved the idea of writing content in clean Markdown files and tracking changes with Git.
In the quest for a website that could be generated from just a small number of files and tested live without an internet connection, I opted for Jekyll. There are a couple of small sacrifices here: By restricting my writeups to Markdown I deny myself some formatting niceties, but it also keeps me focused on writing content, rather than dressing it up. Finally, I can inject any inline-html anywhere in the Markdown files in case I do need a few more formatting options. 
***

## Layout
The key features weren't too demanding: a front page; a running list of projects, notes, and rants; and an easy way to actually type it all up.

To generate the __project list__, __notes list__, and __blog post__ pages, I wrote a couple of control loops that filter for posts based on their category with Jekyll's Liquid templates. Liquid doesn't have a super-comprehensive [set of operations](https://github.com/Shopify/liquid/wiki/Liquid-for-Designers), but it's enough to get the job done.
(Here's the [snippet](https://raw.githubusercontent.com/Poofjunior/website/master/projects_list.md) that generates the links in the __project list__ page.)

<center>
<img src="/projects/website_mark_2/pics/auto_list_generation.png"
vspace="15px">
</center>

56 lines of code to automagically append new projects to the list when I create a new project entry? I'll take that.
To guarantee that posts are appended in alphabetical order, I just need to adhere to a naming scheme of `<year>-<month>-<day>-<post-title>.md`, but I can organize them with whatever file structure I prefer, since Jekyll recursively searches the top-level directory to find all posts.

***
## The Workflow
To create a new project, I just need to start a markdown file with the a quick header at the top that looks like this:
    
    ---
    layout: project_entry
    year: 2015
    title: Website Mark 2
    top_image_link: "/projects/website_mark_2/pics/website_mark_2.png"
    tagline: simple, scalable, and not-too-shabby looking
    ---
    
    start writing markdown here...
    
    
The __project\_entry__ tag flags this entry as a project to be appended to the project list, and the __top\_image\_link__ points to the image to render in that list.

From there, the rest of the file looks like conventional markdown.

Each time I save new file changes, Jekyll updates any changed files, regenerates the relevant list pages if needed, and outputs html files that I can then upload to a server.

At last! These days, starting a new writeup is as easy as popping open a text editor, pasting the preamble, and starting to punch out words.
***
