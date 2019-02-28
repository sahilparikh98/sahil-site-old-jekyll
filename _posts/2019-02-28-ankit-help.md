---
layout: post
title: Python does it all in one line
subtitle: This is for you, Ankit
tags: [personal]
comments: true
---

Recently, a friend asked me for help on a Python program where everything needs to be done in one line. Sometimes, this really isn't possible. However, Python is massively powerful in one line, thanks to it basically being a form of pseudocode. Let's take a look at how this works.  

In this problem, we are given a dictionary object that contains strings mapped to another dictionary (nested dictionaries):  
```python
gradebooks = {'business analytics': {'Alice': 95, 'Troy': 92}, 
'Python Programming': {'James': 89, 'Charles': 100, 'Bryn': 69, 'Alice': 100}, 
'R programming': {'Troy': 93, 'James':100, 'Charles':88}}
```
The first issue we have is to give the max score across all the classes. We can use Python's `max()` function for this. However, we're probably going to have to do some fancier stuff on the inside, because the `max()` function needs to take in an iterable that can be compared. Your first idea may be to just do:
```python
max(gradebooks.values()) # this is wrong
```
However, `gradebooks.values()` returns the values, which in this case would be the dictionaries that represent each student and their score for the class. So `gradebooks.values()` would return an array of these dictionaries: 
```python
[{'Alice': 95, 'Troy': 92}, 
{'James': 89, 'Charles': 100, 'Bryn': 69, 'Alice': 100}, 
{'Troy': 93, 'James':100, 'Charles':88}]
```
This can't be compared in the `max()` function. What it needs is items that are comparable. How about numbers? Those seem pretty comparable to me. How do I turn all of that into a set of numbers? And in one line? Are you overwhelmed?   
It's not a huge issue, because Python has really powerful list builders.  
We're going to use Python's list building concept, which allows us to put values into a list based on some other iterable. The list building concept says that this:
```python
l = ['1', '2']
scores = []
for num in l:
  scores.append(l)
```
is equivalent to:
```python
l = ['1', '2']
scores = [num for num in l]
```
It makes sense if you read it backwards. Let's look at the for loop. This is going to go through every value in `l` and call it num. Then, num is appended. So basically, the statement is `[append num for num in list]`. Make sense? You take what you're appending and put it in the front, and then put the for loop afterwards. This is essentially how the list building syntax works. We'll see how similar it is for dicts in a bit.  
Now let's translate this for the first problem, which is getting the max of all the scores. What we want to do, is make a list of the max scores for each course, and then pass that into the `max()` function, and it'll get the max out of the list. How do I build that list? First, let's do it the way we know:
```python
scores = []
for course in gradebooks:
  values = gradebooks[course].values() # gets a list of all the scores for this course
  scores.append(max(values)) # appends the max from that list
```
Great! Now how do we do this in one line? Let's start by reducing the number of lines we already have by not storing the list of all the scores:
```python
scores = []
for course in gradebooks:
  scores.append(max(gradebooks[course].values())) # appends the max from that list
```
Now, this looks very similar to the simple version of this that we did! We want to take what we're appending and put it in the front, and then put the for loop afterwards. We're appending `max(gradebooks[course].values())`, and the for loop is `for course in gradebooks`. It's just that simple:
```python
scores = [max(gradebooks[key].values()) for key in gradebooks]
```
Now, we just pass it into the `max()` function.
```python
max_overall_score = max([max(gradebooks[key].values()) for key in gradebooks])
```
