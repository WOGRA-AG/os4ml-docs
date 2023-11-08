# Tutorial

Follow this guide to go step by step to get a prediction based on your data.

## Create a Databag

Therefore, open the create Databag dialog, give it a name and upload your data.
You can see expected format of your data [here][File formats].
If you don't have your own data or you just want to play around, you can use [the titanic dataset][titanic csv].

![databag create]

Proceed and wait until the dataset is uploaded and inspected (this may take a while)

![databag done]

## Create a Solution 

Open the create solution dialog and select the databag you just created (if it isn't already selected).
Define the [Problem] on your Databag by specifing the output and give the solution a name.
In case of the titanic dataset choose the column `Survived`.

In the `Select input` drop-down, you could deselect some inputs to exclude them from the Solver, but for now let's just use all inputs.
[Transfer learning] is an advanced feature, so let's use the default values and just click `Submit Solution`.

![solution create]

Currently only the [Ludwig solver] is available, but in future you will be able to select different ones. You can check the list of available solvers [here][Solvers].

Again wailt until the solution is done (this may take a while).

![solution done]
    
## Create a Prediction

Open the create prediction dialog and select the solution you just created (if it isn't already selected).
Enter the name of your prediction and upload your data.
You can download a template to see how your data should look like.

![prediction create]

Wait once more until the prediction is done (this may take a while).

![prediction done]

You can now download and inspect the results of your prediction.

[Problem]: introduction.md#Problem
[Solvers]: solvers.md
[Ludwig solver]: solvers.md#Ludwig-Solver
[File formats]: file_formats.md
[Transfer learning]: transfer_learning.md

[databag create]: assets/images/screenshots/databag_create.png
[databag done]: assets/images/screenshots/databag_done.png
[solution create]: assets/images/screenshots/solution_create.png
[solution done]: assets/images/screenshots/solution_done.png
[prediction create]: assets/images/screenshots/prediction_create.png
[prediction done]: assets/images/screenshots/prediction_done.png

[titanic csv]: assets/datasets/titanic.xlsx
