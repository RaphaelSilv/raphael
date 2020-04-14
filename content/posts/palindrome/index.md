---
title: "C++ practice | Searching for atomic palindromes in any given file"
date: 2020-04-11T00:04:28-03:00
description: ""
categories: [c++, algorithms]
dropCap: true
displayInMenu: false
displayInList: true
draft: false
resources:
- name: featuredImage
  src: "woodtype.jpg"
  params:
    description: "A woodytpe printing font. I would say, different shapes of letters carved on wood."
---
<h5 style="color: gray" align="center"><a style="color: gray" href="https://pixabay.com/images/search/word/"><u>Pixabay</u><a/></h5>
<h2 style="color: black;"><i>"The best is the enemy of the good."</i></h2>
<h4 style="color: gray;">Voltaire</h4>

## [palindrome-hunter](https://github.com/RaphaelSilv/palindrome-hunter)
The best way to learn something new is arguably controversial, but nobody can
honestly disagree that by doing and through repetition is one of the most effectives ways
to achieve such objective!

Expose yourself to information through reading is good, but wouldn't be enough to retrieve
information in the long term memory.

That said, build
[palindrome-hunter](https://github.com/RaphaelSilv/palindrome-hunter) was
my way to develop a better understanding of *c++* and *core programming concepts*.

# What is a palindrome?

> A palindrome is a word, number, phrase, or other sequence of characters which reads the same backward as forward.
<h5 style="color: gray" align="left"><a style="color: gray" href="https://en.wikipedia.org/wiki/Palindrome"><u>Wikipedia</u><a/></h5>

### But, what is an atomic palindrome?
Here goes a practical example:

```sh
Atomic palindrome example: "civic"

!Atomic palindrome example: "A nut for a jar of tuna"
```

### Hey, permuted what?

A permutation is a rearrangement of characters which make possible *"aab"* becomes the palindrome: *"aba"*.
Every palindrome is also a permuted palindrome, but the opposite isn't true.

### Runnin' it
In the main function specify the `txt` file name properly placed at `artifacts` folder
when instantiate a *palindrome* object like so:

```cpp
#include "src/palindrome.h"

int main(int argc, char const *argv[]) {

  Palindrome palindrome = { "the-tragedy-of-hamlet-by-w-shakspeare.txt" };
  palindrome.readWordsFromFile();
}
```

> *"Run Forest, run!"*
<h5 style="color: gray;">Forrest Gump (1994)</h5>


```c++
g++ src/palindrome.cpp main.cpp -o <output file name>
```

The expected output:
```cpp
did is The Permuted Palindrome 435
too is The Permuted Palindrome 436
bee is The Permuted Palindrome 437
offendendo is The Permuted Palindrome 438
bee is The Permuted Palindrome 439
hee is The Permuted Palindrome 440
```

# Implementation details
## Public interface

Besides the main function `void Palindrome::readWordsFromFile()` the Palindrome
object provides facilities implemented to make it's functionality possible.
They are:

```cpp
class Palindrome {
public:
  class Exception {};
  Palindrome(std::string);
  void removeSpecialCharsFromString(std::string&);
  void readWordsFromFile();
  bool isPalindrome(std::string);
  bool isPermutedPalindrome(std::string);
  void toLowerCase(std::string&);
  inline int getNumPalindromes() {
    return numPalindromes;
}
 inline int getNumPermutedPalindromes() {
    return numPermutedPalindromes;
  }

  ~Palindrome();

```
## Algorithms

I will cover the most challenging function it is:

```cpp
bool isPermutedPalindrome(std::string str);
```

Probably the most known method to find a palindrome permutation is through brute
force. It consists of generate every possible permutation and check if it is a palindrome or not.
But it is not the most effective solution. Usually this algorithm requires
`recursion` and you should know how expensive it is. Use it only when you have to.

The way I chose to solve that problem was by first:
* identifying the palindrome properties:

`if` a given word is composed by a odd number o characters each one of them `minus 1` must occur a even number of time;
     for instance: `madam -> [m,m] + [a,a] minus [d]`

`else if` the given word is composed by an even number of characters each one of them must to occur a even number of time;
     for instance: `noon` -> `[n.n]` + `[o,o]`

 Remember *"Every permuted palindrome is a palindrome."*

* Put it into code!

For that I rely on c++ container <a href="http://www.cplusplus.com/reference/set/set/"><code>set</code></a>.
Fortunately, this type of container only allows unique elements in it.
Well, the rest of the job was easy-peasy.
Given a `str` string I verify the number of characters it has. If it's an odd number we know the *" even number of repeated characters minus 1;"* rule.

We can use a flag variable `charRemaining` to help us store this information:

```cpp
  if (str.length() % 2 == 0) {
    charRemaining = 0;
  } else {
    charRemaining = 1;
  }
```

 Iterating `str`:

```cpp

 std::set<char> mySet;

 ...

  for (size_t i = 0; i < str.length(); i++) {
    if (!mySet.insert(str.at(i)).second) {
      mySet.erase(str.at(i));
    }
  }
```

For each character in `str` I call `insert` and with `second` I verify if the element already exists.
Simple logic:

`if` the element do not exists yet, insert it.
`else if` it already exists remove it's occurrence with `erase`.

The return type is a boolean statement with simple comparison:

```cpp
  return charRemaining == mySet.size();
```

That's all folks, hope you have enjoyed. Take care.

# References:

* Programming Principles and Practice Using C++ 2 ed.- by Bjarne Stroustrup.
