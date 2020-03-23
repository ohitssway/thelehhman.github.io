---
layout: post
title:  "Some Counting Problems"
date:   2020-03-23
---

While I (and nearly everyone else) am stuck inside my house for social distancing, I wanted to make most of my time by learning new things. Specifically machine learning and some of the basic math behind. I'm in my last semester studying computational statistics and wanted to review some old class material by solving some problems, trying to implement them in Python, and visually show my intuition behind solving these problems.

I'm starting off this quarantine with a series of posts on probability problems. A lot of these problems will be based off of [STAT 414](https://online.stat.psu.edu/stat414/) and [Sheldon Ross's A First Course in Probability](http://julio.staff.ipb.ac.id/files/2015/02/Ross_8th_ed_English.pdf)

Let's start off with some combinatorics problems!

## License Plates

Let's say we have an empty license plate that can be 5 characters long. We want to find out how many 5 character long licenses are possible if the first 2 characters are for uppercase letters (A-Z) and the other 3 are for digits (0-9). 

<p align="center"> 
    <img src="https://raw.githubusercontent.com/ohitssway/ohitssway.github.io/master/_posts/images/license-plates.PNG">
</p>

First, let's solve this assuming we can allow repeats.

I like to think of these problems by looking at how many options are available at each "slot", in this case how many options there are for each spot in the license plate. Let the underscores represent the spots.

<center>__ __ __ __ __</center>

In the first two spots, we can have any two uppercase letters. So there are 26 options for each of the spots. So far we have:

<center>26*26 __ __ __</center>

And in other spots, we can have any digit in each spot. In each spot, there are 10 such options.

<center>26*26*10*10*10</center>

So if we multiply all these numbers we get a final answer of 672,000.

But if we don't allow repeats. We have 26 options for the first slot and then 25 options for the second slot since one letter has been used already. 

<center>26*25 __ __ __</center>

For the third spot there are 10 options, for the fourth spot there are 9 options, and for the fifth spot there are 8 spots.

<center>26*26*10*10*10</center>

For an answer of 468,000 (26 x 25 x 10 x 9 x 8).

Let's try to generate these answers in Python.

```python

import itertools
import random

random.seed()

# with repeats

characters = [chr(x) for x in range(65,91)]    # creates ['A','B','C', ..., 'Z']
digits = [chr(x) for x in range(48,58)]    # creates ['0','1','2',.., '9']

letters = itertools.product(characters, repeat = 2)
nums = itertools.product(digits, repeat = 3)
license_plates = list(itertools.product(letters, nums))

print(len(license_plates))
print(random.choices(license_plates, k=5))

# without repeats

letters = itertools.permutations(characters, 2)
nums = itertools.permutations(digits, 3)
license_plates_two = list(itertools.product(letters, nums))

print(len(license_plates_two))
print(random.choices(license_plates_two, k=5))
```
