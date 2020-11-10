<!--
.. title: Set up a Github Pages website with Nikola
.. slug: set-up-a-github-pages-website-with-nikola
.. date: 2020-11-06 15:33:16 UTC-05:00
.. tags: nikola, github
.. category: blog
.. link: 
.. description: 
.. type: text
.. author: Philip Griffith
-->

This post will walk you through the steps required to set up a website built with Nikola and hosted on Github Pages. Like any project, it begins with yak shaving.

<!-- TEASER_END -->

# Yak Shaving! {{% emoji water_buffalo %}} &#129682

*<abbr title="Nota bene">N.B.</abbr> This post assumes some very basic knowledge of the command line. If you need help, you can always [try it the hard way](https://learnpythonthehardway.org/python3/appendixa.html){:target="_blank"}. Regardless, you'll want to do everything within the Anaconda prompt once you have it installed.*

### Step 1. Install Python 3.x

Terra Modern recommends installing the latest version of Python 3.x using [Miniconda](https://docs.conda.io/en/latest/miniconda.html){:target="_blank"}, the free, minimal installation of [Anaconda](https://www.anaconda.com/){:target="_blank"}. This gives you access to the *de facto* Python installation environment for data science and spatial analysis, without needing to download the kitchen sink.

Download the 3.x version of Miniconda that's compatible with your computer [here](https://docs.conda.io/en/latest/miniconda.html){:target="_blank"}.

### Step 2. Install Nikola

Broadly speaking, there are two major static site generators (SSGs) built with Python: [Pelican](https://docs.getpelican.com/en/latest/index.html){:target="_blank"} and [Nikola](https://getnikola.com/){:target="_blank"}. Terra Modern is built with Nikola, for the simple reason that Nikola supports blog posts written using the [Jupyter Notebook](https://jupyter.org/){:target="_blank"} format, a common way to document and share Python code. Though not all of our posts will be written using Jupyter Notebooks, it's definitely nice to have the ability to work with such a useful application as we plan the future of this site.

Because it's not available within the conda install environment, you'll need to install Nikola and all of its goodies using `pip` (though you can still do this within your Anaconda prompt):

`pip install Nikola[extras]`

### Step 3. Install Jupyter Notebooks 

To have the ability to read and write Jupyter Notebooks, you'll need to download the`notebook` package from conda. However, at least at the time of this post, Nikola has trouble rendering versions of Jupyter Notebook templates using the latest `nbconvert` library. To solve this problem, we can "pin" the version of `nbconvert` to the latest version that's compatible with Nikola:

`conda install -c conda-forge "notebook>=4.0.0" "nbconvert<6.0"`

### Step 4. Install git

Source control management (SCM) tools are an essential component of modern software development. By incorporating [git version control](https://git-scm.com/){:target="_blank"} into our spatial analysis workflows, Terra Modern is not only better able to work on projects as a team, but we can also leverage Nikola's deployment tools to seamlessly push website changes to our Github Pages.

Download the version of git that's compatible with your computer [here](https://git-scm.com/downloads){:target="_blank"}.

If you're unfamiliar with git or SCM, check out the [Git Handbook](https://guides.github.com/introduction/git-handbook/){:target="_blank"} by GitHub for a great introduction to the topic.

### Step 5. Create a GitHub account

You'll need to create a [GitHub account](https://github.com/){:target="_blank"} in order to host a website on GitHub Pages (it's only fair).

If you're unfamiliar with GitHub and how it works, check out their [Hello World tutorial](https://guides.github.com/activities/hello-world/){:target="_blank"} that covers the basics. If you're working with a team, you might also find the [GitHub workflow](https://guides.github.com/introduction/flow/){:target="_blank"} useful for keeping your projects in good shape.

Thankfully, Nikola will take care of all of the tricky deployment commands required to sync your site with GitHub Pages. As long as you can push and pull changes between a local repository on your computer and its remote version on your GitHub account, you should be good to go!
