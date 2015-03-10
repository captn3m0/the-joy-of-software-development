#The Command Line

This chapter is a short primer on getting started with the command line. It is expected that you are running a POSIX-compatible system, with a standard shell such as bash or zsh. If you are unsure what any of the terms mean, just consult the [GLOSSARY](GLOSSARY.md).

##Command Line Basics

If you are used to working using the Explorer, this might be something new for you. The command line is not quite as complex as you might thing it to be. It is however, all of the following:

- A faster way to get things done (usually)
- A much better way to issue commands
- A much more powerful tool than using the mouse

A shell is a much more powerful version of a REPL. You issue commands and the shell responds back with the result of the command. However, the various shell constructs such as pipes and streams make it much more powerful than an ordinary REPL.

Let us take a look at a simple bash session:

    $ g++ ./otp.cpp -lcypto -o otp
    $ ./otp secret_key
    32482364
    $ echo -n 32482364 | sha256sum
    63c798dc3c8b4a69d79611490d2f0b68c0871143dd9ec3834e56eceb0799e0b9 -
    $ curl -X POST http://inspectb.in/34e00b31 -d \ "hash=63c798dc3c8b4a69d79611490d2f0b68c0871143dd9ec3834e56eceb0799e0b9"
    ok
    $ curl -I http://httpbin.org/ip
    {
      "origin": "103.37.201.27"
    }

All lines that begin with `$` are a command. For eg, the command `g++ ./otp.cpp -lcrypto -o otp` compiles the c++ source file `otp.cpp`. The next command runs the resulting binary (`otp`) passing it the string `secret_key` as input.

The next command makes use of pipes to pass input the `sha256` program. The last two commands use the `curl` utility to make HTTP requests to different URLs.

All of this was done on the command line, and that is the power of the command-line: It can do everything that you can do using other tools, but faster and more effeciently.

For eg, to make the same POST request would require you to either do the following:

- Write some HTML and run it in your browser
- Install a browser extension that lets you send HTTP requests
- Write some code in your programming language of choice to make a request.

Using a cli gives you access to an arsenal of tools such as `curl`, which can be used to do a lot of things.


##Shell Basics

The two most powerful concepts in using shells are pipes and streams.