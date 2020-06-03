# Unleash the power of Jekyll to generate GH-pages
Currently live at `https://<github_username>.github.io/devx.cs.gmu.edu/`.  You can inspect the current deployment at the [Environment tab](../../deployments/).

To overcome GH-pages limitations on the packages that can be used with [Jekyll](https://pages.github.com/versions/), this project uses its own Jekyll without limiting the packages you can use in your website. Now you can use gems such as `jekyll-scholar` or `jekyll-youtube`.

## How to use this repo
The are two folders in this repo:
- [`docs_src`](docs_src) (for humans): the source content used to generate the site. Editing this folder will redeploy the website, it may take some minutes to be reflected, please be patient (after a week GitHub removes Jekyll's build caches). The project will automatically generate the website each time changes are pushed to the the `docs_src` folder in the master `branch`. You can inspect the current build process at the [Actions tab](../../actions/). Visit the `docs_scr` [folder](docs_src) for more details on how to customize the website styles, layouts and content.

- `docs` (for machines): the automatically generated site, this is used by GH-pages to publish the site. **Do not edit this folder**.
 
There is a [GitHub action](.github/workflows/deploy_docs.yml) in charge of automatically listening to pushes to `master/docs_src` and rebuilds the page present in `docs`. GitHub will redeploy the website after `docs` changes like a normal static page.

### Enable GH-pages master/docs deployment
Configure the GH pages settings of your repo:
```
Setting => GitHub Pages => Source => master branch /docs folder
```
Now, pushes to the `docs_scr` folder will publish the site.

# Contributing
Open a [pull request](../../pulls), after it is approved a reviewer will merge it with the `master` branch.

## Keep your fork in sync with the main repo before creating a pull request
 1. Check if you have and upstream repo already:
 ```ShellSession
  git remote -v
 ```
 It should look like this:
```ShellSession
origin  https://github.com/<your_github_username>/devx.cs.gmu.edu.git (fetch)
origin  https://github.com/<your_github_username>/devx.cs.gmu.edu.git (push)
upstream        https://github.com/devuxd/devx.cs.gmu.edu.git (fetch)
upstream        https://github.com/devuxd/devx.cs.gmu.edu.git (push)
```
 1.a. Otherwise, run this command:
```ShellSession
 git remote add upstream https://github.com/devuxd/devx.cs.gmu.edu.git
```
 And try step 1 again.
 
 2. Get the data from the main repo:
 ```ShellSession
 git fetch upstream
```
 3. Choose the branch (`master` in this case) in your repo you want to sync with the main master branch:
 ```ShellSession
 git checkout master
 ```
 4. Finally, to sync with the main master branch, merge its changes with your branch:
 ```ShellSession
 git merge upstream/master
```


 More details [here](https://help.github.com/en/github/collaborating-with-issues-and-pull-requests/syncing-a-fork).

# Working locally
Try changes in your machine before pushing changes to "production".

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

## Deploy changes to your website
Modify the files in `docs_src` to generate the webpage in `docs`,
 at a terminal, assuming you are located in `docs_src`:
```ShellSession
git add .
git c -m "new website release"
git push
```
# Editing the content
Look for `.markdown` or `.md` files in the `docs_src` folder and follow these guidelines:

## Using GitHub Pages

You can use the [editor on GitHub](https://help.github.com/en/github/managing-files-in-a-repository/editing-files-in-your-repository) to maintain and preview the content for your website in Markdown files.

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

Your Pages site will use the layout and styles from the Jekyll theme you have selected in your [repository settings](../../settings). The name of this theme is saved in the Jekyll `_config.yml` configuration file.

### Support or Contact

Having trouble with Pages? Check out our [documentation](https://help.github.com/categories/github-pages-basics/) or [contact support](https://github.com/contact) and we’ll help you sort it out.
