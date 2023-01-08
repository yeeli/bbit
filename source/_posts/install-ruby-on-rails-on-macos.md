---
title: Install Ruby On Rails on macOS
categories:
- Rails
tags:
- Rails
---

##### Overview

We will be setting up a Ruby on Rails development environment on macOS.

Older versions of OS are mostly compatible so follow along as far as you can and then Google search for any problems you run into. There are plenty of people who have documented solutions for them.

## Using ZSH in your Terminal

MacOS Catalina has changed the default terminal from Bash to ZSH. As a result, we'll be adding configs to `~/.zshrc` instead of `~/.bash_profile` like we used in the past.

You can manually change from Bash to ZSH anytime by running the following command:

```bash
chsh -s /bin/zsh
```

## Installing Homebrew

First, we need to install [Homebrew](https://brew.sh/). Homebrew allows us to install and compile software packages easily from source.

Homebrew comes with a very simple install script. When it asks you to install XCode CommandLine Tools, say yes.

Open Terminal and run the following command:

```bash
/bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh)"
```

## Installing Ruby

Now that we have Homebrew installed, we can use it to install Ruby.

We're going to use [rvm](https://rvm.io/) to install and manage our Ruby versions.



Install GPG keys

```bash
gpg2 --recv-keys 409B6B1796C275462A1703113804BB82D39DC0E3 7D2BAF1CF37B13E2069D6956105BD0E739499BDB
```

Install RVM:

```
curl -sSL https://get.rvm.io | bash -s stable
```

To install Ruby and set the default version, we'll run the following commands:

```
rvm install 3.2.0
```

Confirm the default Ruby version matches the version you just installed.

```
ruby -v
```

Setting the new default ruby

```
rvm --default use 3.2.1
ruby -v
ruby 3.2.1p76 (2014-02-24 revision 45161) [x86_64-darwin12.0]
```

## Installing Rails

Installing Rails is as simple as running the following command in your Terminal:

```
gem install rails -v 7.0.4
```

And now we can verify Rails is installed:

```
rails -v
# Rails 7.0.4
```

## Setting Up A Database

We're going to install sqlite3 from homebrew because we can't use the built-in version with macOS Sierra without running into some troubles.

```bash
brew install sqlite3
```

Rails ships with sqlite3 as the default database. Chances are you won't want to use it because it's stored as a simple file on disk. You'll probably want something more robust like MySQL or PostgreSQL.

There is a lot of documentation on both, so you can just pick one that seems like you'll be more comfortable with.

If you're new to Ruby on Rails or databases in general, I strongly recommend [setting up PostgreSQL](https://gorails.com/setup/macos/13-ventura#postgresql).

If you're coming from PHP, you may already be familiar with MySQL.

### MySQL

You can install [MySQL](https://www.mysql.com/) server and client from Homebrew:

```bash
brew install mysql
```

Once this command is finished, it gives you a couple commands to run. Follow the instructions and run them:

```bash
# To have launchd start mysql at login:
brew services start mysql
```

By default the mysql user is `root` with no password.

When you're finished, you can [skip to the Final Steps](https://gorails.com/setup/macos/13-ventura#final-steps).

### PostgreSQL

You can install [PostgreSQL](https://www.postgresql.org/) server and client from Homebrew:

```bash
brew install postgresql
```

Once this command is finished, it gives you a couple commands to run. Follow the instructions and run them:

```bash
# To have launchd start postgresql at login:
brew services start postgresql
```

By default the postgresql user is your current macOS username with no password. For example, my macOS user is named `chris` so I can login to postgresql with that username.



And now for the moment of truth. Let's create your first Rails application:

```bash
rails new myapp

#### If you want to use MySQL
rails new myapp -d mysql

#### If you want to use Postgres
# Note you will need to change config/database.yml's username to be
# the same as your macOS user account. (for example, mine is 'chris')
rails new myapp -d postgresql

# Move into the application directory
cd myapp

# If you setup MySQL or Postgres with a username/password, modify the
# config/database.yml file to contain the username/password that you specified

# Create the database
rake db:create

rails server
```

You can now visit [http://localhost:3000](http://localhost:3000/) to view your new website!

Now that you've got your machine setup, it's time to start building some Rails applications.

If you received an error that said `Access denied for user 'root'@'localhost' (using password: NO)` then you need to update your config/database.yml file to match the database username and password.
