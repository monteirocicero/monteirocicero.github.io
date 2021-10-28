---
layout: post
title: "Design and Development Principles"
date: 2021-04-14 19:50:00 -0000
categories: Design
---

# Design and Development Principles

There is a simple manner to reach a good design and understand it on a software project. The application of some design principles without writing no one line of code could improve the development experience of your systems.

>**Principle.** a moral rule or a strong belief that influences your actions by Oxford dictionaries.

>**Design.**" Structures and decisions at a lower level" by Clean Architecture book.

&nbsp;

# KISS (Keep it Simple Stupid)

## Context
Today developers tend to complicate the problem.\
So, this leads to the spaghetti code, classes, and methods with hundreds of lines of code.\
Make the mistake, don't break down into small problems, and don’t use the conquer and divide strategy to solve complex problems.

## Benefit
Solve more problem faster.\
Solve complex problems in the fewer line of code.\
Better quality code.\
Easier to maintain.\
Easier to extend, modify or refactor.\
Easy to understand the code.\
Simple to test.

## How I do this?
Break Down your tasks into subtasks.\
Break down your problems into many small problems.\
Build small methods that just only solve one little problem.\
Build small classes.\
Try to keep it as simple as possible.

&nbsp;

# DRY (Don’t repeat yourself)

## Context
When we have a lot of code repeat again and again.\
Multiple points to change.\
When we do the same thing for the umpteenth time.

## Benefit
Less code.\
Easy to maintain.\
Reduces the chance of bugs.

## How I do this?
Don’t write a small method, but divide your logic and reuse it.\
Use your IDE, it can be your best friend to suggest a refactoring code.

For example, should we refactor to merge these two products? The answer is no because they are of different contexts, another namespace, so you should have attention to where the repetition is appropriate.

{% highlight kotlin %}
package sales

class Product(val name: String, val description: String, val price: Double)

package fulfillment

class Product(val name: String, val description: String, val price: Double)
{% endhighlight %}

&nbsp;

# YAGNI(You Aren’t Gonna Need It)

A Practice of XP (Extreme programming).\
Simple Design.

## Context
When we build the future feature because I supposed that it will be cheaper to do now instead of in the future.It is known too, as a big design upfront.

## Benefit
Simple Design.\
Care about what is important at this moment.

## How I do this?
We should spend time with the right features in the current time. The future has not come yet.

![yagni](/assets/yagni.png)


>The below image shows for us the cost of the build feature.


![yagni-fowler](/assets/yagni-fowler.png)

**IMPORTANT**: “Yagni is not a justification for neglecting the health of your code base. Yagni requires(and enables) malleable code”. Extract from the Martin Fowler blog.

# Summary
The main ideia is look around and notice that the simple thing could bring the high impact in the maintainability of your code without writing no one line of code, but simple following the best practices of the industry that was accumulated over a long time.

### bibliography
[https://people.apache.org/~fhanik/kiss.html](https://people.apache.org/~fhanik/kiss.html)<br>
[https://dzone.com/articles/software-design-principles-dry-and-kiss](https://dzone.com/articles/software-design-principles-dry-and-kiss)<br>
[https://www.martinfowler.com/bliki/Yagni.html](https://www.martinfowler.com/bliki/Yagni.html)<br>
[ttps://medium.com/better-programming/yagni-you-aint-gonna-need-it-f9a178cd8e1](https://medium.com/better-programming/yagni-you-aint-gonna-need-it-f9a178cd8e1)<br>
(https://people.apache.org/~fhanik/kiss.html)<br>
(https://dzone.com/articles/software-design-principles-dry-and-kiss)<br>
(https://www.martinfowler.com/bliki/Yagni.html)<br>
(https://medium.com/better-programming/yagni-you-aint-gonna-need-it-f9a178cd8e1)<br>

