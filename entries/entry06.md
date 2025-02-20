# Entry 6: Logging Off 
##### 6/2/22

### Context

This will likely be my last blog entry, because we are wrapping up our freedom projects. I will reflect more on the freedom project in the conclusion, but for now, we'll talk about another feature I added to my project, which is now online and can be checked out [here](https://uxma-student-status-e2291.web.app/). Becuase this project is a more personal one, I will not be providing credentials. However, my showcase presentation will show how the project in action. 

Now right away, a new feature you may notice compared to my last blog entry is that there is now a log-in. I decided to create a modal since I felt that would be the easiest way for me to authenticate users, especially because it's only one page. 

<img src="https://raw.githubusercontent.com/jancarloa0524/sep11-freedom-project/main/imgs/modal.png" alt="modal login" width="500">

Of course, when the user tries to login and fails to do so, an "Incorrect password!" message will appear in the modal. I do not allow users to sign-up to the site, due the site being oriented only towards the Taekwondo do-jang that I work for. This simple modal however, can be deleted by anyone who decides to just use inspect element. That's why I implemented security rules which prevent data changes unless the user is logged in. When the user tries to enter data without logging in, Firebase will return an error which I then use to cause an alert:

<img src="https://raw.githubusercontent.com/jancarloa0524/sep11-freedom-project/main/imgs/alert.png" alt="modal login" width="500">

Making sure the website goes online was actually really easy, I only had to install the Firebase CLI into my terminal in Visual Studio Code, and then connect Firebase hosting to my project, which was a pretty simple process of just selecting my `index.html` file as the main file to be hosted. 

