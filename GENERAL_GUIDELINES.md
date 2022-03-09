# General Prolog Guidelines

## Loading files

Unless specified otherwise, one should not load a database in the same file where the reasoning rules are located. For example, if we have a database of Uni courses in file `courses.pl` and a Prolog reasoning system to reason about program plans named `uni_programs.pl`, then the latter should NOT load `courses.pl` itself, as it should work with any course database possible. 

Instead, to test it one can consult both as follows:

```prolog
-? ['courses.pl'].
-? ['uni_programs.pl'].
```

Alternatively, one can design a single program `main.pl` with:

```prolog
:- ['courses.pl'].
:- ['uni_programs.pl'].
```

and just consult `main.pl`.

## Singleton variables

To get more marks and more robust code, we strongly suggest to **avoid singleton variables!** A singleton variable is a variable that only occurs once in the arguments or the body
of a predicate and is thus useless. For example in the following two definitions:

```prolog
calculate(X, Y, Z) :- Z is X+2.
```
Here `Y` is a singleton variable, and should be prefixed by an underscore `_Y` or replaced by an anonymous variable `_`.

Singleton variables make it harder to read the code and can signal a bug, like in the following example:

```prolog
inc(FirstNr, Result) :- Result is Firstnr+1.
```

Here, both `FirstNr`and `Firstnr` will be reported as singleton variables! This is very useful information because it often helps you finding typos, a common source of bugs in Prolog, as shown above (`Firstnr` should have been `FirstNr`).

## Documentation

Each predicate you write should have a concise and clear documentation also indicating its mode of usage. You can find plenty of good documentation examples in the SWI-Prolog manual and even help system (e.g., try `help(append)`).

For **documentation style** similar to JavaDoc, refer to [SWI-Prolog Source Documentation](https://www.swi-prolog.org/pldoc/doc_for?object=section(%27packages/pldoc.html%27)).

## Indentation

As always, your code should be easy to read. Putting every subgoal on a new line is a good idea.

## Efficiency

Unless specifically stressed, you don't have to go out of your way for optimization purposes. However, the code must aim to be reasonably efficient. You should not be traversing the lists unnecessarily, for example. Basically, without doing crazy tricks, your code should aim to be efficient.

## Duplicate answers

In general, you should eliminate duplicates whenever you can. Sometimes, however, you may not be able to eliminate all duplicates, and that's OK. In each query, you should make a decision as to whether or not it is possible to eliminate duplicates.  Sometimes there are different causes of duplicates, and you can deal with one, but not the other. It is part of the task to figure it out when it is doable and when it is not.

## Style

* Simpler, shorter code is generally best.
* Try to use unification variables when possible; for example `swap([A,B], [B,A]).` rather than `swap(L1, L2) :- L1=[A,B], L2=[B,A].`
* Pick intuitive names for your predicates and arguments.
* good naming convention for a helper predicate used by a predicate `pred` is `pred_aux` (`aux` stands for"auxiliary"). This makes it easier to understand what it is used for.

