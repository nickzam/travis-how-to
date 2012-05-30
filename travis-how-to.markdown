Travis CI How To for Ruby projects
==================================

Travis is a continious integration tool that supports following languages (as on 30.05.2012):
  *  Clojure
  *  Erlang
  *  Groovy
  *  Haskell
  *  Java
  *  JavaScript (with Node.js)
  *  Perl
  *  PHP
  *  Python
  *  Ruby
  *  Scala

# Creating *.travis.yml*

Create *.travis.yml* in your root project dir.
Put there ruby versions that you want your project be tested with.

Example:
```
    language: ruby
    rvm:
      - 1.8.7
      - 1.9.3
      - jruby-18mode # JRuby in 1.8 mode
      - jruby-19mode # JRuby in 1.9 mode
      - rbx-18mode
      - rbx-19mode
```
Detailed docs: [travis-ruby][]

# Creating *Rakefile*

Create *Rakefile* in your root project dir.
Put there tasks you want to exec.

Example:
```
    task :test do
        require_relative 'MY_RUBY_SCRIPT.rb'
    end
```
To make it work for you change 'MY_RUBY_SCRIPT.rb' to your script.

Headless Rakefile example for use with cucumber or capybara:
```
    #!/usr/bin/env rake
    task :cucumber do
       # ask Travis to use xvfb headless driver for our task and run it
       system("export DISPLAY=:99.0 && bundle exec rake cucumber")
    end
```
More details on [travis-headless][]

# Creating Gemfile

Create Gemfile in your root project dir.
Here you will list gems that your app use.

Simpliest example, just gems needed for Travis:
```
    source "http://rubygems.org"
    group :test do
        gem 'bundler'
        gem 'rake'
    end
```
Example for testing with cucumber, capybara, capybara-webkit, htttparty
```
    source "http://rubygems.org"
    group :test do
        gem 'bundler'
        gem 'rake'

        gem 'cucumber'
        gem 'rspec'

        gem 'httparty'
        gem 'capybara'
        gem 'rack-test'
        gem 'capybara-webkit'
    end
```
# Linking github account with Travis

1. To start working with Travis obtain [github][] account. If you own one, login into it.
2. Go to [travis][] website, on the top right click "Login via Github".
3. Top right link will be changed to profile avatar. Hover your mouse there and choose "Profile".
4. You will see a list of your projects from your github account.
5. Click on button corresponding to your project, button should change to "On".
6. Click on wrench icon corresponding to your project.
7. You will see configuration for Travis with internal key filled in. 
8. Click Test, then Update

Great, you have connected your github account project with [travis][] !

# Other links:
1. [travis-start][]
2. [travis-docs][]

*Happy CI with Travis!*

Mykola Zamkovoi nickzam@gmail.com

[travis]: http://travis-ci.org/                     "Travis CI"
[travis-docs]: http://about.travis-ci.org/docs/     "Travis Docs"
[travis-start]: http://about.travis-ci.org/docs/user/getting-started/ "Travis Getting started"
[travis-ruby]: http://about.travis-ci.org/docs/user/languages/ruby/ "Travis Ruby"
[travis-headless]: http://about.travis-ci.org/docs/user/gui-and-headless-browsers/ "More on Travis headless testing"
[github]: http://github.com/                        "Github"