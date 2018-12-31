+++
author = "Bowen She"
categories = ["Writing Solid Code", "Defensive Programming"]
tags = ["assertions", "exceptions"]
date = "2018-12-14"
description = "Thoughts about Chapter 2 Assert yourself from book Writing Solid Code"
featured = "Protecting-from-invalid-input-05.jpg"
featuredalt = "funny meme"
featuredpath = "/img/writing-solid-code/CH2-assert-yourself/"
linktitle = ""
title = "Assert yourself"
type = "post"

+++

# Defensive Programming -- Using assertions and exceptions correctly

## what is Defensive programming?

Defensive programming is like defensive driving, which means you are never sure what other driviers will do.
The mindset behind it is that you expect incorrect situations and handle it correctly.

## What to handle correctly?

Unusual execution flow, unusual situations, invalid input and state

## Protecting from invalid input
![](/img/writing-solid-code/CH2-assert-yourself/Protecting-from-invalid-input-01.png)
The principle should be **"garbage in, exception out"** instead of "garbage in, garbage out". You should expect your program will never produce irresponsible output. If invalid input is passed, your system should catch it and alert the user in sort of a way. In such a saying, your system should be thoughtful to provide a mechanism of protection from invalid inputs. One of the methods is **"Data Validation"**, i.e, you can write code to check all possible values of data from external sources, from user, file, DB, Internet, etc. and decide what to do if a bad input is detected. I'll give you a few examples:

- Return a neutral value, e.g, ```null``` or ```undefined```(JS/PHP)
- Substitute with valid data, e.g. ```"Hi".substring(5, -3```) -> ```""```(JS)
- Throw an exception, e.g, ```throw new ArgumentException(...)```
- Show an error message, e.g. pop up an alert window or balloon in the UI
- Log the error message and stop the script, e.g. Spark worker node crashed

## Assertions

Definition from Wiki:

> In computer programming, an **assertion** is a statement that a predicate (Boolean-valued function, i.e. a true–false expression) is always true at that point in code execution. It can help a programmer read the code, help a compiler compile it, or help the program detect its own defects.

Assertions check preconditions and postconditions to ensure that the program can alert developers or users to the unusual bugs. Use asertions for conditions that should never occur in practice. **Failed assertion indicates a fatal error in the program which is usually unrecoverable**. Also, we use assertions to **document assumptions(preconditions & postconditions) in the code**. For example:

```js
private Student GetRegisteredStudent(int id)
{
    Debug.Assert(id > 0); //precondition check
    Student student = registeredStudent[id];
    Debug.Assert(student.isRegistered); //postconditions check
}
```

Usually, assertions are used during development and removed in the release builds but now more and more releases contain assetion codes to give the users a hint of what could go wrong from the assertions if bugs occur.

Another thing about assertions should be noticed is that you should avoid putting executable code in assertions.

```js
Debug.Assert(performActions(), "Could not perform actions!");
```

because ```performActions()``` will not be invoked in production. Instead, better use:

```js
bool actionsPerformed = performActions() //explicitly put the result of an execution into a variable
Debug.Assert(actionPerformed, "Could not perform actions!");
```

## Exceptions

Exceptions provide a way to inform the caller about an error or exceptional events
(which can be totally expected).

In many languages, we use the **try-catch** statement to handle exceptions

<img src="/img/writing-solid-code/CH2-assert-yourself/Protecting-from-invalid-input-04.jpg" alt="" width="400"/>

Remember:

- Throw an exception only for conditions that are **truly exceptional**.
- Use descriptive error messages
- Always include the exception cause when throwing a new exception
- Catch only exceptions you are capable to process correctly(Do not catch all exceptions)
- Have an exception handling strategy for all unexpected / unhandled exceptions
  1. Consider logging
  2. Display to the end users only messages that they could understand

*Question*:

should I throw an exception when I check for username and password?

## Assertions vs. Exceptions
![](/img/writing-solid-code/CH2-assert-yourself/Protecting-from-invalid-input-03.png)
![](/img/writing-solid-code/CH2-assert-yourself/Protecting-from-invalid-input-02.png)

*Questions*:

1. How will you handle errors in mobile games like Angry Bird?
2. How will you handle errors in astronautic softwares?
3. How will you validate the data in the public methods? How do you assume the data is safe
   in private methods?

<end>