In addition to all of this, I will be talking about my [Expo Elevator Pitch](#expo-elevator-pitch-takeaways), [In-Class Presentation](#in-class-presentation-takeaways), and [Overall Takeaways](#overall-takeaways).

### Challenges

Implementing a login was actually quite the task, starting with figuring out how to make a modal to begin with. I followed this [simple tutorial](https://www.youtube.com/watch?v=XH5OW46yO8I), and from there added a login form into the actual modal. 

In order to authenticate users, you need to implement [Firebase Authentication](https://firebase.google.com/docs/auth). 

First, you'll need to import Authentication and initialize the service:

``` javascript
import { getAuth } from 'firebase/auth'

const firebaseConfig = {
    // Config Info
  };

// init app
initializeApp(firebaseConfig)

// init services
const auth = getAuth()
```

Like I said in my last entry, **Firebase is modular**. So, whatever functions I need, I just need to import. In order to implement a log-in, all I needed was to do was use the DOM to connect to the login form, and use the function: `signInWithEmailAndPassword()`, like so:

``` javascript
// Parameters: Authentication database, user inputs for email and password fields; Returns a promise once complete
signInWithEmailAndPassword(auth, email, password)
        .then((cred) => { 
            console.log('user logged in:', cred.user) // log user credentials
            loginForm.reset() // reset form
            modal_container.classList.remove("show"); // Removes modal
        })
        .catch((err) => {
          console.log(err.message) // log error
          loginForm.reset() // reset form
          document.getElementById('modalParagraph').style.display = "block"; // Display "incorrect credentials" message
        })
```

That was easy enough, but the difficult part came with actually securing my data, which I wasn't sure exactly how to do. First, I needed to go back to Firestore, and set up my security rules. 

**NOTE:** *While you can set up security rules in the Firebase console website, those security rules are more like a test-bed. Once you host your site like I do later on, you will need to set up security rules by setting it up with the Firebase CLI in youre console.*

This was also actually really easy:

```
rules_version = '2';
service cloud.firestore {
  match /databases/{database}/documents {
    match /{document=**} {
      allow write: if request.auth != null
      allow read;
    }
  }
}
```

The important part to focus on here is `allow write: if request.auth != null` and `allow read;`. What this basically means is, only allow the user to write data if they are logged in, and always allow the user to read data. 

Now, if users just deleted the modal, they still wouldn't be able to interact with the database. 

The last issue I wanted to fix was the fact that logging in with Firebase Auth functions differently than I thought it would. When the user reloads or closes the page for example, it won't automatically sign out that user like I thought it would, so I needed to use the following functions: `setPersistence()` (*where the paramters of this function are the authentication database, and types of persistence, which are listed next*), `browserSessionPersistence`, and `inMemoryPersistence`.
This function then returns a promise, which is a sign-in method of your choice, along with the promise of that method. 

``` javascript
setPersistence(auth, inMemoryPersistence, browserSessionPersistence)
    .then(() => {
        return signInWithEmailAndPassword(auth, email, password)
        // code from earlier
    })
```

`browserSessionPersistence` makes sure that the user is signed out if the user closes out of the browser, and `inMemoryPersistence` makes sure that the user is signed out if the user reloads the site.

### EDP
Right now, stage 8 of the Engineering Design Process, since I have already communicated my results in presentations and will participate in a final showcase. But I also feel I'm still at stage 7, since I want to improve my project even more. The CSS needs more work, and I want to implement more features, such as pi-charts that help interpret the data collected from attendance that week.
### Skills
I feel like I definetly focus on **"How to learn"** pretty well, since I learned how to implement Firebase Auth, with a mix of security rules from Firestore, including a bit of CSS and even Firebase hosting. Because I understand Firebase way better now, learning it is becoming easier and easier, especially the more I understand the way it all works. The tutorials I used are becoming easier and easier to follow as well.

I also feel I focused quite a bit on **"Problem Decomposition"**, becuase I broke everything down into pieces, doing every part of the log-in piece by piece. First figuring out how the CSS would work, then implementing actual authentication and persistence, then securing data. 
## Conclusions

### Expo Elevator Pitch Takeaways
The SEP11 Expo was essentially like a sort of science fair, where students in our school checked out projects from all the SEP classes. We had to present them fairly quickly, especially to judges. 

*The "Elevator Pitch" I used as a reference when talking to students and judges about my project can be found at the bottom of my notes for this year [here](https://docs.google.com/document/d/1AERpjNvYGv-7j0zZt-k7CRXWcGlXSNnC0KNSQBOWf4k/edit?usp=sharing).*

Presenting my project was a bit nerveracking at first because I just could not remember my script that well, but when the first group of students walked over to my table, I just couldn't contain my excitement for my project because I genuinely love what I've created, and I feel that when you are truly invested in something you accomplished, you'll already know exactly what to say about it. The judges really seemed to love my project, and I feel the energy and excitement for my project really played a part in that. Overall, what I can take away from this experience is that, presentations need to be captivating and energetic, something that people can hang on to every word for. And the perfect way to get there, is to love what you do. 
### In-Class Presentation Takeaways
My presentation was a little bit much I have to admit, it took me way longer than 10 minutes to present in it's entirety, but I honestly felt like there was just so much to explain. 

*My presentation can be found [here](https://docs.google.com/presentation/d/1RGx41RWF23EAVL7cKrE1FMT5hiI3WmC2Rz9e64mWKHg/edit?usp=sharing)*

Creating my slides, I felt like I could explain everything really quickly, and while presenting, my explanations were thorough, showing that I really understood everything I said and did. But, what I can take away from this presentation is that I need to also make sure I focus on what is necessary. Talking about the challenges I encountered could have probably been far shorter, since I went in depth into explaining some code I probably didn't need to explain. I felt my presentation was overall great, I just need to make sure I'm straight to the point while being understandable.
### Overall Takeaways
This project has honestly been quite a journey, since I started off knowing barely anything about JS, and deciding to just do the tool said to be the most difficult, and even trying an idea that might have been way too difficult for me. But through this process, I have learned so so much, more than any other project I've done. This project was a difficult one that required a lot of time and effort, which I put so much into in the moments that I could. It's bare-bones as of this entry, but it works, and I'm proud of what I was able to make. 

[Previous](entry05.md)

[Home](../README.md)