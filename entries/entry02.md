# Entry 2: __Read/Write/Read/Write/Read/Write__
##### 12/13/21

### Context:

So far, I haven't made _a lot_ of progress, but I have made some. My scheduele has been so busy that it's difficult to find time, plus, a few things have caused things to only be harder. But I'm going to talk about my goals for the winter break, and until my next blog entry, and try my best to achieve them. So far, I've learned some of the basics of Firebase itself, but not it's services just yet, I still need to learn how to use it's services, which the first one I'm currently trying to learn is [Firestore](https://firebase.google.com/docs/firestore?authuser=0). I found that learning Firebase, requires looking into every bit of documentation I can. I have to dive deeper and deeper into every link within each subcategory of documentation, in order to fully understand it. An example of this is when I learned about __Module Bundlers__ (defintition). From [Add Firebase to your Javascript project](https://firebase.google.com/docs/web/setup), as I reached __step 4__ (module bundlers), I had to then go to another doc on [Using module bundlers with Firebase](https://firebase.google.com/docs/web/module-bundling), and from there decide on the module bundler I wanted to use, which was [Webpack](https://webpack.js.org/guides/getting-started/), which was even more documetnation to read and follow. This is sort of the reason why it's taking quite a bit for me to make such small amounts of progress, as I will discuss later, the content I need to learn is very dense. Here are some code snippets as to how I installed Webpack:

``` javascript
//Lodash
import _ from 'lodash';

// Webpack
function component() {
  const element = document.createElement('div');

  // UPDATE: LODASH NOW IMPORTED BY THIS SCRIPT; OLD: Lodash, currently included via a script, is required for this line to work
  element.innerHTML = _.join(['Hello', 'webpack'], ' ');

  return element;
}

document.body.appendChild(component());
```

This is a part of `index.js`, which essentially imports other scripts within the `src` folder. Basically, this imports something called `lodash` into our project which is required for webpack to work. Lodash alone is another thing I can look into which I haven't already, but from it's description, it makes it easier to work with arrays of data.

You can also see lodash in `package.json`

``` javascript
{
  "name": "firebase-testing",
  "version": "1.0.0",
  "description": "",
  "private": true,
  "dependencies": {
    "firebase": "^9.4.1",
    "lodash": "^4.17.21"
  },
  "devDependencies": {
    "webpack": "^5.64.0",
    "webpack-cli": "^4.9.1"
  },
  "scripts": {
    "test": "echo \"Error: no test specified\" && exit 1",
    "build": "webpack --mode=development"
  },
  "keywords": [],
  "author": "",
  "license": "ISC"
}
```

`package.json` is important to the bundling process, as it lists dependencies when you install them from your terminal. You'll also notice in scripts, that I added a "build" script that essentially makes it easier to run webpack.

This is just some of what I've learned, but the process to learning all of this, required a lot of reading and testing. In general, like I said before it took some time to learn just these basic steps, especially with my limited time constraints.

### EDP:

I'd say I'm still where I was before, because I'm still __Researching the Problem__, I'm still learning about Firebase and it's services, but I'm also at the __Create a Prototype__ stage. Due to what I've learned so far, I'm able to prototype some of the basic connections to Firebase for the project. Clearly, the next steps would be to continue creating my prototype as I learn Firebase and Javascript, and eventually reach the __Test and Evaluate__ phase in order to understand the issues my program might have, what else I might have to learn, etc.

### Skills:

I learned a lot about __How to read__, because the documentation for Firebase is __DENSE__. I had to really closely read everything in the documents, and folow the instructions carefully. The more links I found, the more research I found I had to do. This was very important for me to imrpove because for the rest of this project, I feel I will be looking at lots and lots of documentation, so I need to learn how to do this process faster and more efficiently.

I also learned a lot about __Problem Decomposition__, because of the fact that as the documentation breaks itself down, it is essentially teaching me more and more ways to produce the bigger result that I want. The process for installing and utilizing Firebase and module bundlers is a complex one but one that, when you break it down, becomes much easier to do. This is something I'm definetly going to need to do when making my project.

### Conclusion:

I want to be in a much better place for my project, because I don't feel like I have made as much progress as I would have liked to. So, over the break, I'm going to really dedicate some time to learning more about Firebase, especially to really understand just how much I might have to learn, and how fast I can do it before I need a prototype ready and working. So, my plan right now is simple, to learn more about Firebase in the coming weeks and try to delve deep into it.

[Previous](entry01.md) | [Next](entry03.md)

[Home](../README.md)