# Copilot my savior

## Challenge

Copilot is great! Look at this great encryption function it wrote for me

![Copilot my savior](/challenge-sources/copilot/thanks_copilot.png)

- [encrypt.py](/challenge-sources/copilot/encrypt.py)
- [flag.txt.enc](/challenge-sources/copilot/flag.txt.enc)

## Getting started
To solve this challenge you'll have to do some byte manipulations in python. If you haven't written python before, don't worry! Python is notoriously simple and easy to pick up, granted that you've written in an imperative language before.

1. If you haven't set up a programming environment with python installed, start [here](/resources/env_setup.html)
2. To get started with some byte manipulations in python, read [this](resources/python_tricks.html)

All in all this challenge is really straightforward, the main goal is to get comfortable with python and doing byte manipulations

## Ok but how do I solve this thing???

You're given a program that takes a secret file (`flag.txt`) and "encrypts" it, changing it to something that is unreadable (`flag.txt.enc`). Your goal is to reverse this process 

Some advice then:
1. Look carefully at `encrypt.py`. What information do we not know? What does the `encrypt` function do? What could you do to undo it's effects if you knew the `???` value? 
2. What happens if you XOR a byte by the same byte twice?
3. Think about the `???` value. What are the possible values that it could be? Could you try to guess it? How many guesses would you need to make? How would you know if your guess was correct?