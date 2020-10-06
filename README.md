Laptop
======
[![Build Status](https://travis-ci.org/monfresh/laptop.svg)](https://travis-ci.org/monfresh/laptop)

Laptop is a script to set up a macOS computer for web development, and to keep
it up to date.

It can be run multiple times on the same machine safely. It installs,
upgrades, or skips packages based on what is already installed on the machine.

This particular version of the script is geared toward beginners who want to
set up a Ruby environment on their Mac to be able to install gems such as Rails
or Jekyll. More advanced users can easily [customize](#customize-in-laptoplocal-and-brewfilelocal)
the script to install additional tools.

Requirements
------------

Supported operating systems:

* macOS Catalina (10.15)
* macOS Mojave (10.14)
* macOS High Sierra (10.13)
* macOS Sierra (10.12)
* OS X El Capitan (10.11)
* OS X Yosemite (10.10)
* OS X Mavericks (10.9)

Supported shells:

* bash
* fish
* zsh


Install
-------

Begin by opening the Terminal application on your Mac. The easiest way to open
an application in macOS is to search for it via [Spotlight]. The default
keyboard shortcut for invoking Spotlight is `command-Space`. Once Spotlight
is up, just start typing the first few letters of the app you are looking for,
and once it appears, press `return` to launch it.

In your Terminal window, copy and paste the command below, then press `return`.

```sh
bash <(curl -s https://raw.githubusercontent.com/monfresh/laptop/master/laptop)
```

The [script](https://github.com/monfresh/laptop/blob/master/mac) itself is
available in this repo for you to review if you want to see what it does
and how it works.

Note that the script might ask you to enter your macOS password at various
points. This is the same password that you use to log in to your Mac. If you
have `rbenv` or `RVM` installed, the script will ask you to uninstall them first
and run the script again. Look at the script output for uninstallation
instructions.

**Once the script is done, quit and relaunch Terminal.**

More [detailed instructions with a video][video] are available in the Wiki.

It is highly recommended to run the script regularly to keep your computer up
to date. Once the script has been installed, you'll be able to run it at your
convenience by typing `laptop` and pressing `return` in your Terminal.

[Spotlight]: https://support.apple.com/en-us/HT204014
[video]: https://github.com/monfresh/laptop/wiki/Detailed-installation-instructions-with-video

Why chruby and not RVM or rbenv?
--------------------------------

It is the smallest, most reliable, and easiest to understand. I like that it does not do some of the things that other tools do:

* Does not hook `cd`.
* Does not install executable shims.
* Does not require Rubies to be installed into your home directory.
* Does not automatically switch Rubies by default.
* Does not require write-access to the Ruby directory in order to install gems.

Other folks who prefer `chruby`:

* <https://kgrz.io/programmers-guide-to-choosing-ruby-version-manager.html>
* <https://stevemarshall.com/journal/why-i-use-chruby/>
* <https://linhmtran168.github.io/blog/2014/02/27/moving-from-rbenv-to-chruby/>

Debugging
---------

Your last Laptop run will be saved to a file called `laptop.log` in your home
folder. Read through it to see if you can debug the issue yourself. If not,
copy the entire contents of `laptop.log` into a
[new GitHub Issue](https://github.com/monfresh/laptop/issues/new) (or attach the whole log file to the issue) for me and I'll be glad to help you. If the script doesn't work for you, it's most likely a bug in my script, which I'd love to fix, so please don't hesitate to report any issues.

What it sets up
---------------

* [Bundler] for managing Ruby gems
* [chruby] for managing [Ruby] versions (recommended over RVM and rbenv)
* [GitHub CLI] brings GitHub to your terminal.
* [Heroku Toolbelt] for deploying and managing Heroku apps
* [Homebrew] for managing operating system libraries
* [Homebrew Cask] for quickly installing Mac apps from the command line
* [Homebrew Services] so you can easily stop, start, and restart services
* [Postgres] for storing relational data
* [ruby-install] for installing different versions of Ruby
* [Zsh] as your shell (if you opt in)

[Bundler]: http://bundler.io/
[chruby]: https://github.com/postmodern/chruby
[GitHub CLI]: https://cli.github.com
[Heroku Toolbelt]: https://toolbelt.heroku.com/
[Homebrew]: http://brew.sh/
[Homebrew Cask]: http://caskroom.io/
[Homebrew Services]: https://github.com/Homebrew/homebrew-services
[Postgres]: http://www.postgresql.org/
[Ruby]: https://www.ruby-lang.org/en/
[ruby-install]: https://github.com/postmodern/ruby-install
[Zsh]: http://www.zsh.org/

It should take less than 15 minutes to install (depends on your machine and
internet connection).

Customize in `~/.laptop.local` and `~/Brewfile.local`
-----------------------------------------------------
```sh
# Go to your macOS user's root directory
cd ~

# Download the sample files to your computer
curl --remote-name https://raw.githubusercontent.com/monfresh/laptop/master/.laptop.local
curl --remote-name https://raw.githubusercontent.com/monfresh/laptop/master/Brewfile.local

# open the files in your text editor
open .laptop.local
open Brewfile.local
```

Your `~/.laptop.local` is run at the end of the `mac` script.
Put your customizations there. If you want to install additional
tools or Mac apps with Homebrew, add them to your `~/Brewfile.local`.
You can use the `.laptop.local` and `Brewfile.local` you downloaded
above to get started. It lets you install the following tools and Mac apps:

* [Firefox] for testing your Rails app on a browser other than Chrome or Safari
* [Flux] for adjusting your Mac's display color so you can sleep better
* [GitHub Desktop] for working with your repos using a GUI
* [iTerm2] - an awesome replacement for the macOS Terminal
* [Nova] - Panic's new macOS native code editor
* [Redis] for storing key-value data
* [Sublime Text 3] - a solid and fast code editor
* [Visual Studio Code] - Microsoft's popular code editor

[Firefox]: https://www.mozilla.org/en-US/firefox/new/
[Flux]: https://justgetflux.com/
[GitHub Desktop]: https://desktop.github.com/
[iTerm2]: https://iterm2.com/
[Nova]: https://nova.app/
[Redis]: https://redis.io/
[Sublime Text 3]: https://www.sublimetext.com/3
[Visual Studio Code]: https://code.visualstudio.com/

Write your customizations such that they can be run safely more than once.
See the `mac` script for examples.

Laptop functions such as `fancy_echo`, and `gem_install_or_update` can be used
in your `~/.laptop.local`.

How to manage background services (such as Postgres)
----------------------------------------------------------
The script does not automatically launch these services after installation
because you might not need or want them to be running. With Homebrew Services,
starting, stopping, or restarting these services is as easy as:

```
brew services start|stop|restart [name of service]
```

For example:

```
brew services start postgresql
```

To see a list of all installed services:

```
brew services list
```

To start all services at once:

```
brew services start --all
```

Credits
-------

This laptop script is inspired by
[thoughbot's laptop](https://github.com/thoughtbot/laptop) script.

### Public domain

thoughtbot's original work remains covered under an [MIT License](https://github.com/thoughtbot/laptop/blob/c997c4fb5a986b22d6c53214d8f219600a4561ee/LICENSE).

My work on this project is in the worldwide [public domain](LICENSE.md), as are contributions to my project. As stated in [CONTRIBUTING](CONTRIBUTING.md):

> This project is in the public domain within the United States, and copyright and related rights in the work worldwide are waived through the [CC0 1.0 Universal public domain dedication](https://creativecommons.org/publicdomain/zero/1.0/).
>
> All contributions to this project will be released under the CC0 dedication. By submitting a pull request, you are agreeing to comply with this waiver of copyright interest.
