# Functional Programming in Scala: Spark Examples

This repo contains examples using patterns outlined in Functional Programming in Scala
to handle common issues encountered in a Spark data setup. These examples use either
Scala native with Spark, Spark SQL functions enabling FP, and Python TODO.

## Chapter 3: Functional Data Structures

In Chapter 3, data structures are built and transformed with pure functions
using the example of a constructing simplified `List[+A]` singely linked list.
Working through the exercises will give an inmate understanding of core collection
methods, native Scala List data sharing, and pattern matching.

While this is useful Scala knownledge, the core data structures used in Spark are
completely isolated and different than those of native Scala. Spark users will not
use these techniques on the data itself but on the higher order operations performed
on `Dataframes`.

### Example: Folding a Sequence of Operations on a Dataframe

_Reference: Section 3.4 - Recursion over lists and generalizing to higher-order functions_

Often repeated operations are a `Dataframe` lead to long chains of `.withColumn`, 
`.withColumnRenamed`, `.select` etc, copied and pasted to iterate over variants.
Using a **fold** on a sequence of values either set by constant or dynamically at runtime,
a sequence of operations on the `Dataframe` can be "automated". This can clean up code
but also allows for more complex operations defined at runtime.

The authors introduce the `.foldRight` primarily to fit with the specific singlely linked
list example. Spark engineers will instead use the the `.foldLeft` instead to iterate over
a sequence of information in the expected order of the sequence.

A simple use of this technique is folding a constant set sequence to perform repeated
operations with different parameters. In the example below, three (or more) cell towers
are given in three dimensional space and then a dataset of individual 

```scala
val towers

val df: Dataframe = Seq(
  ()
)
```

### Example: Column List Generation

One simple example is column list generation for performing 

For example, in section 
