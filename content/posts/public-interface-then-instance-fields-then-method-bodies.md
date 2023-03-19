---
title: "Public interface then instance fields then method bodies"
date: 2023-03-18T23:12:51-04:00
draft: false
---

I write classes in the order below. Students should write classes in this order too. Assignments and projects should be written with this order in mind.

1. Public interface (methods headers &amp; documentation)
2. Instance fields
3. Method bodies (implementation code)

## Public interface

A class's public interface defines how the class will be used by other classes. Everything else about a class exists to support its public interface.

Writing all method headers and complete documentation for each method forces the designer to consciously consider how the class will be used. When the public interface is written concurrently with the implementation the final class is less likely to be a coherent and tightly integrated set of methods and public fields.

Poor designs are easier to recognize when the public interface is written first. Changes to the public interface are inexpensive before implementation code has been written.

## Instance fields

Instance fields exist to maintain the state necessary for a class's methods to operate. Unless an instance field is part of the public interface (which is discouraged in AP Computer Science) it has no other purpose.

Instance fields are often placed at the top of a class to make the class easier to read. The placement of instance fields should not be interpreted as encouragement to specify them before specifying the public interface. (The Big Java textbook places instance fields at the bottom of each class, presumably to encourage that they be written after the public interface.)

Specifying instance fields before the public interface can easily result in the following design issues.

- Duplicate data stored as instance fields
- Unnecessary instance fields
- Failure to store necessary data
- An incoherent public interface

Specifying instance fields before the public interface results in the instance fields driving the public interface. The public interface should drive everything else in the class.

Storing data as an instance field that could have been calculated from the values of other instance fields is (usually) a mistake. Updating an instance field without updating the fields that depend on it can result in an inconsistent state. (Deliberately storing data that could have been calculated is known as caching. Caching requires deliberate techniques to ensure that cached data consistent. Storing a value that could have been calculated without using these techniques is inappropriate.)

## Method bodies

A well designed public interface and well chosen instance fields make it easy to implement each method. Each methods in a well designed class performs a specific focused task. Since the public interface and instance fields have already been completed the methods can also be written in any order.

## Test driven development

Writing the public interface first also encourages the excellent practice of test driven development. Briefly, test driven development involves writing the tests for a piece of code before writing the code. The tests ensure that the code does what it is supposed to do. The code is written to pass the tests (to do what it is supposed to do) and nothing more.

[Test driven development (Wikipedia)](https://en.wikipedia.org/wiki/Test-driven_development)

## Projects &amp; Assignments

I tutor AP Computer Science. Few things make my skin crawl more than projects that require students to use poor designs. I particularly hate projects that specify duplicate data stored as instance fields.

When providing skeleton code for projects consider specifying a public interface rather than instance fields. Many public interfaces can be implemented in surprisingly efficient ways if students are permitted to choose their own instance fields. A `Line` class might be implemented using `String equation` as an instance field. `Line` might also be implemented using `Point2D.Double one, two`.

If you're certain that you want to specify the instance fields for a project, consider specifying the public interface as well. Ensure that the errors discussed above are not present.

Never write skeleton code directly. Always write the entire project (or start with a student's solution from a previous year) then remove the parts you don't want to share with students. Writing skeleton code directly (without the corresponding code inside the methods) can result in projects that are impossible to complete as specified.
