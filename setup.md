# Installing Software

So far, we have only talked about basic shell scripting, and things that can be done on the command line. As we move ahead, we will need to write and discuss code in various programming languages. This chapter is a short primer on how to install various languages, and how to get started with them.

##Version Management
The software you write today might be compiled or distributed in some way. All of these things involve the concept of versioning. You might tag your releases and state the dependencies needed to reproduce it.

Over time, you'd want to upgrade your setup and move to a newer dependency or toolchain. But what if you wanna move to a newer version of the programming language?

Languages used to be slowly evolving, but now the pace of development in various ecosystem is very high. Take for instance Rust (a programming language by Mozilla):

|Version|Date|
|---|---|
|1.0 alpha|2015-01-09|
|0.12   |2014-10-09|
|0.11   |2014-07-02|
|0.10   |2014-04-03|
|0.9    |2014-01-09|

This is 5 releases in one year. In order to help people seamlessly shift between these versions, many languages have come up with the idea of Version Managers.

Arguably the most popular amongst these is `rvm`.

### rvm

`rvm` stands for Ruby Version Manager. It is a shell script to help you install the latest ruby versions, and switch between them easily.

### nvm

### gvm

### rsvm

### virtualenv

## System Package Managers

Apart from languages, you are always installing software, whether it be libraries, editors, or some tool that you are trying out. I use Ubuntu, which is a derivative of Debian, which uses the `apt-get` system. Others include: `brew` and  `macports` (for Macs), `yum` (Red Hat Linux), `nix`, `choco` (Windows).

The primary purpose of a system level package manager is to make sure that various system dependencies don't conflict with each other and stay compatible.

### apt-get

`apt-get` is a system level package manager for Debian based distros. Primary usage:

    sudo apt-get install g++
    sudo apt-get remove git

`apt-get` uses `.deb` file format for packages. The metadata about an installed package can be seen with the `dpkg` command, and you can use the same to install a downloaded `.deb` file.

### brew

brew is arguably the most popular package manager for OS X. (The other contender is `macports`). brew is written in Ruby and is a third-party tool (not supported by Apple) that can be used for installing lots of things on a Mac:

    sudo brew install git
    
### nix

Another package manager I want to mention is `nix`. `nix` has several advantages over other package managers:

- side-by-side installation of multiple versions of a package
- multi-user: two users can have different versions of the same package, without using root
- source/binary: nix has a source model, but can use binary caches as well
- portable: nix runs on mac, linux and some other platforms

##Dependency Managers

This section is specifically about dependency managers used by various languages. Even though software like `dpkg` handle dependency management, most languages come with their own toolkit for this specifically.

The usual ones are `npm` (node.js), `rubygems` (ruby), `composer` (PHP). The more arcane ones are `cargo` (rust).

Lets talk about my favorite among these: `npm`.

### npm

As a side-effect of functional scope in Javascript, `npm` has the distinct advantage of being able to simultaneously load different versions of the same package. `npm` is pretty new, and it also makes a crucial decision: use cheap hard disk space instead of increasing complexity.

The same decision could not have been made in, say 2000, because of the prohibitive cost of storage. However this counts as a smart decision today as it allows a javascript developer to easily install dependencies without having to worry about conflicts at all.

### composer
The original package manager for PHP was PEAR. However, this has more or less been superseded by Composer. Composer uses `package.json` files for storing the metadata and the dependency information.

##lein


