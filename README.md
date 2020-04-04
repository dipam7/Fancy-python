# Fancy-python
This repo is based on my article [How to be fancy with Python](https://towardsdatascience.com/how-to-be-fancy-with-python-8e4c53f47789). It includes small Python tricks that will make your life much much easier. I hope they also help you become a better Python programmer. It is available as a [jupyter notebook](https://github.com/dipam7/Fancy-python/blob/master/fancy_python_github.ipynb) so you can clone and run it yourself. I also post these [small tricks on Linkedin](https://www.linkedin.com/posts/dvasani_python-oneabrssabrpython-activity-6652115242383966208-iYG2) with [my own hashtag](https://www.linkedin.com/feed/hashtag/?highlightedUpdateUrns=urn%3Ali%3Aactivity%3A6652115242383966208&keywords=%23one_ss_python&originTrackingId=BFp0%2B8VATZyjB2sqJjeD%2Bw%3D%3D) so make sure to follow me there. Also, if you know some tricks of your own, submit a pull request and I'll be more than happy to include it.

**Table of contents**:
- [Keyboard shortcuts](#ks)
- [Zip, enumerate](#ze)
- [Comprehensions](#c)
  * [Lists](#l)
  * [extra: operator.itemgetter()](#oi)
  * [Dictionaries](#di)
- [Star operator ](#star)
- [Partials](#par)
- [Asserts](#ass)
- [Pathlib and os.walk](#pat)
- [Generators](#gen)
- [dir, isinstance, hasattr](#dih)
- [Pipe](#pipe)
- [Cleaner constructor](#cons)
- [All, Any](#aany)
- [Multiple assignment](#ma)
- [Callable](#ca)
- [Faster membership checking](#fmc)
- [Advanced tricks](#advt)
  * [2 loops in one line](#2l)
  * [Flatten lists](#ft)
  * [defaultdicts instead of dicts](#dd)
  * [making delegation work](#deleg)
  * [__ all __ for better imports](#all)
  
- [Conclusion and further reading](#con)


Things to include:
posts from linkedin

<a name='ks'></a>
### -1. Keyboard shortcuts

`TAB` to indent code

`SHIFT + TAB` to unindent code

To comment a bunch of code, select it and press `CONTROL + /`

To surround something with quotation marks or brackets around something, press `SHIFT + "` or `SHIFT + (`

<a name='ze'></a>
### 0. Zip, enumerate

Usually in Python, we loop over things like this:

![Comprehensions 1](https://github.com/dipam7/Fancy-python/blob/master/images/comprehensions_1.png)

To do the same with multiple lists, use zip

![Comprehensions 2](https://github.com/dipam7/Fancy-python/blob/master/images/comprehensions_2.png)

And if you need indexes by any chance you can just do

![Comprehensions 3](https://github.com/dipam7/Fancy-python/blob/master/images/comprehensions_3.png)

<a name='c'></a>
### 1. Comprehensions

<a name='l'></a>
#### Lists

The best part about Python is that you can accomplish so much in so less code. Take list comprehensions for example. If you want to create a list of numbers in a certain range you can easily do it as follows:

![Comprehensions 4](https://github.com/dipam7/Fancy-python/blob/master/images/comprehensions_4.png)


You can also apply conditions on it very easily.


![Comprehensions 5](https://github.com/dipam7/Fancy-python/blob/master/images/comprehensions_5.png)

One practical example of this is to convert a number to its digits.

![Comprehensions_6](https://github.com/dipam7/Fancy-python/blob/master/images/comprehensions_6.png)

This concept of applying a function to every element of the list reminds me of map

![Comprehensions_7](https://github.com/dipam7/Fancy-python/blob/master/images/comprehensions_7.png)

Just like lists, there are comprehensions for dictionaries and generators as well. We'll talk about generators later.

<a name='oi'></a>
#### operator.itemgetter

Let's start with dictionaries. First let's learn about something called `operator.itemgetter`. It retreives every element of the specified index.

Say you have a list of lists like this

![Dict_comp_1](https://github.com/dipam7/Fancy-python/blob/master/images/dict_comp_1.png)

and you want to get the first element of every inner list. You can do so as follows

![Dict_comp_2](https://github.com/dipam7/Fancy-python/blob/master/images/dict_comp_2.png)

Cool right?

Let me give you one more example. You can use it with the `key` argument in the sorted function.

![Dict_comp_3](https://github.com/dipam7/Fancy-python/blob/master/images/dict_comp_3.png)

See how it works?

<a name = 'di'></a>
#### Dictionaries

Okay back to dictionaries. A basic dictionary comprehension would be to map every element to an index.

![Dict_comp_4](https://github.com/dipam7/Fancy-python/blob/master/images/dict_comp_4.png)

A good practice for such dictionaries is to also create the reverse mapping. Trust me, you'll need it later.

![Dict_comp_5](https://github.com/dipam7/Fancy-python/blob/master/images/dict_comp_5.png)

We want to be able to do grouping in dictionaries like this:

![Dict_comp_6](https://github.com/dipam7/Fancy-python/blob/master/images/dict_comp_6.png)

Let's break that down. The first thing we need to do for this to work is sorting by grade

![Dict_comp_7](https://github.com/dipam7/Fancy-python/blob/master/images/dict_comp_7.png)

Then we can use itertools to group them

![Dict_comp_8](https://github.com/dipam7/Fancy-python/blob/master/images/dict_comp_8.png)

And finally create a comprehension in the format we need by choosing just the 0th element from every tuple, in this case, student name

![Dict_comp_9](https://github.com/dipam7/Fancy-python/blob/master/images/dict_comp_9.png)

Go over that one more time to make sure you understand it.

<a name = 'star'></a>
### 2. * operator

I bet those comprehensions were a lot to take in. Let's move onto lighter stuff for a while

The * operator can be used to repeat strings. For example

![Star_1](https://github.com/dipam7/Fancy-python/blob/master/images/star_1.png)

Now you probably don’t want to print “Python is cool” a whole lot of times but you should use it for something like this

![Star_2](https://github.com/dipam7/Fancy-python/blob/master/images/star_2.png)

The * operator can also be used to unpack iterables like lists

![Star_3](https://github.com/dipam7/Fancy-python/blob/master/images/star_3.png)

We can also use it with function arguments when we don't know the number of arguments in advance

![Star_4](https://github.com/dipam7/Fancy-python/blob/master/images/star_4.png)

`*args` is used for variable number of arguments and `**kwargs` is used for named arguments

<a name = 'par'></a>
### 3. Partials

Something else you can do with functions is create partial functions. What are they? 

Suppose we have a function to calculate simple interest. We can set default values for some parameters (from right to left).

![Partial_1](https://github.com/dipam7/Fancy-python/blob/master/images/partial_1.png)

However, we cannot set the default value of just **p** in this way.

We can do so using a partial function. In a partial function, we set default values for some arguments, left to right and then use that as a function. Let’s set a default value for just **p**.


![Partial_2](https://github.com/dipam7/Fancy-python/blob/master/images/partial_2.png)

Although partials work from left to right, we can also skip parameters in between by using named arguments.

![Partial_3](https://github.com/dipam7/Fancy-python/blob/master/images/partial_3.png)

Partials are mainly used when you want to fix a few parameters and experiment with the rest.

<a name = 'ass'></a>
### 4. Asserts

Test driven development means you write tests and then you write code to pass those tests. You can write mini-tests in Python using **assert**. 

For example, you might want to make sure the shape of a certain object is what you expect it to be.

![Assert_1](https://github.com/dipam7/Fancy-python/blob/master/images/assert_1.png)

You can also write a custom error message after a comma. Writing these mini-tests will be super helpful in making sure parts of your code work as expected. It will also help you debug things efficiently.

<a name = 'pat'></a>
### 5. Pathlib

If you haven't already stopped using strings for paths, stop right now!

![pathlib_1](https://github.com/dipam7/Fancy-python/blob/master/images/pathlib_1.png)

Check out [this article for more examples and explanations](https://medium.com/swlh/five-most-useful-pathlib-operations-77f9c96790b3).

Having said that, os.walk is a really fast way of traversing a directory recursively. 

![pathlib_2](https://github.com/dipam7/Fancy-python/blob/master/images/pathlib_2.jpeg)

<a name = 'gen'></a>
### 6. Generators

We can use the yield keyword instead of return keyword in Python to create a generator. The advantage of using a generator is that is generates things on the fly and forgets them. This saves memory.

![gen_1](https://github.com/dipam7/Fancy-python/blob/master/images/gen_1.png)

We can also create them using comprehensions

![gen_2](https://github.com/dipam7/Fancy-python/blob/master/images/gen_2.png)

Proof that you can iterate over generators only once.

![gen_3](https://github.com/dipam7/Fancy-python/blob/master/images/gen_3.png)

To search for 5 in nums it had to generate numbers from 0 to 5. Now it starts from 6.

<a name = 'dih'></a>
### 7. dir, isinstance and hasattr

If we want to know all the attributes and methods related to a particular object, we can use `dir()`

![dir_1](https://github.com/dipam7/Fancy-python/blob/master/images/dir_1.png)

We can also check for attributes directly using `hasattr`

![dir_2](https://github.com/dipam7/Fancy-python/blob/master/images/dir_2.png)

And we can check the type of a variable using isinstance. This is usually done to ensure the parameter passed to a function is of the correct type.

<a name = 'pipe'></a>
### 8. Pipe instead of function chaining.

If you want to run a bunch of functions through every element in your data, chaining them can get clunky. And writing multiple funciton calls everytime is not efficient. For this you can create a pipeline with inner functions.

![pipe_1](https://github.com/dipam7/Fancy-python/blob/master/images/pipe_1.jpeg)

<a name = 'cons'></a>
### 9. Cleaner constructor

When we define classes in python we write a lot of `self.something = something`. If our class takes a lot of parameters, this can soon become clunky. And it is also boring to type. We can very easily write a function to do this for us and call it inside our __init__.

![con_1](https://github.com/dipam7/Fancy-python/blob/master/images/con_1.jpeg)

<a name = 'aany'></a>
### 10. All, any

You can use these if you want to test something on all or any values of an iterable.

![aany](https://github.com/dipam7/Fancy-python/blob/master/images/all_any.png)

<a name = 'ma'></a>
### 11. Multiple assignment

You can assign the same value to multiple variables in Python as follows.

![test](https://github.com/dipam7/Fancy-python/blob/master/images/multiple_assignment.png)

<a name = 'ca'></a>
### 12. Callable

You can check if an object is callable in python using the **callable** keyword.

![test](https://github.com/dipam7/Fancy-python/blob/master/images/callable.png)

<a name = 'fmc'></a>
### 13. Faster Membership Checking
Membership checking in Python lists is a linear operation. You can use a set instead to make it faster. Set's are implemented as hash maps and will give you constant time. 

![test](https://github.com/dipam7/Fancy-python/blob/master/images/mem_check.png)


<a name = 'advt'></a>
### 13. Advanced tricks

<a name = '2l'></a>
#### 2 loops in one line

You can use Python's itertools library to write nested for loops in one line

![test](https://github.com/dipam7/Fancy-python/blob/master/images/2loops.png)

<a name = 'ft'></a>
#### Flatten lists

You can flatten lists in Python using sum(). You can also do this recursively 

![test](https://github.com/dipam7/Fancy-python/blob/master/images/flatten_lists.png)

<a name = 'dd'></a>
#### defaultdict

When you create a dictionary in Python, you might be using an if statement to check if a key is present. If it's not, you set a default value for that key, otherwise, you do something else. You can do the same using the .setdefault() method available with dictionaries in Python. However, an even cleaner way to do this is to use defaultdicts. Check out this example and then read the [documentation](https://docs.python.org/3/library/collections.html#collections.defaultdict)

![test](https://github.com/dipam7/Fancy-python/blob/master/images/defaultdicts.png)

<a name = 'deleg'></a>
#### Delegation in Python

When an inherited class has * args or ** kwargs in its constructor, we want to replace those arguments with the arguments of the class it inherits from when showing the doc page or the help page. This is not the default behavior in Python. You can use the delegates function from [this article](https://lnkd.in/g3V95t3) to do so.

![test](https://github.com/dipam7/Fancy-python/blob/master/images/delegation.png)

<a name = 'all'></a>
#### Dunder all for better imports

We are not advised to use from library import * because it can import a lot of unnecessary things. To avoid this, when writing a library, we can define __ all __. Then, only the things contained in __ all __ will be exported.

![test](https://github.com/dipam7/Fancy-python/blob/master/images/all_imports.png)

<a name = 'con'></a>
### Conclusion and further reading

Those were some Python tricks that I believe would help everyone. Herea are some more links to keep you busy. Keep learning.

- [A walkthru on writing better functions in Python](https://towardsdatascience.com/a-walkthru-for-writing-better-functions-6cb37f2fa58c)
- [Upgrading python lists](https://towardsdatascience.com/upgrading-python-lists-35440096ec36)
- [How to be fancy with OOP in Python](https://towardsdatascience.com/how-to-be-fancy-with-python-part-2-70fab0a3e492)
- [Some neat Jupyter tricks](https://medium.com/swlh/some-neat-jupyter-tricks-be0775c3f17).
- [Primer on Python decorators](https://realpython.com/primer-on-python-decorators/#decorating-classes)
- [Primer on meta-classes in Python](https://jakevdp.github.io/blog/2012/12/01/a-primer-on-python-metaclasses/)

### References:

These things are referred from various sources but quite a few of them are referred from [fastai walkthrus](https://www.youtube.com/watch?v=44pe47sB4BI&list=PLJ3bz91D0hbrDaPFoN0dor0keyKnmvPqy)
