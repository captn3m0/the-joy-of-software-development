# HTTP, REST and APIs

**Note**: Beta chapter. Might contain errors and mistakes. Read with caution. File an issue on github if you spot a mistake.

HTTP is perhaps the most-used application layer protocol in existence. Most of the network traffic
that flows over the internet identifies as HTTP. This includes everything you do on Facebook, most of what
Netflix is streaming, and everything you'd count as "content" (such as Wikipedia, or New York Times).

I love HTTP. I think all web developers should strive to understand it deeply, because it is what makes the web,
after all. Even if you are not interested in web development, learning a protocol that is so deeply
entrenched everywhere is a meaningful endeavour, and I highly recommend it.


## HTTP

The Hyper-Text Transfer Protocol was invented by Tim-Berners Lee, giving rise to what we call the "World Wide Web", or
more commonly as the "Web". There are a few key pieces of why HTTP is so great at what it does, and what I'd count
as the reasons behind its success:

1. Plain Text: HTTP is a plain text protocol, which means its very easy to implement for a programmer. Writing web servers
is as simple as writing a TCP socket server that sends back proper plain text responses.
2. Linkability: Most of the protocols that came before HTTP implemented decentralization on the server side usinc server syncs and transfers, such as Gopher and SMTP. HTTP on the other hand, followed the same principles of decentralization but allowed the client content to link to other servers. The simple fact that you can click on a link on google.com to reach twitter.com is magical, if you haven't seen it before.
3. Stateless: HTTP did not have a concept of sessions at the start. Every request made to the server is a fresh request with no knowlege of any previous requests that might have been made. This simplification makes it very easy for a programmer to implement HTTP.
4. CGI: Common Gateway Interface was a very popular way to hook up an HTTP server with a shell script, or any other application. It allowed people to create dynamic websites, which paved the way for the internet to become what it is today (lots of cat pictures).

When you are making a web request to any server, your browser does the following:

1. Opens a TCP socket to the website (after resolving it via DNS)
2. Sends some request data over the wire in plain-text format
3. Wait for a response
4. Read the response data as it arrives over the TCP connection
5. Render the returned HTML in your browser so its readable.

Both the request and response in HTTP is divided into two secions: a header and a body. The header is a key-value store that holds some metadata information about the request/response. The body on the other hand is the content of the request/response itself.

However, a look at the HTTP packet structure shows one more section:

```
POST /search
Host: google.com
User-Agent: josd-reader

q=hello+world
```

The two headers are separated from the body with a `\r\n\r\n`, as defined in the HTTP spec. However, even before the header, the client must provide the URI of the resource that you are trying to access. This is provided as an argument to the HTTP verb (GET in this case). The "path" of this request is "/search", as a result.

Different RFCs define various headers and body encodings used in the HTTP protocol. For eg RFC [X] specifies the date format used in all HTTP communication. (Irrespective of the header). The User-Agent format is defined in RFC [Y], and the Encoding header format is specified in the HTTP Spec itself.

If you are interested in the entire HTTP request/response cycle, it is covered in a lot more detail in the [what-happens-when](https://github.com/alex/what-happens-when) repository, which tries to answer "What happens when you type google.com into your browser and press enter?"