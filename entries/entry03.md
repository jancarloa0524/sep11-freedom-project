# Entry 3
##### 2/13/22

### Context:

This time, I got around to learning a bit more about [Firestore](https://firebase.google.com/docs/firestore/?authuser=0) and how to use it, through a [tutorial](https://firebase.google.com/codelabs/firestore-web?authuser=0#0) to creating a Firebase project that uses Firestore. The project itself is a restuarant review site. 

I also ended up chaning my plan for my FP, which I will explain the reason why, and detail now. First, my original idea I feel is far too difficult for me to create at the rate I'm learning. So, I decided to do something a little simpler, since it was an idea I began to work on anyway. I have started to track the progress of students that I teach, so now, instead of making a schedueler to help me plan classes and such, I'm going to instead make a status reporter. It's simple, I input the names of students that attend everyday, and by the end of the week, the program will have already made the data of attendance ready for me, all I would need to do is write an entry for each student. I can input this into a program which Firestore can store every day, and then can retrieve once the final day comes, from there, I put in my entries, and the output is a fully completed status report. This idea, I feel is far more unique and doable, since the schedueler was really just a more personalized calendar. The status reporter, could be used by a lot of people actually, who are looking for an easy way to track the progress of people. 

I actually prototyped it a little bit, and created a program that sort of does the very basics of my idea. It can create a list of students, and the days they came in for class, however it creates a table that has duplicate rows of data. Each students name is repeated, for each day they come in, instead of only being written once, with the number of days they took class all written in the 2nd column of that row. 

``` javascript
function week(monday, tuesday, wednesday, thursday, friday, weekStr) {
    weekStr = monday + tuesday + wednesday + thursday + friday
    let array = weekStr.split(" ")
    let finalSet = [...new Set(array)]; // Removes duplicate names in previous array
    console.log(Array.from(finalSet))
    return Array.from(finalSet)
}
```

The above is a snippet of code from the program, and it essentially creates an array of every student that came in for class that week, by putting every day of students into a huge array, and turning it into a Set which deletes all the duplicates. This is used as a sort of "check" later on in my program, in a bunch of for loops that really become way too complicated. 

Now, aside from this, I had to learn quite a bit. It was a bit of a process, even changing IDE's, because CS50's IDE simply wasn't cutting it, since I could not install and run the Firebase CLI. But from this process, I ended up learning about:

#### Firestore

Basically, Firestore follows a [NoSQL data model](https://firebase.google.com/docs/firestore/data-model?authuser=0), which are easy to read but not easy to write. This is perfect for websites, since you need to read information to the user more often than not, so servers need to be able to handle this. 

Firestore Data is stored in **Documents and Collections**. This data is accessed via a file tree method, where documents can only be found in collections, and documents can connect to a collection (so deleting said document won't delete that collection). So, you end up with a system sort of like this:

`Collection => Document => Linked Collection => Document`

For the purposes of the project, our data could look like this:

`restaurants => restaurant1 => reviews => review2`

Where `restaurants` and `reviews` are collections, and `restuarant1 and review1` are documents. 

Documents themselves hold JSON data which is very easy to read and store. 

#### Project Examples

The first thing I learned was how to add documents to a collection

``` javascript
FriendlyEats.prototype.addRestaurant = function(data) {
  var collection = firebase.firestore().collection('restaurants');
  return collection.add(data);
};
```

Basically, the above code takes documents, each of which are Restaurants, and it puts them into a collection called `restaurants`. The app itself essentially generates a random list of documents to add for us. We can't actually read this data on our site yet, though.

So, we write this:

``` javascript
FriendlyEats.prototype.getAllRestaurants = function(renderer) {
  var query = firebase.firestore()
      .collection('restaurants')
      .orderBy('avgRating', 'desc')
      .limit(50);

  this.getDocumentsInQuery(query, renderer);
};
```

This code above will retrieve 50 restaurants from the collection to display on the page, ordered by average rating. 

``` javascript
FriendlyEats.prototype.getAllRestaurants = function(renderer) {
  var query = firebase.firestore()
      .collection('restaurants')
      .orderBy('avgRating', 'desc')
      .limit(50);

  this.getDocumentsInQuery(query, renderer);
};
```

And this code above is a **snapshot listener**, which will listen for changes in our data and update the page. 

We also need to get data for each restaurant.

``` javascript
FriendlyEats.prototype.getRestaurant = function(id) {
  return firebase.firestore().collection('restaurants').doc(id).get();
};
```

The above code does exactly this, when we click on a restaurant in our list displayed on the page, we will use this to see the data on that restaurant.

The rest of the code used in the Firebase project becomes much longer and more difficult to understand, but you essentially also add the ability to filter your data for specific results, and submit a review. 
Filtering data obviously requires using Firestore to change the results on the page, which is done by "Deploying Indexes", and submitting a review is essentially adding a document to the collection `reviews` based on the input given. 

From here, we update the security rules on our website, so that only "Safe" changes can be made by users, such as using a sign-in to manage your own reviews. 

Firestore is a complex way to store data, made simple. To me, it isn't so simple yet, but it will be soon I'm sure. 

### EDP:

Right now, I'm definetly still on **Step 2 of EDP**, since I'm still **researching** Firebase, but I'm actually also on **Step 5**, since I have been creating and testing a **prototype** that works based off of what I already know about Javascript. The next steps for me are to honestly learn more about arrays specifically and how to work with that data in Javascript, as well as continuing to learn about Firebase. So now, it will be even more research. 

### Skills:

I feel I definetly worked more on **Time Management**, since I ended up doing quite a bit. I didn't make a lot of progress on just Firebase, but I did end up creating a prototype of sorts, which worked. I mostly worked on this on whatever breaks I had, and that has paid off. 

I also really improved my **Logical Reasoning**. I often make things a lot harder than they have to be for myself, all because I feel like challenging myself with a really unrealistic goal. So, I'm happy I thought this through and had the logical reasoning to decide on a new project. 

### Conclusion:

I made quite a lot of progress in general, but individually not as much. The prototype, while it is progress, is also sort of meaningless since I'm going to rewrite all of it anyway. But, it did help me realize I needed a lot of help with learning arrays and such, so I'm very happy that I realized this. I'm going to focus more on learning, since my project is much easier to create, so the creation process can wait a bit, while I try to get myself caught up. 

[Previous](entry02.md) | [Next](entry04.md)

[Home](../README.md)