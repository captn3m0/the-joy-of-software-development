#Software Security

Irrespective of what field you are working in, its always nice to have an understanding of basic computer security. A lot of it is dependent on the nature of work you are doing; for instance securing a web server is way different than securing the source code for a mobile app. I'll cover most fundamental principles and some specific advice.

Need: Often the security aspect of an application is ignored, downplayed, outsourced or sometimes added as an afterthought. There have been many large security breaches recently, and it just goes on to show that getting security right is hard.

Security is very often described to be  as weak as the weakest link, and that is usually true. We as software developers have a responsibility to make sure that what we make is as secure as it should be.

Don't read this chapter and expect to become an expert in it. If you are making a product where security is of paramount importance, hire an expert. There are dozens of cases of half-assed security measures being taken across the industry and it comes back to bite you each time. Choosing cost over security is never the right choice. Just don't do it.

A very counterintuitive idea in security is that the more open and simple a design is, the more secure it is. There are two portions to this argument:

1. Open designs are more vetted, and vulnerabilities are more liable to be identified quickly. There are some people who would argue against this, but historically open designs are much less likely to be vulnerable or have backdoors.
2. Simpler schemes that involve less moving parts are much more secure. Each piece of complexity you introduce brings with it, what we call additional surface area of attack. For instance every additional login mechanism you add to your site is another piece to be attacked.

Another idea that is popular in cryptography is that you *never make your own crypto*. Cryptography is very easy to screw up. A simple mistake of failing to seed the random number can be fatal. If there is one thing you remember from this chapter, let it be this: Don't ever write your own crypto algorithm.

If you do, make sure that you have a PhD in crypto, get it published, vetted, standardized and wait a long time(years) before using it in production.

#Some Basic Principles

##Least privilege
Any piece of code that running on the system should be able to the least amount of damage if it falls apart. For instance, is your script only supposed to write to database, make sure that it doesn't have rights to drop the database.

Even simple things like opening a file in r+w mode when just r would suffice matter. Make sure that the next time you are building something, all its portions are running with the least rights they possibly can.

The point of computer security is to mitigate and reduce the possible threats to a system, and the principle of least privilege is an excellent rule that does exactly that.

##Saving passwords
Don't store passwords in plaintext, like what youporn did. Don't just hash them with sha1 like what LinkedIn did. Don't encrypt them with AES like what Adobe did.

Just use bcrypt. bcrypt is a slow hashing algorithm that is specifically made to deter attacks such as brute-forcing and rainbow tables. It incorporates a salt and a cost parameter to be future proof.

It is trivial to use in all programming languages, and is widely supported. Don't overthink it and just use bcrypt.

##Don't trust users
While its true that not all users are going to attack your system., it only takes one determined hacker to screw things up. Consider all user input to be tainted. The location based with that you were thinking about can be hacked by simply spoofing the GPS. The user's about me field is not always going to be text. And the hidden userid field in your HTML needs to be validated as well.

This can be understood especially well if you have ever worked on a multiplayer game. Game Developers always have the choice of making dumb clients where all computations are done on servers, or intelligent clients where the client can compute renders by itself based on its own information and that provided by the server.

The trouble is to what degree can the game server trust the client. 