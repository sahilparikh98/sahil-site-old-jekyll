---
layout: post
title: Python does it all in one line
subtitle: This is for you, Ankit
tags: [personal]
comments: true
---

Recently, a friend asked me for help on a Python program where everything needs to be done in one line. Sometimes, this really isn't possible. However, Python is massively powerful in one line, thanks to it basically being a form of pseudocode. Let's take a look at how this works.  

In this problem, we are given a dictionary object that contains strings mapped to another dictionary:  
```python
gradebooks = {'business analytics': {'Alice': 95, 'Troy': 92}, 
'Python Programming': {'James': 89, 'Charles': 100, 'Bryn': 69, 'Alice': 100}, 
'R programming': {'Troy': 93, 'James':100, 'Charles':88}}
```
The first issue we have is to give the max score across all the classes. We can use Python's `max()` function for this. However, we're probably going to have to do some fancier stuff on the inside, because the `max()` function needs to take in an iterable that can be compared. Your first idea may be to just do:
```python
max(gradebooks.values())
```
However, gradebooks.values() returns the values, which in this case would be the dictionaries that represent each student and their score for the class. So `gradebooks.keys()` would return an array of these dictionaries: 
```python
[{'Alice': 95, 'Troy': 92}, 
{'James': 89, 'Charles': 100, 'Bryn': 69, 'Alice': 100}, 
{'Troy': 93, 'James':100, 'Charles':88}]
```
This can't be compared in the `max()` function. What it needs is items that are comparable. How about numbers? Those seem pretty comparable to me. How do I turn all of that into a set of numbers? And in one line? Are you overwhelmed?   
It's not a huge issue, because Python has really powerful list builders. What we're going to do now is get a list of all the scores, and pass that list into the `max()` function. First let's get the list:
```python
scores = [max(gradebooks[key].values()) for key in gradebooks]
```
This might look a little confusing. We're using Python's list building concept, which allows us give a list values based on some other iterable. The list building concept says that this:
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
It makes sense if you read it backwards. Let's look at the for loop. This is going to go through every value in `l` and call it num. Then, num is appended. So basically, the statement is `[append num for num in list]`. Make sense?
