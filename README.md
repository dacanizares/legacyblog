
# My personal Blog

[![Build Status](https://travis-ci.org/dacanizares/dacanizares.github.io.svg?branch=master)](https://travis-ci.org/dacanizares/dacanizares.github.io) 

Based on Jekyll Now. Hosted on GitHub Pages at https://dacanizares.github.io/.

## How to run locally

### Pre-requisites

* Install Ruby: (https://www.ruby-lang.org/en/downloads/)

* Clone repository: [wikilaterus instructions](https://github.com/equilaterus/wikilaterus/wiki/Cloning-a-repo-on-Github).

### Windows:

On the folder *util* of the project you will find some bat files that contain required commands to start the site locally.

1. Run for the first time **win-install-bundler.bat**.

2. Run **win-install-site.bat** to download all dependencies.

3. Run **win-run-site.bat** to execute the site. Command line will show you the localhost url where the site was deployed.

### Any OS:

Execute the following commands from project's root.

1. For the first time:
    ```
    gem install bundler
    ```

2. Download all dependecies:
    ```
    bundle install
    ```

3. Run the server:
    ```
    bundle exec jekyll serve
    ```

## License

The content of this project itself is licensed under the Creative Commons Attribution 4.0 International ([CC BY 4.0](https://creativecommons.org/licenses/by/4.0/)) license, and the underlying source code used to format and display that content is licensed under the MIT license.
