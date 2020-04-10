
# Design Principles
Improving quality, design and maintainability with Design Principles

## D.R.Y (Don’t repeat yourself) Principle
Analysis of the written code and the desire to improve it are always key in software writing.

When writing several classes with similar properties, we may encounter similar problems. This is a sign that the code inside these classes is common and it may indicate that it should be separated into another class that will deal with repetitive tasks in one place. Thanks to this operation, both classes will use the same code, and thus, the probability of error will drop.

## KISS - Keep It Simple, Stupid!
This rule is often mentioned when discussing architecture or details of building projects. Its essence is striving to maintain an elegant and transparent structure, without adding unnecessary elements.

## SOC - Separation of Concern
The separation of issues consists in the division of the program into separate modules that overlap with as little functionality as possible. We call this kind of program modular. Each element of the system should have its separate and singular application. The purpose of SoC (Separation of Concern) is to create a system in which each part plays a significant role while maintaining the possibility of maximum adaptation to changes. SoC does not refer only to the system architecture, but to various issues, eg to divide the application into layers (presentation, business logic, access to data, database).

## CQS - Command Query Separation
It is a rule that says that every method in the system should be classified into one of two groups:

Command - these are methods that change the state of the application and do not return anything.
Query - these are methods that return something, but do not change the state of the application.

## Tell, don't ask Principle
Used to eliminate type casting and checkong


