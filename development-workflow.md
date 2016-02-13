# Git Initial Dev Workflow

## Branches

* master

The only constant branch in initial development is
the master branch. It contains finished chunks of code. This doesn't mean
that it only contains completely finished features but everything in the master
branch is usable and tested.
Every other branch will be temporary in its existence.

## Feature workflow

After the planning has concluded, you will come to the point of starting the
implementation. But how to develop from scratch (with a framework in background)?
Exactly what should be done in one branch and when do you skip to another branch?

This is not as easy as it should be. The first step to make the entire process
scalable to multiple developers is to define the boundaries of sub systems.
In a large system you will have many interacting components. But each sub system
(e.g. user and group system) will have some internally used code and code that
is used from the outside. By defining the outside interfaces and laying out
the dependencies, it should be possible to bring all features in a linear
path.

This path will be the development timeline if only one developer works on the
project. If more devs are at hand the sub systems should be decoupled enough
(even interacting ones) to work on them at the same time. Especially in the
beginning there will be a lot of ground work necessary to build up extension
points, etc. Each of these layers should be done in one branch and merged after
testing.

Once a specific set of features is available - the core set, it is possible
to develop specific features in one branch, because all extension points to
connect the new features with the existing structure should be up and running
at that point.

## Github issues

The Github issues can be used for multiple purposes. First it's a bugtracker.
But it also works as a project planning tool.

How to use it? After initial planning there should be issues for each sub system
with info on the specs. These issues will not be done one by one. In a usual
development you will hit each of these again and again until the final functionality
as specified is developed.

In addition to these very vague issues, there will be issues for every bug or
UX problem you encounter during unscripted testing in the browser.

Again these issues don't have to be fixed/resolved one by one. Rather you should
determine where the issue lies and give all necessary info on how to solve it
in the issue itself.

The next step is to prioritze these specific issues. Some might be fixed
along the way when you touch the necessary files anyway. Others might get fixed,
because the entire feature will be reworked, etc.

UX errors in particular should be postponed until a more complete set of
features is developed to prevent fixing something, that will be changed
anyway.

Once you start working on an issue, assign it to you.
