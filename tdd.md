# Test Driven Development

Test Driven Development (or TDD) is the practice of writing tests before you write your actual code. However, this chapter is devoted to not just TDD in particular, but the entire practice of writing tests.

Everyone knows that they should test their code.

Almost everyone knows understands that they should write tests for this.

Yet still, the majority of code I see is untested or never written with testing in mind.

If you have never written automated tests yourself, I'm going to walk through an example showing how writing tests can save you from bugs and needless effort.

```js
function basename(path){
  var pieces = path.split('/');
  return pieces[pieces.length - 1];
}
```

This is our base code, committed today. It was written with the following assumptions:

- path is a unix style pathname (/etc/passwd)
- path includes atleast one backslash

After some time, another developer wanted a method to extract the ending portion of an http url. Since this method was part of the common utilities, the developer saved time by reusing this method.

So, earlier we had:

```js
basename('/etc/passwd') -> passwd
```

And now, with the second code commit, it is being used for:

```js
basename('http://twitter.com/elonmusk') -> elonmusk
```

Now, as often happens, the HTTP url was given as user input in the website. However, users were often inputting the twitter usernames instead of the twitter profile links, which broke the function.

The developer decided to add a check:

```js
function basename(path){
  if(path.substr(0,7) !== 'http://')
    throw new Error("Invalid path");
  var pieces = path.split('/');
  return pieces[pieces.length - 1];
}
```

With this check, the method started to throw an error whenever an invalid link was passed to it. All was well, until someone realized that this had broken another piece of code that used this method to parse pathnames.

Remember the original reason the code was written? It was to parse pathnames like `/etc/passwd`. However, now the method throws an error when it is passed the same argument.

We have, essentially broken the code.

Writing tests saves you from this scenario, by essentially what is called "Regression Testing" It is just a way of making sure that your code does exactly what it is supposed to do. The next time someone changes a functionality in the code, the tests will not pass if the previous functionality is affected in any way.

In this case, the test could have been as simple as the following:

```js
if(basename('/etc/passwd')!=='passwd')
  throw new Error('Test failed')
```

This simple test would have failed when the HTTP check was added later.

## Other Benefits

Writing tests has far more benefits than just regression testing. Among these include:

- Modular code: Writing code that can be tested forces you to break your code into smaller pieces.
- Identifying bugs: Tests can help you narrow down the scope of a bug very easily.
- Reducing manual testing: Instead of the write-compile-refresh cycle, you can just run your tests (or have them run automatically on saving). You should understand that you were already testing your code. It was just a slower and more cumbersome process. Automated testing is how to make it better.

## Testing Best Practices

Its difficult to get started with testing for the first time. These are some of the questions I have heard over time:

- Should I test all my code?
- Should I be testing my dependencies?
- If there are nested methods (X calls Y calls Z), how should I write their tests? In which order?
- How much time does it take to write tests?
- Should I use a testing framework? Which one?
 
TODO: Answer these questions (links to SO/programmers.se as well)

## Types of Tests

Over time, tests have come to be classified in two categories: unit tests and integration tests. Unit tests are the small tests, which test a minor functionality encapsulated in a single method.

Integration tests are higher level tests, which test the entire flow of a process. For instance a unit test would check if your money conversion routine works properly or not. On the other hand, the Integration test would run your code as a black box passing it the original input and checking the final output.

The input may be from a text file, or a web page. And the output may be arrived after calls to many different functions. Something like taking the original money parameters and calculating the mortgage in the specified currency.

The primary difference between these two is that Integration tests follow a black box approach, just giving the initial input and testing it against the final output. If your software is an API, the integration test would make an actual call to the API instead of just calling the internal method. The final output will also be checked in the same manner.

## BDD and other concepts








