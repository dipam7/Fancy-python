# Fancy-python
This repo is based on my article [How to be fancy with Python](https://towardsdatascience.com/how-to-be-fancy-with-python-8e4c53f47789). It includes small Python tricks that will make your life much much easier. I hope they also help you become a better Python programmer. It is available as a jupyter notebook so you can clone and run it yourself. Also, if you know some tricks of your own, submit a pull request and I'll be more than happy to include it.

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
- [Pathlib](#pat)
- [Generators](#gen)
- [dir, isinstance, hasattr](#dih)
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

<a name = 'con'></a>
### Conclusion and further reading

Those were some Python tricks that I believe would help everyone. Herea are some more links to keep you busy. Keep learning.

[Upgrading python lists](https://towardsdatascience.com/upgrading-python-lists-35440096ec36)

[How to be fancy with OOP in Python](https://towardsdatascience.com/how-to-be-fancy-with-python-part-2-70fab0a3e492)

[Some neat Jupyter tricks](https://medium.com/swlh/some-neat-jupyter-tricks-be0775c3f17).

[Primer on Python decorators](https://realpython.com/primer-on-python-decorators/#decorating-classes)

[Primer on meta-classes in Python](https://jakevdp.github.io/blog/2012/12/01/a-primer-on-python-metaclasses/)

### References:

These things are referred from various sources but quite a few of them are referred from [fastai walkthrus](https://www.youtube.com/watch?v=44pe47sB4BI&list=PLJ3bz91D0hbrDaPFoN0dor0keyKnmvPqy)
