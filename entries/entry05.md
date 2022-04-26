# Entry 5: Burning Through Code
##### 4/26/22

### Context

Over the Spring Break, I realized that I really needed to work on my Freedom Project. Luckily, I was easily able to find a good [tutorial](https://www.youtube.com/watch?v=9zdvmgGsww0&list=PL4cUxeGkcC9jERUGvbudErNCeSZHWUVlb) on learning Firestore, because I honestly didn't really understand how Firestore worked. Despite [Entry 3](entry03.md) being a tutorial that I also followed, which did help me understand how Firestore works, it didn't help me understand how to actually work with the syntax. Rather it made me copy + paste code and attempted to explain it. While I then understood what it did, I felt I needed a simpler explanation. I could have tried to break down the code I saw and looked through Firebase's documentation for it, I felt so confused by what I saw that I wasn't sure I would understand it anyway. That is where the first tutorial comes in, since it explained every part of Firebase/Firestore to me, to the point where I now understand how to really use Firebase. 

Another thing I'd like to point out is that the project I made in the last entry, while helpful in my understanding of Javascript and what I wanted for my project in general, ended up being entirely useless. The fact is that I realized that what I wanted to do with my site was show the data and it's changes live, and my project did not do this. 

### What I learned about Firebase/Firestore

The first thing I essentially realearned was:
#### **How to install webpack,**
into my project. While I learned how to do this in my [second entry](entry02.md), the proecess it presented was much more difficult than the process I learned through the tutorials. To simplify it, all I needed to do was:
1. Set up my `dist` and `src` folders with the necessary files
2. Create package.json with `npm init -y`, install Webpack, and then Firebase into project directory via the terminal. This will create a bunch of files. 
3. Set up `webpack.config.js` and copy-paste the following. (This essentially sets up webpack to bundle all your written code into a bundle.js, which is the file your website will read.)
``` javascript
const path = require('path')

module.exports = {
  mode: 'development',
  entry: './src/index.js',
  output: {
    path: path.resolve(__dirname, 'dist'),
    filename: 'bundle.js'
  },
  watch: true
}

// init firebase
initializeApp(firebaseConfig)
```

4. Make sure to type in `"build" : "webpack"` into the scripts section of `package.json`

And thats it! Just link `bundle.js` in your index.html file and it's complete! Make sure to run `npm run build` in your project directory with the terminal so that it bundles your code. I then learned how to

#### **Write Code w. Firebase**

Doing this actually became really simple once I understood that **Firebase is modular**. The functions that you want to use, you will need to import at the top of the `index.js` file. This is shown clearly with the following code:

``` javascript
import { initializeApp } from 'firebase/app'

const firebaseConfig = {
    apiKey: "",
    authDomain: "",
    projectId: "",
    storageBucket: "",
    messagingSenderId: "",
    appId: ""
  };

// init app
initializeApp(firebaseConfig)
```

At the top, I import the function `initializeApp()`, which will initiailize the Firebase Configuration shown. In order to import Firestore and it's functions, I need to write the following:

``` javascript
import { getFirestore } from 'firebase/firestore'

// firebaseConfig and initialization here, etc. 

// Grabbing the Firestore database / init firestore
const db = getFirestore()
```

This essentially connected me to the database. Now, if I want to access a collection, I would import the function `collection()`, and then if I want a doc, I would need `doc()`, and `getDoc()`. That would look like this:

``` javascript
import { getFirestore, collection, doc, getDoc} from 'firebase/firestore'

// firebaseConfig and initialization here, etc.

// Grabbing the Firestore database / init firestore
const db = getFirestore();

// Collection reference to "collectionExample" from database
const colRef = collection(db, 'collectionExample')

// Document reference to "document ID" in "collectionExample", from database
const docRef = doc(db, 'collectionExample', 'docID')

// Get document using document reference
getDoc(docRef)
    // After recieving document, then log all it's data, including it's ID, to the consoele. 
  .then((doc) => {
    console.log(doc.data(), doc.id)
  })
```

When reading this code along with the comments, it becomes really easy to understand. The functions are for the most part, pretty simple to use, the only issue is really understanding how data is transferred from the server to the host. I learned about a lot more functions, such as `onSnapshot()` which can get data in real-time, which was perfect for my project. 

### So what exactly did I end up making?

![Prototype](https://github.com/jancarloa0524/sep11-freedom-project/blob/main/imgs/prototype-img.png?raw=true)
### EDP

### Skills

### Conclusion


[Previous](entry04.md) | [Next](entry06.md)

[Home](../README.md)
