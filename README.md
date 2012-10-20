![Probability.js Logo](https://github.com/fschaefer/Probability.js/raw/master/misc/Probability.js.png)

# What is it?

Probability.js makes it easy to call JavaScript functions by probability in
Node.js and the browser.

## Why?

Circumstances are rare that you need to call functions by a certain probability
in your daily work. But sometimes, especially in game development and in
statistical applications, it's very handy to have an easy way of doing so.
This library is inspired by [this](http://stackoverflow.com/questions/3983660/probability-in-javascript-help)
question on stackoverflow.com.

## Overview

### Probabilitilized functions

A `probabilitilized function` are several functions combined to one function by
`probability objects`. It is created by calling the constructor `Probability()` 
with `probability objects` as arguments:

    var probabilitilized = new Probability(probabilityObject, probabilityObject /* , ... */);

or with an array of `probability objects`:

    var probabilitilized = new Probability([probabilityObject, probabilityObject /* , ... */]);

### Probability objects

A `probability object` consists of an object with the properties `p` and `f`.
`p` is the probability by that the function `f` is called when the
`probabilitilized function` is invoked.

The value of the probability `p` have to be a string with an integer value
suffixed with `%` between 0 and 100 or preferred a float lesser than or equal to
1.0. `f` is an ordinary JavaScript function:

    var probabilityObject = {
        p: '50%',
        f: function () {}
    };
    
    /* or */
    
    var probabilityObject = {
        p: 0.5,
        f: function () {}
    };

The sum of all probabilities `p` must be lesser or equal to `100%` or, respectively,
`1.0`. Otherwise a `TypeError` is thrown. That's also the case for malformed
`probabilityObjects`.

## Usage example

    /* a counter to show the number of function calls */
    var counter = {
        0: 0,
        1: 0,
        2: 0
    };
    
    /* create a "probabilitilized function" by invoking Probability() with 3 "probability objects" */
    var probabilitilized = new Probability({
        p: '30%',                                         /* the probability by that ... */
        f: function () {                                  /* ... this function is called */
            counter[0]++;
        }
    }, {
        p: '10%',
        f: function () {
            counter[1]++;
        }
    }, {
        p: '60%',
        f: function () {
            counter[2]++;
        }
    });
    
    /* call the probabilitilized functions 100 times */
    for (var i = 0; i < 100; i++) {
        probabilitilized();
    }
    
    /* show that every function is called by its probability */
    console.log(counter); // => {"0":27,"1":11,"2":62}

