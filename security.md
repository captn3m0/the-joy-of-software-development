# Software Security

Irrespective of what field you are working in, its always nice to have an understanding of basic computer security. A lot of it is dependent on the nature of work you are doing; for instance securing a web server is way different than securing the source code for a mobile app. I'll cover most fundamental principles and some specific advice.

Need: Often the security aspect of an application is ignored, downplayed, outsourced or sometimes added as an afterthought. There have been many large security breaches recently, and it just goes on to show that getting security right is hard.

Security is very often described to be  as weak as the weakest link, and that is usually true. We as software developers have a responsibility to make sure that what we make is as secure as it should be.

Don't read this chapter and expect to become an expert in it. If you are making a product where security is of paramount importance, hire an expert. There are dozens of cases of half-assed security measures being taken across the industry and it comes back to bite you each time. Choosing cost over security is never the right choice. Just don't do it.

A very counterintuitive idea in security is that the more open and simple a design is, the more secure it is. There are two portions to this argument:

1. Open designs are more vetted, and vulnerabilities are more liable to be identified quickly. There are some people who would argue against this, but historically open designs are much less likely to be vulnerable or have backdoors.
2. Simpler schemes that involve less moving parts are much more secure. Each piece of complexity you introduce brings with it, what we call additional surface area of attack. For instance every additional login mechanism you add to your site is another piece to be attacked.

Another idea that is popular in cryptography is that you *never make your own crypto*. Cryptography is very easy to screw up. A simple mistake of failing to seed the random number can be fatal. If there is one thing you remember from this chapter, let it be this: Don't ever write your own crypto algorithm.

If you do, make sure that you have a PhD in crypto, get it published, vetted, standardized and wait a long time(years) before using it in production.

# Some Basic Principles

## Least privilege
Any piece of code that running on the system should be able to the least amount of damage if it falls apart. For instance, is your script only supposed to write to database, make sure that it doesn't have rights to drop the database.

Even simple things like opening a file in r+w mode when just r would suffice matter. Make sure that the next time you are building something, all its portions are running with the least rights they possibly can.

The point of computer security is to mitigate and reduce the possible threats to a system, and the principle of least privilege is an excellent rule that does exactly that.

## Saving passwords
Don't store passwords in plaintext, like what youporn did[TODO:Citation]. Don't just hash them with sha1 like what LinkedIn did. Don't encrypt them with AES like what Adobe did.

Just use bcrypt. bcrypt is a slow hashing algorithm that is specifically made to deter attacks such as brute-forcing and rainbow tables. It incorporates a salt and a cost parameter to be future proof.

It is trivial to use in all programming languages, and is widely supported. Don't overthink it and just use bcrypt.

Argon is another hash function that has been vetted and is recommended for password hashing. Do check if it is available in your language of choice easily.

## Don't trust users
While its true that not all users are going to attack your system., it only takes one determined hacker to screw things up. Consider all user input to be tainted. The location based with that you were thinking about can be hacked by simply spoofing the GPS. The user's about me field is not always going to be text. And the hidden userid field in your HTML needs to be validated as well.

This can be understood especially well if you have ever worked on a multiplayer game. Game Developers always have the choice of making dumb clients where all computations are done on servers, or intelligent clients where the client can compute renders by itself based on its own information and that provided by the server.

The trouble is to what degree can the game server trust the client. A hybrid alternative is quite common, where the server makes some sanity checks on whatever data the client provides.

Similarly, in any other piece of software, it is essential that all _user input data_ is properly sanitized and considered as _tainted_. The majority of wordpress exploits have been because of untrusted user input being used directly somewhere.

## How to get started

Software Security (commonly known as infosec or netsec) is a vast and complex field. Getting started with software security (becoming a hacker) involves a certain mindset. You must be thinking of how the original piece of code was written and what vulnerabilities it might hold without (often) access to the code itself.

A few good starting points:

### Participate in CTF Contests

Capture The Flag (or CTF) contests are the elite playgrounds of hackers around the world. Various organizations hold CTF contests of varying difficulty. 

TODO: Write some more

### Get certifications

This is a somewhat controversial topic, but there are a few certification courses that are of actual value (in both credibility and knowledge gained) in the industry. A few such courses are:

TODO: Add list

### Keep up with the exploits

Hundreds of exploits and vulnerabilities are announced every week. These include vulnerabilies in softwares that you use daily: Windows, Twitter, Facebook, Chrome, Firefox and almost everything else.

Platforms such has HackerOne and BugCrowd have made reporting security bugs very easy these days. This has also made them a very good medium for accessing recently announced reports. Follow these, and other mediums and stay updated on the new vulnerabilities that are announced daily. There are also a lot of announce-only mailing lists that
specifically announce new CVEs and vulnerabilities.

### Learn the tools

Doing penetration testing, or participating in CTFs will make you understand the importance of toolkits in infosec. Tools are usually classified as offense or defense type, depending on their usage.

An automated tool can often exploit a vulnerability far more easily and faster than you can do it manually, if at all.  Get comfortable with multiple programming languages, especially python.

Note that just knowing how to use the tools is not enough. That will make you a script-kiddie (a term used to denote wannabe hackers who only know how to hack using certain tools). Understanding the concepts behind it, and having the ability to write your own exploits is what makes you a real hacker.

## Attempt Bug Bounties

Maybe companies (including Google, Facebook) offer Bug Bounties for discovering and responsibly disclosing security exploits in their system. These bounties take the form of swag (T-shirts!) and/or monetary reward. If you decide to go hunt for security issues, here are a few do's and dont's:

1. Do ensure you have read the guidelines and understand the scope. Do not overreach beyond what is reasonably expected.
2. Do not report trivial mis-configuration bugs. Google, for eg maintains a list of "nonvulns" (TODO: add link) that is highly informative.
3. Do not run a vulnerability scanner and report the findings as bugs. Take time to craft a report, and understand what the tool does instead.

A few websites: hackerone, bugcrowd etc

## Further Resources

- Links to conferences
- Links to books and recommended readings
- Discuss career choices, crypto, tool development, etc?