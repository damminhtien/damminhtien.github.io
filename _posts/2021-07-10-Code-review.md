---
title: Question for code review
tags: programming clean-code workflow
---

@Author: damminhtien :whale:

@LastUpdate: 10/07/2021

### Questions to ask yourself when conducting a code review

Let's look over some of the questions we might ask ourselves while reviewing code. 

1. Is the code clean and modular?
  + Can I understand the code easily?
  + Does it use meaningful names and whitespace?
  + Is there duplicated code?
  + Can I provide another layer of abstraction?
  + Is each function and module necessary?
  + Is each function or module too long?

2. Is the code efficient?
  + Are there loops or other steps I can vectorize?
  + Can I use better data structures to optimize any steps?
  + Can I shorten the number of calculations needed for any steps?
  + Can I use generators or multiprocessing to optimize any steps?

3. Is the documentation effective?
  + Are inline comments concise and meaningful?
  + Is there complex code that's missing documentation?
  + Do functions use effective docstrings?
  + Is the necessary project documentation provided?

4. Is the code well tested?
  + Does the code high test coverage?
  + Do tests check for interesting cases?
  + Are the tests readable?
  + Can the tests be made more efficient?

5. Is the logging effective?
  + Are log messages clear, concise, and professional?
  + Do they include all relevant and useful information?
  + Do they use the appropriate logging level?

Source: AWS Machine Learning Foundations Nanodegree Program
