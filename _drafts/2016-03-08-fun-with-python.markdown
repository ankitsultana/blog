---
Title: Fun with Python
---

I have recently been reading up on OOP realization in Python, and along the
way I have discovered some really cool concepts that I feel are worth sharing,
and at the same time, need to transcribed somewhere for my own future reference.

### Pre Groundwork

Before starting, I will assume that you know that *everything* in Python is
an object. Be it integers, strings, functions etc. Also I have written this
article assuming that the reader has basic knowledge of Python syntax, and a
rudimentary knowledge of OOP concepts like classes, objects and methods.

### Groundwork

Before beginning with anything, we will need to understand a few things.

#####1. Higher Order Functions et al

A *Higher Order* function is one that can take a function as an argument, or
returns a function.

An *anonymous function* is a function that is not bound to an identifier. It is
also known as function literal.

A *Lambda* in python is a construct that supports the creation of anonymous
functions at runtime.

#####2. Methods vs Functions

A function is a callable object in Python, i.e. it can be called using the *call*
operator `()`. You would generally see them as defined using a `def` or else
in their anonymous form, when they are constructed using a `lambda`.

A method is a special class of function which can either be *bound* or *unbound*
. I will explain it later, don't worry if you don't know what they are.


#####3. First Class Functions/Methods/Objects

According to wikipedia,

> In CS, a programming language is said to have first-class functions if the
> language supports passing functions as arguments to other functions, returning
> them as the values from other functions, and assigning them to variables or
> storing them in data structures.

There is a somewhat debatable criteria, that a language must also support
anonymous functions as well, but we will not delve into that.

