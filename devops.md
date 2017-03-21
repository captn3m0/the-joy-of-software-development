# System Orchestration

At the beginning was a single server. There was one tiny application
to be installed on the server, thankfully a single binary.
You copied it over to the home directory, and ran it inside a
screen session[screen]. A few days later, the server restarted, and
you did it again every time the server rebooted.

A few more times and you decided to create a cronjob[footnote] to start the process every time the server boots. Then came other responsibilities:

- Ensure that the database server starts _before your application_.
- Upgrade a package you were using because you found out it had a critical vulnerability.
- Write a script that takes a daily backup of the database server.
- Restore from the database backup when you accidentally deleted the production database (happens with everyone!)
- Fix the SSH config to secure your server better.

These are some of the things System Admins are expected to do. Over time
as the industry has matured, we have moved from ad-hoc scripts and manual
intervention to automating everything.

There are tools available to make the job of a Dev Ops engineer much more
easier than the counterpart from 10 years back. As usual, instead of focusing
on tools, we'll rather focus on tool categories:

## Package Managers
Unlike the language specific package managers (discussed in **TODO**), we also have package managers for your OS/distro combination. These would include `apt-get` (ubuntu), `apt` (debian), `pkg` (\*bsd), or `pacman` (Arch Linux). Get comfortable with the package manager and try figuring out how it works. `apt-get`, for eg is a nicer interface to `apt` (the debian package manager), and as a consequence uses the same package file structure (`.deb`). Both of these internally call `dpkg` to actually perform package operations (such as un/installations).

Other things you might wanna read about will be:

- How to do scheduled upgrades of your system.
- How to pin dependencies to a certain version, so that it doesn't upgrade accidentally.
- How to cache your package repositories, and see if that helps in making the upgrades faster.
- Create your own package and publish it.

## Shell Scripting

While I refer to this section as shell scripting, it is not necessary to stick to a shell-language (bash/zsh) to actually get this done; you can do these tasks equally well using a common scripting language - many people prefer Python/Perl over Shell.

You might wanna refresh the basics of using a shell from [Command Line chapter][cli.md].