# Gerry's Personal Home Page

Jekyll site for Gerry's personal home page.

[Good Clean Read theme by adueck](https://adueck.github.io/good-clean-read).

[Live Site](https://gshaw.ca)

### Build Instructions

```
brew install asdf
asdf list
asdf plugin add ruby
asdf plugin-update ruby
asdf list all ruby
asdf install ruby latest
asdf global ruby 3.2.2 # change specfic version to latest stable
gem install bundler
bundle add webrick # https://github.com/jekyll/jekyll/issues/8523

brew install just
just -l
just install
just start
```

Pushing to GitHub will publish the site.
