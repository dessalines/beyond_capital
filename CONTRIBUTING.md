# Contributing

## Technology

This site has a simple technology stack that should be accessible to anyone who has worked with HTML & CSS.

We use [Jekyll](https://jekyllrb.com/), a static website generator written in the [Ruby](https://www.ruby-lang.org/en/) language, to compile together the raw site assets. Jekyll allows us to:

* Not repeat ourselves while writing HTML. Multiple pages on a web site may share the same header, and Jekyll allows us to create a `header.html` that is inlined automatically on every page.
* Use fancy technology like [SCSS](http://sass-lang.com/), an extension of CSS that similarly allows us to write well-formed stylesheets without repeating ourselves.
* Have a unified build system, essential for working collaboratively.

If you're reading this through GitHub, you've probably realized that we use [Git](https://git-scm.com/) to manage our source code.

## Installing Git

If you are using OS X or Linux, your system may already have Git installed. Git is supported by all major systems (including Windows) and can be downloaded from the [official site](https://git-scm.com/).

### Windows

If you are on Windows, the Git installer will also install some dependencies that simulate a Unix environment that your OS X and Linux comrades already have. For instance, Git installs OpenSSH for generating SSH keys through `ssh-keygen`, which is utilized below.

Recommended options during the installation process:

* Select "Use Git from the Windows Command Prompt," which will allow you to use `git` and some of its related tools directly from the familiar command line. Some tools, such as `ssh-keygen`, will only be accessible through the "Git Bash" interface.
* Uncheck "Windows Explorer integration" to avoid cluttering your right-click menu in Explorer windows.
* Leave "Checkout as-is, commit Unix-style line endings" selected.
* Leave all other options as default.

## Configuring Git

Make sure you have a [GitLab](http://gitlab.cdap.cf) account too, so you can push public changes to our source code.

Replace the example name and email address in the following steps with the ones you used for your Github account. Enter each command one at a time, skipping any comment lines that being with `#`:

*If you are on Windows, many of the commands in this section likely must be executed through the "Git Bash" interface.*

```sh
git config --global color.ui true
git config --global user.name "YOUR NAME"
git config --global user.email "YOUR@EMAIL.com"
# Generate an SSH key, pressing [enter] for all options to use their defaults:
ssh-keygen -t rsa -C "YOUR@EMAIL.com"
```

The next step is to take the newly generated SSH key and add it to your Github account. You want to copy and paste the output of the following command and [paste it here](http://gitlab.cdap.cf/profile/keys).

```sh
cat ~/.ssh/id_rsa.pub
```

Once you've done this, you can check and see if it worked:

```sh
ssh -T git@gitlab.cdaf.cf
```

You should get something like:

```
Hi USERNAME! You've successfully authenticated, but GitHub does not provide shell access.
```

## Installing Ruby

While your system may already have a Ruby environment installed, it's likely an outdated package. At the time of writing, Ruby 2.3 is the latest package. You can check your version of Ruby by running `ruby -v` at the terminal or command prompt.

### Mac OS X

First, we need to install Homebrew. Homebrew allows us to install and compile software packages easily from source.

Homebrew comes with a very simple install script. When it asks you to install XCode CommandLine Tools, say yes.

Open Terminal and run the following command:

```sh
ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)"
```

We're going to use `rbenv` to install and manage our Ruby versions.

To do this, run the following commands in your Terminal:

```sh
brew install rbenv ruby-build

# Add rbenv to bash so that it loads every time you open a terminal.
#
# If you use an alternative shell, such as zsh, you'll want to add this line to its
# respective dotfile instead (e.g. `~/.zshrc` instead of `~/.bash_profile`).
echo 'if which rbenv > /dev/null; then eval "$(rbenv init -)"; fi' >> ~/.bash_profile
source ~/.bash_profile

# Install Ruby
rbenv install 2.3
rbenv global 2.3
ruby -v
```

### Linux

This section is particularly geared for Ubuntu, but these steps should be reproducible on any Linux distribution with some effort.

This uses [RVM](https://rvm.io/rvm/install) to install ruby and setup its dependencies.

First add the gpg keys for RVM. 
```sh
gpg --keyserver hkp://keys.gnupg.net --recv-keys 409B6B1796C275462A1703113804BB82D39DC0E3
```

Then install RVM with a stable ruby:
```sh
\curl -sSL https://get.rvm.io | bash -s stable --ruby
```

### Windows

Unfortunately, Ruby releases on Windows lag behind the other operating systems. Nevertheless, at the time of writing, you can install 2.2.4 through using [RubyInstaller](http://rubyinstaller.org/downloads/). Be sure to download the x64 version if you're on a 64-bit system (you most likely are).

Recommended options during the installation process:

* Check "Add Ruby executables to your PATH" to allow access to the Ruby programs through the command line.

## Installing Bundler

[Bundler](http://bundler.io/) is the standard package management system for Ruby. We use it to manage our Ruby dependencies such as Jekyll. Once Ruby is installed, installing Bundler is very simple:

```sh
gem install bundler
```

Depending on your system's configuration, you may have to include `sudo` before that command.

## Fork this repository

We follow the "pull requests" flow, which involves maintaining a personal "forked" repository and asking the maintainers of the main code repository to accept your changes one-by-one. Refer to the official ["Fork A Repo"](https://help.github.com/articles/fork-a-repo/) GitHub guide for more information on this flow.

Before proceeding, ensure that you've forked this repository to your own personal GitHub account by clicking the "Fork" button at this repository's root page.

## Download your forked repository

Finally, you're ready to download a local copy of the codebase.

```sh
git clone http://gitlab.cdaf.cf/YOUR-USERNAME/beyond-capital
cd beyond-capital
```

This should create and navigate to a folder named `beyond-capital` in whichever directory the command was executed.

## Installing the project's Ruby dependencies

The `beyond-capital` folder has a `Gemfile` file that lists all of the Ruby packages that this project depends on (e.g. Jekyll). Run the following command to install these packages on your machine.

```sh
bundle install
```

## Work on the code

You're read to start modifying project files!

```sh
jekyll serve
```

You'll see something like the following:

```
Configuration file: /Users/Me/Development/beyond-capital/_config.yml
            Source: /Users/Me/Development/beyond-capital
       Destination: /Users/Me/Development/beyond-capital/_site
 Incremental build: disabled. Enable with --incremental
      Generating...
                    done in 0.087 seconds.
 Auto-regeneration: enabled for '/Users/Me/Development/beyond-capital'
Configuration file: /Users/Me/Development/beyond-capital/_config.yml
    Server address: http://127.0.0.1:4000/beyond-capital/
  Server running... press ctrl-c to stop.
```

Navigate to `http://127.0.0.1:4000/beyond-capital/` in your web browser. Once you make changes to the source code, you can refresh your browser to see them live!

## Commit your changes

Git is an unfortunately complicated tool, but you can utilize the following work flow for the majority of your work.

```sh
# Register all new changes to the code
git add -A

# Bundle up the changes with a short commit message
git commit -m "Make header font larger"

# Push the commit to your forked repository on the "master" branch
git push origin master
```
