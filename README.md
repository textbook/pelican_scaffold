Pelican Scaffold
================

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

1. Set up the source repository (again, probably `<yourname>.github.io-source`)
 on Travis; it's probably best to set it build only on pushes, so that pull
 requests don't cause any trouble.

1. Generate an authentication token for GitHub (`Settings > Personal access
  tokens > Generate new token`), which will allow the deployment script to push
  to the output repository, and add it to Travis as an environment variable
  named `GH_PAGES`.

1. Delete this `README` file, to avoid issues with Pelican processing `markdown`
 files, then push to your source repo.

Voila!

Acknowledgements
----------------

The build script is based heavily on [*"How to automatically build your Pelican
blog and publish it to Github Pages"*][zonca] by Andrea Zonca, with the
modifications suggested in [*"Deploying Pelican Sites Using Travis CI"*][yap] by
Kevin Yap.



 [ghp]: https://pages.github.com/
 [pelican]: http://docs.getpelican.com/
 [travis]: https://travis-ci.org/
 [yap]: http://kevinyap.ca/2014/06/deploying-pelican-sites-using-travis-ci/
 [zonca]: http://zonca.github.io/2013/09/automatically-build-pelican-and-publish-to-github-pages.html
