# tasks

Здесь будут добаляться задачи с решением с различных платформ

//leetcode 2629. Function Composition

Given an array of functions [f1, f2, f3, ..., fn], return a new function fn that is the function composition of the array of functions.

The function composition of [f(x), g(x), h(x)] is fn(x) = f(g(h(x))).

The function composition of an empty list of functions is the identity function f(x) = x.

You may assume each function in the array accepts one integer as input and returns one integer as output.

 

Example 1:

Input: functions = [x => x + 1, x => x * x, x => 2 * x], x = 4
Output: 65
Explanation:
Evaluating from right to left ...
Starting with x = 4.
2 * (4) = 8
(8) * (8) = 64
(64) + 1 = 65
Example 2:

Input: functions = [x => 10 * x, x => 10 * x, x => 10 * x], x = 1
Output: 1000
Explanation:
Evaluating from right to left ...
10 * (1) = 10
10 * (10) = 100
10 * (100) = 1000
Example 3:

Input: functions = [], x = 42
Output: 42
Explanation:
The composition of zero functions is the identity function

Constraints:

-1000 <= x <= 1000
0 <= functions.length <= 1000
all functions accept and return a single integer

// Solution

/**
 * @param {Function[]} functions
 * @return {Function}
 */
var compose = function (functions) {
    let i = functions.length
    return function (x) {
        if (i < 1) return x
        let newX = functions[functions.length-1](x)
        let newFunctions = functions.splice(0, functions.length - 1);
        const func = compose(newFunctions)
        return func(newX)
    }
};

/**
 * const fn = compose([x => x + 1, x => 2 * x])
 * fn(4) // 9
 */

 // leetcode 2703. Return Length of Arguments Passed

 Write a function argumentsLength that returns the count of arguments passed to it.
 

Example 1:

Input: args = [5]
Output: 1
Explanation:
argumentsLength(5); // 1

One value was passed to the function so it should return 1.
Example 2:

Input: args = [{}, null, "3"]
Output: 3
Explanation: 
argumentsLength({}, null, "3"); // 3

Three values were passed to the function so it should return 3.

//Solution

/**
 * @param {...(null|boolean|number|string|Array|Object)} args
 * @return {number}
 */
var argumentsLength = function(...args) {
    return Array.from(args).length
};

// leetcode 2666. Allow One Function Call
Easy
Companies
Given a function fn, return a new function that is identical to the original function except that it ensures fn is called at most once.

The first time the returned function is called, it should return the same result as fn.
Every subsequent time it is called, it should return undefined.
 

Example 1:

Input: fn = (a,b,c) => (a + b + c), calls = [[1,2,3],[2,3,6]]
Output: [{"calls":1,"value":6}]
Explanation:
const onceFn = once(fn);
onceFn(1, 2, 3); // 6
onceFn(2, 3, 6); // undefined, fn was not called
Example 2:

Input: fn = (a,b,c) => (a * b * c), calls = [[5,7,4],[2,3,6],[4,6,8]]
Output: [{"calls":1,"value":140}]
Explanation:
const onceFn = once(fn);
onceFn(5, 7, 4); // 140
onceFn(2, 3, 6); // undefined, fn was not called
onceFn(4, 6, 8); // undefined, fn was not called
 

Constraints:

calls is a valid JSON array
1 <= calls.length <= 10
1 <= calls[i].length <= 100
2 <= JSON.stringify(calls).length <= 1000

// solution

/**
 * @param {Function} fn
 * @return {Function}
 */
var once = function(fn) {
    let flag = false
    return function(...args){
        if (flag) return undefined
        flag = true
        return fn(...args)
    }
};

/**
 * let fn = (a,b,c) => (a + b + c)
 * let onceFn = once(fn)
 *
 * onceFn(1,2,3); // 6
 * onceFn(2,3,6); // returns undefined without calling fn
 */

