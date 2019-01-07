+++
author = "Bowen She"
categories = ["python", "quiz"]
tags = ["python"]
date = "2018-12-29"
description = "Do you know all the frequently used ticks in Python?"
featured = "test-days.png"
featuredalt = "quiz time"
featuredpath = "/img/LeetCode/"
linktitle = ""
title = "Python Quiz 01"
type = "post"
+++

*Bring out a white paper and write all the answers to the quiz on the paper. See if you can finish all of these answers.*

1. How do you create a array which contains 2 - 10 in one-liner?

    <details><summary>CLICK ME</summary>
    <p>

    ```python
    # using list comprehension
    [i for i in range(2, 11)]
    # Or
    list(range(2, 11))
    ```
    </p>
    </details>

2. How do you randomly select 3 numbers from an integer array '''A'''?
    <details><summary></summary>
    <p>

    ```python
    import random
    random.sample(A, 3)
    ```
    </p>
    </details>
3. How do you create a array of length 13 that for index > 4 its element is any random lowercase vowel('a', 'e', 'i', 'o', 'u') but for index in [0, 4], its element is the square root value of the index?
    <details><summary></summary>
    <p>

    ```python
    import random
    # random.sample's return type is a list
    [i**0.5 if i < 5 else random.sample('aeiou', 1)[0] for i in range(13)]
    ```
    </p>
    </details>
4. How do you you heap sort an array A? How do you add a new value into a heap? How do you pop the root value from a heap? How do you add a new number to a min heap with a fixed length?
    <details><summary></summary>
    <p>

    ```python
    import heapq
    heapq.heapify(A)
    heapq.heappush(A, a)
    b = heapq.heappop(A)
    b = heapq.heappushpop(A, a)
    ```
    </p>
    </details>
5. How do you find all the permutations of a string ```s```?
    <details><summary></summary>
    <p>

    ```python
    import itertools
    itertools.permutations(s)
    ```
    </p>
    </details>
6. How do you combine two same-length arrays A and B as a pair array?
    <details><summary></summary>
    <p>

    ```python
    zip(A, B)
    # if A and B is not same length, what's the result?
    ```

    </p>
    </details>
7. Given a key "WTF" and a dictionary d, how do you find the value of the key and if the key doesn't exist in the dict, can you return "" instead?(one-liner)
    <details><summary></summary>
    <p>

    ```python
    d.get("WTF", "")
    ```
    </p>
    </details>

8. How do you replace all the "is" to "si" in string "isawakiss"?
    <details><summary></summary>
    <p>

    ```python
    "isawakiss".replace("is", "si")
    ```
    </p>
    </details>
9. How do you replace all the vowels in a string to ```'_'```?(regex)
    <details><summary></summary>
    <p>

    ```python
    import re
    re.sub("[aeiou]", "_", s)
    ```
    </p>
    </details>
10. lowercase and uppercase of the string ```s```?
    <details><summary></summary>
    <p>

    ```python
    s.lower()
    s.upper()
    # print the alphabet
    import string
    string.ascii_letters
    string.ascii_lowercase
    ```
    </p>
    </details>
11. convert all the elements in string array ```S``` into the form specified in question 9, and combine the result string array into one huge string?
    <details><summary></summary>
    <p>

    ```python
    ''.join([re.sub('[aeiou]', '_', s) for s in S])
    ```
    </p>
    </details>

12. how do you convert base-2 binary number string to int?
    <details><summary></summary>
    <p>

    ```python
    int("10001", 2)
    ```
    </p>
    </details>
13. how do you find the binary expression of a 10-base number?
    <details><summary></summary>
    <p>

    ```python
    bin(23)[2:]
    ```
    </p>
    </details>
14. Do you know how to do string formatting in python?
For example, given a list A, can you print something like "hey, look. This is a list: ####?" "####" represents the contents in the list.
    <details><summary></summary>
    <p>

    ```python
    "hey, look. This is a list: %s" % A
    "hey, look. This is a number: %d" % 23
    "hey, look. This is a string: %s" % "WTF"
    "hey, look. This is a float number: %f " % 3.14
    ```
    </p>
    </details>
15. What is the output of the following program?
```Python
names = "{1}, {2} and {0}".format('John', 'Bill', 'Sean')
print(names)
```
  <details><summary></summary>
  <p>
  ```shell
  Bill, Sean and John
  ```
  </p>
  </details>

16. How to print the clock time in this format "XX:XX:XX" given the total seconds ```s```? (one-liner)
    <details><summary></summary>
    <p>
    ```python
    "{:02d}:{:02d}:{:02d}".format(secs // 3600, *divmod(secs % 3600, 60))
    # print the clock time
    import time
    time.strttime('%H : %M : %S')
    time.strttime('%I : %M : %S %p')
    ```
    </p>
    </details>

17. What is the built-in functions to convert between ASCII numbers and characters?
    <details><summary></summary>
    <p>
    ```python
    ord('s')
    chr(65)

    ```
    </p>
    </details>
18.  How do you determine if a character is a digit or not, is a letter or not?
    <details><summary></summary>
    <p>
    ```python
    's'.isdigit()
    's'.isalpha()

    ```
    </p>
    </details>