As you might have guessed Python supports first class functions. In fact, as
Guido Van Rossum mentioned in his [blog](http://python-history.blogspot.in/2009/02/first-class-everything.html)
all objects in Python are <span class="capsule">First Class</span>. And since
*everything* in Python is an Object, *everything* in Python is first class.

Python also supports the creation of anonymous functions using a construct
called <span class="capsule">lambda</span>. Enough talk, let's start with code samples:

{% highlight python %}
l = [1, 3, 4]
print filter(lambda x: x % 2 == 0, l)
{% endhighlight %}

The code above prints all the elements in `l` that are even. If you don't know,
the `filter` function takes in arguments as `(function, iterable)`. Lambdas are
convenient when you need the features of a function but you only need it
once. Although, real world `lambda` use cases are rare. [^1]

[^1]: [Lambda use cases](http://stackoverflow.com/questions/134626/which-is-more-preferable-to-use-in-python-lambda-functions-or-nested-functions)

To sum this up, in Python you can pass functions as arguments to other functions
, return functions from other functions and assign them to variables. An example
for the latter is:

{% highlight python %}
func = lambda x: x * 2  # func is now a function
func(2)                 # Use it like so!
{% endhighlight %}

**Note:** Above example is only for educational purposes. You shouldn't really
do that. In fact, this is exactly the use case for declaring a function using
`def`, which are essentially syntactic sugar for lambdas.

### Bound/Unbound methods

For the rest of the discussion, assume there is no such thing as
*static methods*. Consider a simple class `Dog` as an example:

{% highlight python %}
class Dog:
    def bark(self):
        print 'Bark Bark'
    def run(self):
        print 'running'
{% endhighlight %}

Say you have an Dog instance, `scoobydoo`.

{% highlight python %}
scoobydoo = Dog()
{% endhighlight %}

Now if you want `scoobydoo` to `bark`, you would call it like so:

{% highlight python %}
scoobydoo.bark()
{% endhighlight %}

This is actually translated to this:

{% highlight python %}
Dog.bark(scoobydoo)
{% endhighlight %}

Can you tell what methods are we calling in the above *two* examples ?
Specifically, try to figure out what are the **method names** in the two
examples above.

The methods in the two examples above are **not** the same. How ? Why ?

Well first of all let's establish the fact that the call operator is used to
call any callable object, and is invoked by appending `()` to the object name.

So we can very well deduce that the method names for the two cases above are
`scoobydoo.bark` and `Dog.bark`.

This is damn important, so I repeat, the method names for the two cases above
are `scoobydoo.bark` and `Dog.bark`

As you might have noticed they are not the same. In fact, they have one pretty
big difference in that the first method is *bound* to the instance `scoobydoo`,
while the second one is not bounded to any instance of `Dog`.

Actually the method, `scoobydoo.bark` is a *bound method* and `Dog.bark` is an
*unbound method*. The first one is *bound* to an instance of the `Dog` class,
while the second is not bound to any instance of `Dog`. So naturally when I need
to call a *unbound method* (remember we are not considering static methods),
I need to provide the instance corresponding to which I want the method to
execute.

> Hence we establish that *unbound methods* can't be called without passing the
> instance as an argument.

Python requires that the instance should be passed as the first argument of the
method.

As for the *bound methods*, the original instance is implicitly stored, so
whenever a bound method is called, it corresponds to the appropriate instance.

Let's see some examples to understand even more:

{% highlight python %}
class Dog:
    def bark(self):
        print '%s is barking' % self.name
    def __init__(self, name):
        self.name = name

scoobydoo = Dog()

scoobydoo.bark()        # scoobydoo.bark -> bound method -> bound to scoobydoo
Dog.bark(scoobydoo)     # Dog.bark       -> unbound method

temp = scoobydoo.bark   # temp -> bound method -> bound to scoobydoo
anothertemp = Dog.bark  # anothertemp -> unbound method

{% endhighlight %}

Practically speaking, you won't notice much difference between a bound method,
a function, a callable object (i.e. an object that implements the `__call__`
operator) or a class constructor. They all look the same. As an example, `len`
is a function while `str` is a type constructor.

In fact, consider the following code:

{% highlight python %}
x = scoobydoo.bark
x()                # x is a bound method, not a function !
{% endhighlight %}

Let's try to use our newly acquired knowledge to solve a problem. Try to figure
out why this code is giving the error shown:
{% highlight python %}
class Foo:
    def __init__(self):
        print 'initialized'
    def bar():
        print 'bar'

Foo().bar()

Traceback (most recent call last):
  File "<stdin>", line 1, in <module>
TypeError: bar() takes no arguments (1 given)
{% endhighlight %}

---

Now let's talk about *static methods*.

One might be tempted to believe that *static methods* are *unbound methods*, but
that is **not** the case. Why you say? Well remember that *unbound methods*
require an instance to be passed as the first argument, *static methods* don't
per se.

**Note:** From Python 3.0, the concept of unbound methods has been removed and
the expression `Dog.bark` returns a plain function [^2]

[^2]: [Guido Van Rossum](http://python-history.blogspot.in/2009/02/first-class-everything.html)

### Namespaces

The Python docs say that Namespaces are a mapping from names to objects. You
must be familiar with scopes. A scope is a textual region in the program.
A namespace is a way to implement scope. Say you have the following function:

{% highlight python %}
def foo():
    x = 0
    print x  # x exists here, in foo's namespace

# x doesn't exist here
print x  # --> ERROR!
{% endhighlight %}

Essentially the Python interpreter uses a Namespace to lookup a certain variable
, which namespace(s) to choose is determined by the scope.

Example of namespaces are the set of built-in names, the global names in a
module and the local names in a function invocation.

Namespaces are created at different moments and have different lifetimes.

For Example: The namespace containing the built-in names is created when the
Python interpreter starts up, and is never deleted.

###### Importance

Knowledge of Namespaces is important to avoid common pitfalls when importing
modules. As you know there are several ways to import a module:

######1. import moduleName

This is generally the best way to import your modules. You can access the
imported module's namespace by prepending the moduleName followed by a dot
before accessing any member of that module. This way you can keep your working
script's global namespace and the imported module's namespace isolated. However,
you cannot have a name in your global namespace that has the same name as the
imported module's namespace.

######2. from module import name

This **imports the name** into your current namespace. So you don't need to
prepend with the imported module's name, and can use the name directly. However,
you can't use the name you imported for something else.

######3. from module import *

This **imports all names** into your current namespace. Generally, this isn't
a good practice since it leads to "namespace pollution".

---

**References:**
