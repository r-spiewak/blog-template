# Blog Template

See the GitHub Pages [here](https://r-spiewak.github.io/blog-template/).


## Using the Template

1. Create a repo using the template.
2. Clone that repo.
3. Set up that repo as a public repo, and set up [GitHub Pages](#github-pages-build-instructions).
4. Update:
    1. In [_config.yml](_config.yml):
        1. `title`
        2. `baseurl`
        3. `favicon_svg`
        4. `favicon_png`
        5. `favicon_ico`
    2. Update the three favicon files in [assets/images](assets/images/) (the names should match the attributes `favicon_svg`, `favicon_png`, and `favicon_ico` defined in [_config.yml](_config.yml), as modified above).
    3. Update blog pages in [_site_content](_site_content/) for your new blog!


## GitHub Pages Build Instructions

The following are the steps necessary to set up the GitHub Pages to host the site:
1. Make sure the repo is public or in a paid tier that includes Pages hosting.
2. On GitHub, go to Settings -> Pages. Under `Build and deployment`, under `Source`, select `GitHub Actions`.
3. The jekyll build and deploy workflows in [.github/workflows/jekyll.yml](.github/workflows/jekyll.yml) will then build the site and deploy it to Pages.


## Local Build Instructions

The following steps are necessary to build the site locally.


### Requirements

This site is built with [Jekyll](https://jekyllrb.com/docs/installation/ubuntu/), a Ruby gem. It requires:
- [Ruby](https://www.ruby-lang.org/en/downloads/) version 2.7.0, including all development headers (check your Ruby version using `ruby -v`)
- [RubyGems](https://rubygems.org/pages/download) (check your Gems version using `gem -v`)
- [GCC](https://gcc.gnu.org/install/) and [Make](https://www.gnu.org/software/make/) (check versions using `gcc -v`,`g++ -v`, and `make -v`)

Steps:
1. Install Jekyll prerequisites:
```
sudo apt-get install ruby-full build-essential zlib1g-dev
```
2. Set up a gem installation directory for your user account:
```
echo '# Install Ruby Gems to ~/gems' >> ~/.bashrc
echo 'export GEM_HOME="$HOME/gems"' >> ~/.bashrc
echo 'export PATH="$HOME/gems/bin:$PATH"' >> ~/.bashrc
source ~/.bashrc
```
3. install Jekyll and Bundler:
```
gem install jekyll bundler
```


### Build

Run the following from the root of the repo:
```
bundle install
bundle exec jekyll build --trace
```


### Serve

To serve the site locally (and automatically rebuild on any changes), run the following:
```
bundle exec jekyll serve --livereload --host localhost --port 4444 --livereload-port 35730
```


### Troubleshooting

1. If build errors persist even if there is nothing referring to those variables (and/or the file no longer has that many lines for which the build error produces the failing line reference), run `bundle exec jekyll clean` and rebuild. Also try manually removing the `.jekyll_cache` directory.
2. If a complaint is given about `port is in use or requires root privileges`, check if the port is in use with `sudo ss -tulpn | grep 4444`. If the port is not in use, try removing the `--livereload` flag, as it sometimes seems to override the `--port` flag (actually, the livereload exposes a second port, and that is changed with the `--livereload-port` flag).
