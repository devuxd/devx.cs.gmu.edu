# Few Notes from Liquid  
  
The Liquid language is specified by `{% ... %}` and `{{ ... }}`. The first one is used for calling operators like `for`, `if`, `assign`, `endif`, etc. The latter is used for referencing a variable. More information can be found in the [official Liquid documentation](https://shopify.github.io/liquid/).  
  
The `site` variable is a global variable accessing data specified in `_config.yml`. For example, `site.projects` refers to data files in `_projects`, or `site.baseurl` refers to the url set in `_config.yml`.  
  
The `page` variable refers to the data in the *caller file*. For example, for the following data file, we have `page.pageTitle`, `page.pageDesc`, `page.pageDate`, and `page.content`.  
  
```  

---  
pageTitle: some Title  
pageDesc: some description for the file  
pageDate: some date information  
---  
Some description that is accessed by page.content.   
This info can be written in `markdown` format.  

```  
  
More information can be found in the [Jekyll website](https://jekyllrb.com/docs/variables/).  
  
# Main Pages    

There are 5 main pages: `index.markdown` (home page), `gallery.markdown`, `news.markdown`, `people.markdown`, `projects.markdown`, and `publications.markdown`. These main pages are specified in the root of `docs_src` in markdown files. The format of these files are as follows:   

``` 

--- layout:  <a layout from _layouts>      
title: <some title>    
permalink: /<the link for the page>/    
--- 

```   

`layout` specifies the layout on which the page is rendered.  
`title` specifies the title of the page. `permalink` specifies how the page is accessed. More info can be found in the [Jekyll website](https://jekyllrb.com/docs/permalinks/).    

# Template Directories
    
`_layouts` and `_includes` are `HTML` files act as templates that are filled with data.  

## _layouts
   
The main `_layout` is `default` which sums up everything in a full `HTML` page.  
It starts by including `head.html` and `header.html` from `_includes` and adding the content of the *caller*.  
  
Other layouts must identify how to be rendered. That is they should include the following header on top to call the `default` layout.   

```
  
---  
layout: default  
---  

```  
  
The layouts that are called by main pages are:  
  
 - `gallery` is called by `gallery.markdown`. It reads data from `_pagedata > galleryPageData.md` 
 - `home` is called by `index.markdown`. It reads the welcome message and picture from `_pagedata > homePageData.md`. It also reads data from `_posts` (as news) and `_projects` (for research highlights). 
 - `news` is called by `news.markdown`. It reads data from `_posts`. 
 - `people` is called by `people.markdown`. It reads data from `_pagedata > peoplePageData.md` and `_members`. The liquid code inside the page is grouping the members and checking the existence of properties for clean rendering. 
 - `projects` is called by `projects.markdown`. It reads data from `_pagedata > projectsPageData.md` and `_projects`. 
 - `publications` is called by `publications.markdown` and reads the `bib` files of the `_bibliography` and `_pagedata > publicationPageData.md` 


The following layouts are called by **data files**.   
   
 - `member` is a profile page for each member of the lab. It is called by each member in `_members` and reads data from `_pagedata > memberPageData.md`.   
 - `post` is page dedicated to each piece of news and called by each post in `_posts`. Currently, there is no accessible link in the website.  
 - `project` is a project page called by each project in `_projects`.  
 - `tool` is a page for available tools and reads data from `_tools`.
 

### Notes ! 

The url of the pages are defined in `_config.yml` as `/:collection/:name` where `:name` is the filename (Read more [here](https://jekyllrb.com/docs/permalinks/#collections)). That is, for `_members > Abc.md`, the url of Abc profile is `/members/abc`. (Note the lowercase `abc`). 

If the page is retrieved by processing the `site` variable, then its url is `{{ site.baseurl }} {{ varName.url }}`. For example:

```

{% for proj in site.projects %}  
  <a href="{{ site.baseurl }}{{ proj.url }}">More...</a>  
{% endfor %}
```

## _includes   

This directory contains the `html` pieces of code that are reused and called using `{% include ....html %}`. Some include files require additional inputs.  
  
 - `custom-head` (created by David and not being used in the current version of code)  
- `footer` is intended to implement a footer and to be included in the `default` layout. (not used at the moment`  
- `head` contains the head of the `HTML` page. It also includes the scripts for *bootstap* library.  
- `header` is the navigation bar and is included in the `default` layout. It reads the navigatin items from `_pagedata > navbarItems.md`
- `newsPanel` is the panel for news items in `home` and `news` pages. It should be called as `{% include newsPanel.html post=X messageThreshold=Y %}`
- `peoplePanel` is the panel reused in `people` page. It should be called as `{% include peoplePanel.html person=X %}`
- `projectPanel` is the panel reused in `home` and `projects` pages. It should be called as `{% include projectPanel.html project=X highlightTruncateLimit=Y learnMore=Z %}`


# Data Directories  
 
The only files that are going to be modified regularly are data files.   

## _bibliography 

This directory includes `references.bib` which is a `bib` file. 
The `project` property of bibitems is used to filter publications in `project` pages.
The first and last names of `author`s are matched against the first and last names of members to filter publications for `member` pages.
In the current design, all bibitems are called in the `publications.html` layout.  

## _members   

This directory contains the `md` files for each member. Each member file should have the following format:  
  
```
  
--- 
layout: member    
key: 
first_name:   
last_name: 
level: 
status:     
title:       
start_year: 
end_year:     
email:    
image: /assets/img/team/  
website:   
twitter:     
github:   
bib_id: 
--- 
The is the **bio** of the student written in markdown.
  
```  

Required fields are marked by (Req).
  
- (Req) The layout should be `member`. 
- (Req) `first_name` and `last_name` are displayed in the website.
- (Req) `key` should be unique. It is used in project files and used in `project.html` layout to identify project members.  
- (Req) `level` must be one of the values used in `people.html` page. Right now there are the following roles: `Faculty`, `PhD`, `Master`, `REU`, and `ASSIP`.
- (Req for non-Faculty members) `status` is either `student` or `alumni`. It is used to sort members in `people` page.
- (Req) `title` is used to display the title of the member. It is used in `people` and `member` pages.
- (Req for non-Faculty members) `start_year` is the year the student joined the lab. It is used to sort the members in `people` page.
- `end_year` is the year the member left the lab. If it is equal to `start_year`, it **should not** be added.
- `email` is not displayed in the website currently.
- (Req) `image` property are for locating the images of members. All images **should** be at `/assets/img/team/`.
All characters are case-sensitive, e.g., `jpg` is different from `JPG`.
All images **should** be squared (e.g., 450*450). Images should have small size for better rendering.
If there is no image, then the placeholder image should be added: `/assets/img/team/placeHolder.png`.  
- `website`, `twitter`, and `github` specify complete links to these external sites.
- `bib_id` is the name under which the papers are published. This property is not used currently.
- The bio is written in `md` format. It is displayed in `member` pages. 
  


## _pagedata   

The directory contains the data files used in differnt pages. These filed are not directly rendered, and they don't need the `layout` property. To be consistent, they should specified in which page they are being used through `for` property.

### galleryPageData

To add a new image, add the reasonably resized image to `/assets/img/gallery`, and add the location of the image plus a caption to the **same** index of the `images` and `captions` arrays.   

## _posts   

The news are stored individually in `_posts`. The naming convension for the news files is `yyyy-mm-dd-<some informative name>.md`. The format of each news file is:  
  
``` 
 
--- 
layout: post    
title:  Title of the news    
date:   yyyy-mm-dd hh:mm:ss -0400    
categories: jekyll update    
--- 

The description of the news in the markdown format.  

```  

The `categories` property is not used in the current implementation.  
In the current design, only the `yyyy-mm-ss` info of the date is being used.  

## _projects    

This directory stores the data of projects, current and old ones. The format of the data files is as follows:  
  
```

--- 
layout: project
key:     
title:
highlightMediaType:
highlightMediaURL:
highlight:   
currentMembers: [memberKey1,memberKey2] 
previousMembers: [memberKey3,memberKey4] 
active: true    
--- 
```   

- `layout` must be `project`  
- `key` is a unique value used in selecting highlights in `home` page.
- `highlightMediaType` is either `image` or `YouTube`. This is used in highlights in `home`, all `projects`, and individual `project` pages.
- `highlighMediaURL` depending on the `highlightMediaType` is either the YouTube URL (for `YouTube`) of the location of an image in `/assets/img/research/` directory.
- `highlight` is a summary of the project. It is displayed on `home`, all `projects`, and individual `project` pages.
- `currentMembers` is an array of members' `key`s who are currently active in the project.  
- `previousMembers` is an array of members' `key`s who previously contributed.  
- `active` is a boolean that specifies if the project is currently active or not. It is used to sort projects in all `projects` page.

# assets
  
Assets include `css` files (imported in `_includes > head.html`), `icons` and `img`. New `css` files should be added in `assets > css` and called in `head.html`.   

## img
  
It includes `gallery` pictures (e.g., group pictures), `research` pictures (for projects), and `team` pictures (for members of the lab).