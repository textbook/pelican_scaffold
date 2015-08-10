Pelican Scaffold
================

A simple template for Pelican sites on GitHub Pages with Travis integration.

Introduction
------------

[Pelican] is a Python-powered static site generator that, when combined with
the hosting provided by [GitHub Pages][ghp] and automated build and CI from
[Travis], makes it incredibly easy to manage your own blog.

However, getting set up with a full workflow is still a little tricky. This
repo aims to simplify things; all you need is `git`, Python and `pip`
(installing in a `virtualenv` is generally recommended, but not required) and
you can be up and running in five minutes.

Installation
------------

1. Fork this repository, check it out and `cd` into the directory.

1. Run `pip install -r requirements.txt` to install Pelican and the other
  dependencies (if you add other dependencies, remember to use `pip freeze >
  requirements.txt` to keep the list up to date).

1. Run `pelican-quickstart` to create the basic Pelican files, including
  `pelicanconf.py` and `publishconf.py` - just hit <kbd>Enter</kbd> for most of
  the questions, but answer the following:

   - *What will be the title of this web site?*

   - *Who will be the author of this web site?*

   - *What is your URL prefix?* (use `http://<yourname>.github.io`)

  It may seem odd to answer `N` to *Do you want to upload your website using
  GitHub Pages?*, but we're dealing with that ourselves!

1. This repository includes `pelican-plugins` and `pelican-themes` as
  submodules, so you can `git submodule update --init --recursive` to download
  the appropriate content (this might take a while, so skip ahead to updating
  the deploy script and return once it's done).

1. To use that content, set `THEME = 'pelican-themes/<yourchoice>'` and
  `PLUGIN_PATHS = ['pelican-plugins']` in `pelicanconf.py`.

1. Update `deploy.sh` with your GitHub username as `GH_USERNAME` to ensure
  that the site gets published to the correct place (if you don't want to use
  `<yourname>.github.io`, you will need to edit more extensively).

1. Set up your forked repository on Travis; it's probably best to set it build
 only on pushes, so that pull requests don't cause any trouble. You can modify
 `.travis.yml` to match your version of Python, if required.

1. Generate an authentication token for GitHub (`Settings > Personal access
  tokens > Generate new token`), which will allow the deployment script to push
  to the output repository, and add it to Travis as an environment variable
  named `GH_PAGES`.

1. If you don't have it already, create a new GitHub repository named
 `<yourname>.github.io` for the site to be published to.

1. Commit and push this repository to kick off the build and publication of
  the first version of your new site.

Voila! You can now develop your site locally, or add new articles directly on
GitHub in the content folder, and the live version will be updated accordingly.
The site will be visible online at `http://<yourname>.github.io`.

Tips
----

 - A `CNAME` file is required if you want to use a custom domain with GitHub
   Pages. The easiest way to provide this is to add an `extra` directory to
   `content`, put the appropriate `CNAME` in that directory (see [GitHub's
   help][domain]) and add `STATIC_PATHS.append('extra')` and
   `EXTRA_PATH_METADATA['extra/CNAME'] = {'path': 'CNAME'}` to
   `pelicanconf.py`. You can then set `SITEURL = "<your.custom.domain>"` instead
   of `SITEURL = "http://<yourname.github.io>"`

 - Note that `pelicanconf.py` should contain settings used for both local
   development *and* publication, but `publishconf.py` will be used by the
   deploy script, so you can use that for things that make local development
   more complex (e.g. I only have the publication `SITEURL` defined in the
   publication config so that `localhost` still works OK).

Acknowledgements
----------------

The build script (`deploy.sh`) is based heavily on [*"How to automatically build 
your Pelican blog and publish it to Github Pages"*][zonca-article] by [Andrea 
Zonca][zonca], with the modifications suggested in [*"Deploying Pelican Sites 
Using Travis CI"*][yap-article] by [Kevin Yap][yap].

 [1]: 
 [2]: 
 [domain]: https://help.github.com/articles/adding-a-cname-file-to-your-repository/
 [ghp]: https://pages.github.com/
 [pelican]: http://docs.getpelican.com/
 [travis]: https://travis-ci.org/
 [yap]: https://github.com/iKevinY
 [yap-article]: http://kevinyap.ca/2014/06/deploying-pelican-sites-using-travis-ci/
 [zonca]: https://github.com/zonca
 [zonca-article]: http://zonca.github.io/2013/09/automatically-build-pelican-and-publish-to-github-pages.html
