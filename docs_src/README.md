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
  
 - `gallery` is called by `gallery.markdown`. It reads data from `_pagedata > galleryImages.md` 
 - `home` is called by `index.markdown`. It reads the welcome message and picture from `_pagedata > homeMessage.md`. It also reads data from `_posts` (as news) and `_projects` (for research highlights). 
 - `news` is called by `news.markdown`. It reads data from `_posts`. 
 - `people` is called by `people.markdown`. It reads data from `_members`. The liquid code inside the page is grouping the members and checking the existence of properties for clean rendering. 
 - `projects` is called by `projects.markdown`. It reads data from `_projects`. 
 - `publications` is called by `publications.markdown` and reads the `bib` files of the `_bibliography`  


The following layouts are called by **data files**.   
   
 - `member` is a profile page for each member of the lab. It is called by each member in `_members`.   
 - `post` is page dedicated to each piece of news and called by each post in `_posts`.  
 - `project` is a project page called by each project in `_projects`.  
 

## Notes ! 

The url of the pages are defined in `_config.yml` as `/:collection/:name` where `:name` is the filename (Read more [here](https://jekyllrb.com/docs/permalinks/#collections)). That is, for `_members > Abc.md`, the url of Abc profile is `/members/abc`. (Note the lowercase `abc`). 

If the page is retrieved by processing the `site` variable, then its url is `{{ site.baseurl }} {{ varName.url }}`. For example:

```

{% for proj in site.projects %}  
  <a href="{{ site.baseurl }}{{ proj.url }}">More...</a>  
{% endfor %}
```

However, to manually creating the url, note that url must be lowercase. For example:

```

{% for collab in page.current_collaborators %}  
    <a href="{{site.baseurl}}/members/{{collab | downcase}}">{{collab}}</a><br>  
{% endfor %}
```

## _includes   

This directory contains the `html` pieces of code that are reused and called using `{% include ....html %}`.    
 - `custom-head` (created by David and not being used in the current version of code)  
- `footer` is intended to implement a footer and to be included in the `default` layout. (not used at the moment`  
- `head` contains the head of the `HTML` page. It also includes the scripts for *bootstap* library.  
- `header` is the navigation bar and is included in the `default` layout. It reads the navigatin items from `_pagedata > navbarItems.md`  


# Data Directories  
 
The only files that are going to be modified regularly are data files.   

## _bibliography 

This directory includes `references.bib` which is a `bib` file. The `key` of bibitems are explicily reused in `_members` and `_projects` files. In the current design, all bibitems are called in the `publications.html` layout.  

## _members   

This directory contains the `md` files for each member. Each member file should have the following format:  
  
```
  
--- 
layout: member    
key: student_key    
role: phd_student    
title: PhD Student    
first_name: First Name    
last_name: Last Name    
start_year: 2017    
email: <email>@gmu.edu    
image: /assets/img/team/<studentName>.jpg    
website: http://mason.gmu.edu/~<masonlive username>    
twitter: https://twitter.com/<twitterID>    
github: https://github.com/<GithubID>    
publications: [bibItemKey1,bibItemKey2] 
--- 
The is the **bio** of the student written in markdown.
  
```  
  
- The layout should be `member`. 
- `key` should be unique. It is used in project files and used in `project.html` layout to look for collaborators.  
- `role` must be one of the values used in `people.html` page. Right now there are the following roles: `lab_director`, `phd_student`, `master_student`, `undergrad_student`, `highschool_student`, and `REU`. Currently, the `role` property is only used in `people.html` layout.  
- `start_year` is used to sort the students in the `people.html` layout.  
- `publications` is an array of bibitem keys in `references.bib`.  
- The bio is written in `md` format.  
  
Properties can be removed/commented out by adding `#`. `email`, `image`, links, `publications`, and `bio` can be commented out.  

## _pagedata   

The directory contains the data files used in differnt pages. As these filed are not directly rendered, they don't need the `layout` property. To be consistent, they should specified in which page they are being used through `for` property.  

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

This directory stores the data of projects, current and old ones. The format of the data files is as folloes:  
  
```
  
--- 
layout: project    
title: Project title    
video: youtube link  
photo: local path to the link  
short_desc: Some short description.     
current_collaborators: [memberKey1,memberKey2] prev_collaborator: [memberKey3,memberKey4] active: true    
publications: [bibItemKey1,bibItemKey2] --- Long description for the project in markdown.  
```   

- `layout` must be `project`  
- `video` should be a youtube link (optional), used in `home.html`, `projects.html`, `project.html`, and `member.html`.  
- `photo` should be in the local. More photos can be added in the long description.  
- `short_desc` is used in `home.html` in research highlights, `projects.html` in summary of the project, in `project.html`, and in `member.html`.  
- `current_collaborators` is an array of member `key`s.  
- `prev_collaborators` is an array of member `key`s previously contributed.  
- `active` is a boolean that specifies if the project is currently active or not.  
- `publications` is an array of bibitem keys.   

# assets
  
Assets include `css` files (imported in `_includes > head.html`), `icons` and `img`. New `css` files should be added in `assets > css` and called in `head.html`.   

## img
  
It includes `gallery` pictures (e.g., group pictures), `research` pictures (for projects), and `team` pictures (for members of the lab).