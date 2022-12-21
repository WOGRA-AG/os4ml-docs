# Introduction

Let's start with the basic Terminology of os4ml first.

## Databag

A databag is a container for your data.
Learn how to create a databag [here][tutorial] or see the different types of files you can upload [here][file formats].


## Solver

A solver is an abstraction of a specific AI algorithm.
It trains an AI model on the data of a databag.
[Here][solvers] you can find a list of all available solvers.


## Solution

A run of a [solver] on a [databag] is called Solution.
The solution stores additional information, such as the columns of the databag that get predicted.
You can follow the [tutorial] to create one.


[databag]: #Databag
[solver]: #Solver

[tutorial]: tutorial.md
[file formats]: file_formats.md
[solvers]: solvers.md