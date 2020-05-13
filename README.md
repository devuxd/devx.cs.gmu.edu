# Using Jekyll to generate DevX GH-pages
Currently live at [https://luminaxster.github.io/devx.cs.gmu.edu/](https://luminaxster.github.io/devx.cs.gmu.edu/).

## Installation
Installing GitHub pages locally, for  *MacOS*,
 at a terminal, assuming you are located in `docs_src`: 
```ShellSession
xcode-select --install
ruby —version
#Should be >2.5
gem install --user-install bundler jekyll
echo 'export PATH="$HOME/.gem/ruby/2.6.0/bin:$PATH"' >> ~/.bash_profile
#Relaunch console
gem env
sudo gem install bundler
bundle install
```
More details [here](https://jekyllrb.com/docs/installation/macos/).

## Run locally
At a terminal, assuming you are located in `docs_src`
```ShellSession
bundle exec jekyll serve
```

## Deploy changes to the website
Modify the files in `docs_src` to generate the webpage in `docs`,
 at a terminal, assuming you are located in `docs_src`:
```ShellSession
bundle exec jekyll clean
bundle exec jekyll build
rm -rf ../docs
mv _site/ ../docs
git status
git add -A
git c -m "new website release"
git push
```

## Welcome to GitHub Pages

You can use the [editor on GitHub](https://github.com/luminaxster/devx.cs.gmu.edu/edit/master/README.md) to maintain and preview the content for your website in Markdown files.

Whenever you commit to this repository, GitHub Pages will run [Jekyll](https://jekyllrb.com/) to rebuild the pages in your site, from the content in your Markdown files.

### Markdown

Markdown is a lightweight and easy-to-use syntax for styling your writing. It includes conventions for

```markdown
Syntax highlighted code block

# Header 1
## Header 2
### Header 3

- Bulleted
- List

1. Numbered
2. List

**Bold** and _Italic_ and `Code` text

[Link](url) and ![Image](src)
```

For more details see [GitHub Flavored Markdown](https://guides.github.com/features/mastering-markdown/).

### Jekyll Themes

Your Pages site will use the layout and styles from the Jekyll theme you have selected in your [repository settings](https://github.com/luminaxster/devx.cs.gmu.edu/settings). The name of this theme is saved in the Jekyll `_config.yml` configuration file.

### Support or Contact

Having trouble with Pages? Check out our [documentation](https://help.github.com/categories/github-pages-basics/) or [contact support](https://github.com/contact) and we’ll help you sort it out.
