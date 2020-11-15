---
metadata:
    description: In this problem you have to beat the computer in a guessing game
title: 'Problem #023 - guess the polynomial'
---

In this problem you have to devise a strategy to beat the computer in a "guess the polynomial" game.

===

<script>
    var max_degree = 5;
    var max_coef = 3;
    var poly_times = 0;
    var evaluated_at = [];

    // Generate a random integer between a and b, inclusive.
    randint = function(a, b) {
        return Math.floor(Math.random()*(1+b-a)) + a;
    }

    reset_poly = function() {
        poly_times = 0;
        evaluated_at = [];
        document.getElementById("polyHint").innerHTML = "";
        document.getElementById("polyAt").innerHTML = 0;
    }

    var poly = new Array(max_degree + 1);
    generate_poly = function() {
        reset_poly();
        for (var i = 0; i <= max_degree; ++i) {
            poly[i] = randint(0, max_coef);
        }
    }

    evaluate_poly = function() {
        var a = parseInt(document.getElementById("polyAt").value);
        var value = 0;
        for (var i = 0; i <= max_degree; ++i) {
            value += poly[i]*a**i;
        }
        document.getElementById("polyHint").innerHTML = `The polynomial is ${value} when evaluated at ${a}.`;
        if (-1 === evaluated_at.indexOf(a)) {
            evaluated_at.push(a);
            ++poly_times;
            document.getElementById("polyTimes").innerHTML = poly_times;
        }
    }

    window.onload = generate_poly;
</script>

![]()

### Problem statement

I want you to play a little game with the computer. The computer is going to think of a polynomial with non-negative, integer coefficients.
Let's say $p(n)$ is the secret polynomial the computer is thinking of.

I want you to find out what $p(n)$ is, and the only thing you can do is to ask for the value of $p(n)$ at non-negative integers.
For example, you can ask what $p(49)$ is.
You have to come up with the best strategy possible, that allows you to determine $p(n)$ in the least number of guesses possible.

You can test your strategy with the computer below.
The computer will only think of polynomials with degree at most $3$
and the coefficients will be at most $3$ as well, but that is just to make testing your strategy easier.
The strategy should work for higher degrees and larger coefficients.

With the restrictions for the computer test, we have

$$
p(n) = c_0 + c_1n + c_2n^2 + c_3n^3, 0 \leq c_i \leq 3
$$

!!! Give it a try!

---

<div>
    <br />
    You evaluated the current polynomial for <span id="polyTimes">0</span> different value(s).
    <br />
    <button onclick="generate_poly()">Generate a new polynomial</button>

    <br />

    <label>Ask the computer to evaluate the polynomial at</label> &nbsp; <input id="polyAt" type="number" step="1" min="0" size="6" value="0">. &nbsp; <button onclick="evaluate_poly()">Evaluate</button>

    <p id="polyHint"></p>

    <br>

    Your guess: $p(n) = $
    <input id="c0" type="number" step="1" min="0" max="3" size="1" value="0">
    $+$
    <input id="c1" type="number" step="1" min="0" max="3" size="1" value="0">
    $n + $
    <input id="c2" type="number" step="1" min="0" max="3" size="1" value="0">
    $n^2 + $
    <input id="c3" type="number" step="1" min="0" max="3" size="1" value="0">
    $n^3$
    <br />
</div>

---

If you need any clarification whatsoever, feel free to ask in the comment section below.

### Solution

The solution to this problem will be posted [here][sol] after this problem has been live for 2 weeks. You can also use that link to post your own solution in the comments! Please **do not** post spoilers in the comments here.
<!--You can read the solution [here][sol] to compare with your own solution. You can also use that link to post your own solution in the comments! Please **do not** post spoilers in the comments here.-->

---

If you enjoyed the problem and would like to get new problems directly in your inbox, be sure to [subscribe to the Problems newsletter][subscribe].

[sol]: ../../solutions/{{ page.slug }}
[subscribe]: https://mathspp.com/subscribe
