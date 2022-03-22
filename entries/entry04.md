# Entry 4: A Controlled Fire, For Now
##### 3/21/22

### Context: 

I have finally created a working prototype of my project, but it doesn't use Firebase. I wanted to put what I had learned about arrays and JS objects, to proper use this time, and hopefully I can use some, or even all of this code, in my final project. I overcame a pretty big issue with my project that I couldn't solve the first time around as well. The output is a table of all the students and what days they came in. 

### Prototype 2, technically:
My first prototype did the exact same thing, except, it couldn't organize the days into each student. So, it would end up looking like this:
``` javascript
studentList = [
    ['Student_1', 'Monday'],
    ['Student_2', 'Monday'],
    ['Student_1', 'Tuesday']
    ['Student_2', 'Thursday']
];
```
Instead of something like this:
``` javascript
studentList = [
    ['Student_1', 'Monday, Tuesday'],
    ['Student_2', 'Monday', 'Thursday'],
];
```

My second prototype actually uses JS objects instead of just arrays, because of the fact that JS objects are just so much more organized. I could even create a template for "Student Cards", and everytime a student shows up in the list of students, it creates a Student Card for that student! The template looks like this:

``` javascript
var studentCardTemplate = 
    {
        name:'',
        days: ''
    };
```

And later on in my code, for each student in the student list, the following code runs:
``` javascript
fullListArray.forEach(function(student){
        const profile = Object.create(studentCardTemplate)
        profile.name = student
        studentList.push(profile)
    });
```

`fullListArray` is the full list of students, put together from each day using the same code I used in my last entry. For each student chosen in that array, their name is set, and then I simply push that card, or in this case, `profile`, to the end of the array `studentList`, which is the array of JS object cards. 

Here is where I actually solved a problem I had in prototype 1. In prototype 1, I tried to do the names, and days for each student, all in the same loops, leading to me having three loops, all in one. This did't work out well at all, and they were all regular `for()` loops. This time around, I learned about the `forEach()` method, and the `for in` method. `forEach()` is great with arrays, especially when your going to go through every value in that array. `for in` is great when working with JS objects, because it assigns a variable that goes through every property in a JS object. 

I ended up using both loop methods in a smart way to add the days that students attened, to their cards. In my, I also have an object containing all the arrays of students for each day, which looked like this:

``` javascript
let week = {
    Monday: monArr,
    Tuesday: tueArr,
    Wednesday: wedArr,
    Thursday: thurArr,
    Friday: friArr
}
```

With this, I was able to do the following:

1. Access a day of the week
2. Access the array of student cards, and access each student
3. If that student is included in the array for that day, add that day to the the student card under the `day` property. 

So, this ended up looking like this:

``` javascript
//  Second Array adds days students attend. 
for (let day in week ) { // First loop goes over each day of the week, and the values that each hold
    studentList.forEach(function(student){ // Second loop goes over every student in the studentList array, and checks if there name is in a day 
        if (week[day].includes(student.name) == true) {
            student.days += (day + " ")
        }
    })
}
```

Within my `forEach` loop, I used the `.includes()` method to quickly figure out if a day had the name of the student selected in the studentList. This was way easier than making figuring out how to make another loop to manually do all this for me. 

Once both loops are done, all I have to do is `console.table()` the result, and I now have exactly the result I wanted. 

The biggest thing I learned while doing this, is that I can have seperate `for()` loops to perform seperate tasks, to have the desired result that I want. I now need to figure out how to implement this into Firebase, in order to finish off my MVP. 

### EDP:

Same as before, still on **Step 2: Research the Problem** when it comes to Firebase, but I'm going to finally step out of that and begin to use it now that I finished **Step 5: Create a Prototype**, and can now move on to **Step 6: Test and Evaluate the Prototype**.  

### Skills:

One skill I had definetly improved on was **Problem Decomposition**, because that is exactly what I did to figure out how to make my second prototype. My thought process (initially) went as follows: 

1. Get student array for each day
2. Go through each day of the week. 
    * IF the student ISNT in the studentList array yet, create their object on the day that is being looked at!
    * IF they student IS in the studentList object array, add the day currently looked at. 

This was a good start, but clearly it wouldn't work as well creating the studentList array first, *then* adding the days in, based on if a student selected in studentList array, could be found in the array of names for each day. Thanks to developing my problem decomposition skills, I was able to figure this out. 

Another skill I have imrpoved has to be **Growth Mindset**, because I took the time to learn a lot more aobut arrays, and while I didn't use everything I learned, all of that helped me to better understand how to rewrite my code from my first prototype. 
### Conclusion: 

One of my biggest conclusions, is that using multiple seperate `for` loops is a great way to manipulate data, because it's easier and efficient. My biggest conclusion though, is that code is something you really have to think outisde the box about. Solutions can be so simple, yet so hard to figure out, but they are usually right there, they just need to be thought about for a little bit. 

[Previous](entry03.md) | [Next](entry05.md)

[Home](../README.md)