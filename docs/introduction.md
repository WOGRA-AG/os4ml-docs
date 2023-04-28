# Introduction

Let's first start with the basic terminology of os4ml. It is illustrated in the following picture:

![terminoloy]

## Databag
A databag is a convenient container for storing your data.
You can easily create a databag by following the instructions in this [tutorial][tutorial], or explore the various file formats you can upload [here][file formats].
To manage the diversity of data types, we use the concept of multimodal data.
Think of multimodal data as a table where each column is associated with a specific datatype, and the rows represent data corresponding to these columns.

The [petfinder dataset][petfinder dataset] is an excellent example of multimodal data.
For instance, it features Fenny, a dog(type 1) who is five years old and has been waiting for adoption for 100 days (AdoptionSpeed 4).
The columns Type and AdoptionSpeed are categorical, the column Name contains text data, and Age is a numerical value.
Additionally, the Image column contains image data.

![petfinder]

## Problem
Based on a databag, you can define a problem to be solved by specifying one or more output columns to be predicted.
In the petfinder dataset example, you would typically want to predict the 'AdoptionSpeed' column.

[Here][databag examples] you can find more examples that illustrate how to model your machine learning problem using the multimodal approach.

## Solver
A Solver is an abstraction of an AI algorithm that can solve a specific problem, by training an AI model on data from a Databag to predict the specified columns.
To explore available solvers, check out [this list][solvers].

## Solution
When a [solver][solver] is executed on a [problem][problem], it produces a solution that can be used to predict values for unseen data.
To learn how to create a solution using a solver, check out this [tutorial][tutorial].


[databag]: #Databag
[solver]: #Solver
[problem]: #Problem
[databag examples]: /os4ml/examples/

[tutorial]: tutorial.md
[file formats]: file_formats.md
[solvers]: solvers.md

[terminoloy]: assets/images/databag_solver_solution.png
[petfinder]: assets/images/petfinder.png
[petfinder dataset]: https://www.kaggle.com/c/petfinder-adoption-prediction/data
