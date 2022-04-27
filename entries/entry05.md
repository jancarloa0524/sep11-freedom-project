# Entry 5: Burning Through Code
##### 4/26/22

### Context

Over the Spring Break, I realized that I really needed to work on my Freedom Project (which you can view [here](https://github.com/jancarloa0524/uxma-student-status)). Luckily, I was easily able to find a good [tutorial](https://www.youtube.com/watch?v=9zdvmgGsww0&list=PL4cUxeGkcC9jERUGvbudErNCeSZHWUVlb) on learning Firestore, because I honestly didn't really understand how Firestore worked. Despite [Entry 3](entry03.md) being a tutorial that I also followed, which did help me understand how Firestore works, it didn't help me understand how to actually work with the syntax. Rather it made me copy + paste code and attempted to explain it. While I then understood what it did, I felt I needed a simpler explanation. I could have tried to break down the code I saw and looked through Firebase's documentation for it, I felt so confused by what I saw that I wasn't sure I would understand it anyway. That is where the first tutorial comes in, since it explained every part of Firebase/Firestore to me, to the point where I now understand how to really use Firebase. 

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

<img src="https://github.com/jancarloa0524/sep11-freedom-project/blob/main/imgs/prototype-img.png?raw=true" alt="prototype" width="400">

This is pretty much it, first you have options for adding data, then the real-time data table which would hold the students who attended class *(so if `attendance: []` instead of say, `attendance: ["Monday", "Tuesday"]`, then they do not appear in this table)*. Then you've got the options for resetting or removing data, and finally, a reference table for the students names, because you need to input the name correctly for it all to work. For someone who already works with those students everyday, this isn't much of an issue. For many of these, I really didn't struggle much, the common issues I encountered was trying to figure out how specific data like attendance is added or removed, which I learned is done with the functions `arrayUnion()` and `arrayRemove()`.

### Challenges

So while doing all of this within a week was a challenge itself, the challenges I faced while programming this were mainly:
1. Creating the first real-time table
2. Creating the ability to add certain days to a students attendance
3. Adding the ability to add to a students report, rather than just writing a whole new one. 

Through these challenges, though, I learned that one way to test out my code was to create a simpler version of what I want in jsbin. I will be going over one of these, since the explanations are in-depth. 

For the real-time table, I needed to figure out how to make it so that the user can see the data being updated in real-time, meaning the table could be adding/removing students, and adding/changing data within it. I knew I had to use `onSnapshot` for this, and had to loop through each and every doc. I figured that once I loop through each doc, I needed to use the DOM to create the elements of the table needed, and set the data for each cell, by creating an example in [jsbin](https://jsbin.com/qikaguquxo/2/edit?html,css,js,console,output). This ended up looking something like this, when written with Firebase in mind:

``` javascript
import {getFirestore, collection, onSnapshot} from 'firebase/firstore' 

onSnapshot(colRef, (snapshot) => {
    var table = document.querySelector('.table') // Select the table

    // Select every doc and add a row of data from it 
    snapshot.docs.forEach((doc) => {
        // Create and append the row to the table
        let row = document.createElement('tr')
        row.classList.add('row')
        table.appendChild(row)
        // If the document's attendance is NOT equal to nothing, then add data to each cell. 
        if(doc.data().attendance != "") {
            for (var j = 0; j <= 2; j++) {
                let item = document.createElement('td')
                if (j == 0){
                    item.innerHTML = doc.data().name
                } else if (j == 1) {
                    item.innerHTML = doc.data().attendance.join(', ')
                } else if (j == 2) {
                    item.innerHTML = doc.data().report
                }
                row.appendChild(item)
            }
        }
    })
})
```
While this did work, once I actually added data, it wouldn't just update the data live, it would add an entirely new set of data to the table, instead of only adding that specific data. 

The challenge I really encountered here was this: was the solution one that used purely javascript, or one that Firestore could solve? From the demo in [Entry 3](entry03.md), I thought my solution would be one found in the documentation for Firebase, but after digging for a solution, I couldn't find any. 

So, I decided to go back to the [jsbin](https://jsbin.com/qikaguquxo/2/edit?html,css,js,console,output) and test out the purely Javascript approach, which worked very well. My final code looked like this:

``` javascript
// Real-Time Table
onSnapshot(colRef, (snapshot) => {
    var table = document.querySelector('.table')

    // Upon recievining a "snapshot" of the collection once a change is made, I delete ALL the current data shown, before adding the new data!
    let rows = document.querySelectorAll('.row')
    for (var i = 0; i < rows.length; i++) {
        rows[i].remove()
    }
    let data = document.querySelectorAll('td')
    for (var i = 0; i < data.length; i++) {
        data[i].remove()
    }

    snapshot.docs.forEach((doc) => {
        let row = document.createElement('tr')
        row.classList.add('row')
        table.appendChild(row)
        if(doc.data().attendance != "") {
            for (var j = 0; j <= 2; j++) {
                let item = document.createElement('td')
                if (j == 0){
                    item.innerHTML = doc.data().name
                } else if (j == 1) {
                    item.innerHTML = doc.data().attendance.join(', ')
                } else if (j == 2) {
                    item.innerHTML = doc.data().report
                }
                row.appendChild(item)
            }
        }
    })
})
```

I feel that the comment pretty much explains exactly what I did. To summarize the challenges I faced, I had to understand when to use Firebase and when to use pure Javascript to find a solution, as well as testing solutions through jsbin. 
### EDP

I'd say that I jumped all the way to Step 7 of the *Engineering Design Process*, which is to **Improve as needed**. I now have a very much working prototype, and the improvements I want to make are simple, making this into a better UI. This won't change my current code very much and in fact, will probably be more HTML and CSS heavy, while only creating minor changes to my code. I do want to add many more features however, because I will actually be using this in the future. 

### Skills

I'd say that I definetly improved **How to learn**, because I literally had to learn some basic Firestore functions within a week, on my own. This was made easy with the right research and tutorials. 

I'd say I also improved my **Creativity**. I'd say I found solutions to my problems really quickly because of this, especially with my idea of trying to break down what it is I'm trying to do by recreating that specific component in jsbin. Once I've done this, I easily move on to trying to implement my solution, which so far, has worked perfectly. 

### Conclusion

Firebase, and Firestore, are very complex tools. However, they are very powerful tools as well, while being relatively simple once you learn to understand how it all really works. I have to pay special attention to detail when working with Firebase, because the solutions to my problems could be very easy if I just think about the solution in the right way. 

[Previous](entry04.md) | [Next](entry06.md)

[Home](../README.md)
