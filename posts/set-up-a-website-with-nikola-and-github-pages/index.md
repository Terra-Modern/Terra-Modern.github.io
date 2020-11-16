<!--
.. title: Set up a website with Nikola and GitHub Pages
.. slug: set-up-a-website-with-nikola-and-github-pages
.. date: 2020-11-06 15:33:16 UTC-05:00
.. tags: Nikola, GitHub
.. category: Blog
.. link: 
.. description: 
.. type: text
.. author: Philip Griffith
-->

This post will walk you through the steps required to set up a website built with Nikola and hosted on GitHub Pages. Like any project, it begins with yak shaving.

<!-- TEASER_END -->

# Yak Shaving! {{% emoji water_buffalo %}} &#129682

*<abbr title="Nota bene: 'Note well'">N.B.</abbr> This post assumes some very basic knowledge of the command line. If you need help, you can always [learn it the hard way](https://learnpythonthehardway.org/python3/appendixa.html){:target="_blank"}. Regardless, you'll want to do everything within the Anaconda prompt once you have it installed.*

### Step 1. Install Python 3.x

Terra Modern recommends installing Python 3.x using [the latest version of Miniconda that's compatible with your computer](https://docs.conda.io/en/latest/miniconda.html){:target="_blank"}. Miniconda is a free, minimal installation of [Anaconda](https://www.anaconda.com/){:target="_blank"} that gives you access to the *de facto* Python installation environment for data science and spatial analysis, without also needing to download the kitchen sink.

### Step 2. Install Nikola

Broadly speaking, there are two major static site generators (SSGs) built with Python: [Pelican](https://docs.getpelican.com/en/latest/index.html){:target="_blank"} and [Nikola](https://getnikola.com/){:target="_blank"}. Terra Modern is built with Nikola, for the simple reason that Nikola supports blog posts written using the [Jupyter Notebook](https://jupyter.org/){:target="_blank"} format, a common way to document and share Python code. Though not all of our posts will be written using Jupyter Notebooks, it's definitely nice to have the ability to work with such a useful application as we plan the future of this site.

Because it's not available within the conda install environment, you'll need to install Nikola and all of its goodies using `pip` (though you can still do this within your Anaconda prompt):

`pip install Nikola[extras]`

### Step 3. Install Jupyter Notebooks 

To have the ability to read and write Jupyter Notebooks, you'll need to download the`notebook` package from conda. However, at least at the time of this post, Nikola has trouble rendering versions of Jupyter Notebook templates using the latest `nbconvert` library. To solve this problem, we can "pin" the version of `nbconvert` to the latest version that's compatible with Nikola:

`conda install -c conda-forge "notebook>=4.0.0" "nbconvert<6.0"`

### Step 4. Install git

Source control management (SCM) tools are an essential component of modern software development. By incorporating [git version control](https://git-scm.com/){:target="_blank"} into our spatial analysis workflows, Terra Modern is not only better able to work on projects as a team, but we can also leverage Nikola's deployment tools to seamlessly push website changes to our Github Pages.

To access this functionality, you'll want to [download the version of git that's compatible with your computer](https://git-scm.com/downloads){:target="_blank"}.

If you're unfamiliar with git or SCM, check out the [Git Handbook](https://guides.github.com/introduction/git-handbook/){:target="_blank"} by GitHub for a great introduction to the topic.

### Step 5. Create a GitHub account

Finally, you'll need to create a [GitHub account](https://github.com/){:target="_blank"} in order to host a website on GitHub Pages (it's only fair).

If you're unfamiliar with GitHub and how it works, check out their [Hello World tutorial](https://guides.github.com/activities/hello-world/){:target="_blank"} that covers the basics. If you're working with a team, you might also find the [GitHub workflow](https://guides.github.com/introduction/flow/){:target="_blank"} useful for keeping your projects in good shape.

Thankfully, Nikola will take care of all of the tricky deployment commands required to correctly store and sync your site with GitHub Pages. As long as you can push and pull changes between a local repository on your computer and its remote version on your GitHub account, you should be good to go!

# Create a Nikola site

*N.B. What follows is a pared-down version of the information available on the [Nikola website](https://getnikola.com/getting-started.html#init){:target="_blank"}, so head there if you'd like to learn more about the numerous possibilities available when using the library.*

Once you have all of the necessary programs installed, you can create a brand new Nikola site by opening your Anaconda prompt, navigating to the place on your computer where you want to create your site's directory, then entering the following command:

`nikola init --demo <type your site's directory name here>`

When you include the `--demo` argument, Nikola will ask you a series of questions to make sure that everything is configured correctly, as well as populate your new site with examples of many of the things it's able to do, which can be really helpful when you're just starting out. However, before you deploy your site, you'll want to [remove the unused bits that Nikola generates](https://getnikola.com/getting-started.html#rm-demo){:target="_blank"}. If you're already familiar with Nikola, or simply want to begin a site from scratch, use this command instead:

`nikola init --quiet <type your site's directory name here>`

After you initiate your site using one of the commands above, you'll need to tell Nikola to build your site for the first time with this command:

`nikola build`

This is [one of the things that separates SSGs](https://getnikola.com/handbook.html#why-static){:target="_blank"} from website generators like [WordPress](https://wordpress.com/){:target="_blank"} that create dynamic sites: every time you add a page or make a change to your website, you'll need to tell Nikola to build a new version of the entire site on your own computer before deploying it to a server. Don't worry, though, this isn't as bad as it sounds! Nikola will only rebuild those files that have been affected by your most recent changes, so while the first build may take some time, subsequent builds will usually only need to update a small section of the site.

Once the site is built, you can view it locally using this command:

`nikola serve --browser`

If you're anything like me, you'll need to make *lots* of changes before you're happy with your website and its content. Rather than having to manually build and serve the site every time you need to double-check the final product, Nikola will do this for you when you build the site using either of these commands:

`nikola auto --browser` or `nikola auto -b`

Now you can save a change to your site and it will automatically be reflected in your browser window. Just make sure you leave the Anaconda prompt running while you work.

# Create a post

"But wait!" I hear you say. "How do I add content to my website? And why are you so handsome?" To be clear, in what follows we're going to create a blog post, but if you understand the fundamentals, [building a standard webpage with Nikola isn't much different](https://getnikola.com/creating-a-site-not-a-blog-with-nikola.html){:target="_blank"}.

The process for creating a new post is as simple as:

`nikola new_post --format=markdown` or `nikola new_post -f markdown`

Nikola will ask you for the title of your post, then take care of configuring everything else. By default, Nikola will create a post in the [reStructuredText](https://docutils.sourceforge.io/rst.html){:target="_blank"} format, which is used by many Python libraries for documentation. Because I prefer writing in [Markdown](https://www.markdownguide.org/){:target="_blank"}, I need to specify that format when creating a post, otherwise I could leave out the `format` option. Built to be flexible, [Nikola supports Markdown, as well as many other formats](https://getnikola.com/handbook.html#supported-input-formats){:target="_blank"}, out-of-the-box.

To make things even easier, adding the argument `-e` to the `new_post` command will automatically open the new post in a text editor:

`nikola new_post -f markdown -e`

To get this functionality in Windows, you'll first need to set a new environment variable named `EDITOR` whose value is the full path to the executable file of your favorite text editor (Terra Modern recommends using [Notepad++](https://notepad-plus-plus.org/){:target="_blank"}!). You can set an environmental variable from the command line by running the Windows Command Prompt as an administrator, then entering this command:

`setx EDITOR "<type the full path to your text editor here>"`

# Deploy your site to GitHub Pages

Once you've created your website and filled it with amazing content, the only thing left to do is share it with the world. [To let others view your site through their browser, you'll need to store its files on a web server](https://developer.mozilla.org/en-US/docs/Learn/Common_questions/Pages_sites_servers_and_search_engines){:target="_blank"}. Enter [GitHub Pages](https://pages.github.com/){:target="_blank"}: by storing your website in a specific way within a git repo (what the cool kids call a "repository"), then uploading that repo to GitHub, GitHub Pages will act as your site's web server. For. Free. Like almost everything else, Nikola will do all of this for you automatically, though it *does* require a bit of setup first. What follows can also be found [in the Nikola handbook](https://getnikola.com/handbook.html#deployment){:target="_blank"}, so head there if you'd like the nitty-gritty details.

### Step 1. Create a local git repo

You'll first want to initialize a repo in your site's main directory using this command in your Anaconda prompt:

`git init .`

This will add a `.git` folder in your main directory that allows git to "see" and back up all the files and directories that make up your site.

### Step 2. Create a remote GitHub repo

Next, log in to your [GitHub account](https://github.com/){:target="_blank"} and create a new repository. To keep things simple, the name of the repo should match the name of your site's main directory. Make sure the repo is public!

### Step 3. Link your local repo to your remote repo

Once that's done, note the full <abbr title="Universal Resource Locator">URL</abbr> of your new remote GitHub repo (it will start with `https:` and end with `.git`) and return to your Anaconda prompt. You now need to tell your local repo about the remote one you just created. You can do that with the following command:

`git remote add origin <the full URL of your new remote GitHub repo>`

Your local repo now knows where to upload the files when Nikola tells it to do so.

### Step 4. Update your site's configuration file

Navigate to your site's main directory, where you'll see its configuration file, `conf.py`. This Python file contains the settings that Nikola uses when building your site; there are all sorts of options that you can fiddle with, but in this post we only need to change one. Open `conf.py` in your favorite text editor or <abbr title="Integrated Development Environment">IDE</abbr> and search for the `GITHUB_DEPLOY_BRANCH` variable.

If you're creating a user or organization site, you'll want to change this variable to `main`, [given GitHub's recent changes to how they name the default branch](https://github.com/github/renaming){:target="_blank"}.

If you're creating a project site, change this variable to `gh-pages`.

Nikola now knows how to store your fully built website within a repo so that GitHub Pages will recognize and host it on its web server.

### Step 5. Deploy your site to GitHub Pages!

Finally, deploy your site by uploading it to your GitHub account, using this command:

`nikola github_deploy`

This command builds your site, commits all the changes to your local git repo in their proper branches, then pushes everything to your remote repo on GitHub. Once GitHub has processed your changes, GitHub Pages will then begin hosting your site. The update process typically doesn't take long, though you will need to refresh your browser to see the changes.

If you created a user or organization site, your site will be hosted at `https://<your repo name>.github.io`.

If you created a project site, your site will be hosted at `https://<your GitHub user name>.github.io/<your repo name>/`.

# {{% emoji party_popper %}} Celebrate! {{% emoji confetti_ball %}}

Congratulations! You've successfully set up a website with Nikola and GitHub Pages!

Now that you have a website up and running, there's much that can be done. Stay tuned for a post on all the tweaks that we've made to build the Terra Modern organization site you see here.