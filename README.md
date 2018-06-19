# Apps.GSA.Gov

This is the public repo for the apps.gsa.gov proof of concept demo. The goal is to create an active marketplace that helps GSA employees evaluate and compare approved software products. Information on product's description and approval status are listed. Additionally, resources for staff to request products and how to get started requesting a product can be found.

This repo is open source, maintained by the [Digital Service Team in the office of the CTO](https://tech.gsa.gov/). If you have any questions regarding this repo or the content listed, please contact [cto@gsa.gov](mailto:cto@gsa.gov).

## How to request a product

TBD


### How to run this locally

1. Install [Ruby](https://www.ruby-lang.org/) on your system. This site
   requires version 2.2.4 or greater. You can see if a compatible version is
   already installed by running `ruby -v` in a terminal window.

   You may wish to install a version manager such as
   [rbenv](https://github.com/rbenv/rbenv) to manage and install different
   Ruby versions.

1. Install [Node.js](https://nodejs.org/) on your system. This site requires
   version 4.2 or greater or version 5 or greater. You can see if a compatible
   version is already installed by running `node -v` in a terminal window.

   You may wish to install a version manager such as
   [nvm](https://github.com/creationix/nvm) to manage and install different
   Node.js versions.

   *Why Node.js?* It's used to build the [lunr.js search
   index](http://lunrjs.com/) and search user interface components supplied by
   the [`jekyll_pages_api_search` gem](https://rubygems.org/gems/jekyll_pages_api_search).
   We also use [browserify](https://www.npmjs.com/package/browserify)
   and [uglifyify](https://www.npmjs.com/package/uglifyify) to compile the
   custom [`assets/js/products.js`](assets/js/products.js]) code into
   `js/products-bundle.js`, as specified in the
   `jekyll_pages_api_search.browserify` property of
   [`_config.yml`](_config.yml).

1. Create a clone of this repository on your computer and change into its
   directory:
   ```sh
   $ git clone https://github.com/GSA/apps-gsa-gov.git
   $ cd apps-gsa-gov
   ```

1. Run `./go init` to install the [Ruby gems](https://rubygems.org/) specified
   in the [`Gemfile`](Gemfile) and the [npm modules](https://www.npmjs.com/)
   specified in [`package.json`](package.json).

   The `./go` script is [Bundler](http://bundler.io)-aware, so you do not need
   to run `bundle install` first.

   *Windows users:* You may need to run the script as `ruby ./go init`
   instead, and run other `./go` script commands in a similar fashion.

1. Run `./go build` to build the site, and `./go serve` to build and serve the
   site locally at http://127.0.0.1:4000.

   These commands run `jekyll build` and `jekyll serve`, respectively. You can
   pass command line arguments as you would to those bare commands.

   *Why not just run `bundle exec jekyll serve`?* `./go init` and `./go serve`
   perform the same environment setup as `bundle exec`, but the `./go` script
   also sets the `NODE_PATH` environment variable to add the `node_modules`
   directory, so that the locally-installed `browserify` and `uglifyify`
   modules are discoverable.

   This is because `jekyll_pages_api_search` contains components that
   `require()` these modules, but these components reside in a directory this
   is neither a child nor a parent of the site. Consequently, [the default
   Node.js module resolution
   algorithm](https://nodejs.org/api/modules.html#modules_all_together) will
   not discover the modules on its own.

