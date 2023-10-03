# Chapter 3: Functional Data Structures

In Chapter 3, data structures are built and transformed with pure functions
using the example of a constructing simplified `List[+A]` singely linked list.
Working through the exercises will give an inmate understanding of core collection
methods, native Scala List data sharing, and pattern matching.

While this is useful Scala knownledge, the core data structures used in Spark are
completely isolated and different than those of native Scala. Spark users will not
use these techniques on the data itself but on the higher order operations performed
on `Dataframes`.

## Folding a Sequence of Operations on a Dataframe

_Reference: Section 3.4 - Recursion over lists and generalizing to higher-order functions_

Often repeated operations are a `Dataframe` lead to long chains of `.withColumn`,
`.withColumnRenamed`, `.select` etc, copied and pasted to iterate over variants.
Using a **fold** on a sequence of values either set by constant or dynamically at runtime,
a sequence of operations on the `Dataframe` can be "automated". This can clean up code
but also allows for more complex operations defined at runtime.

The authors introduce the `.foldRight` primarily to fit with the specific singlely linked
list example. Spark engineers will instead use the the `.foldLeft` instead to iterate over
a sequence of information in the expected order of the sequence.

```scala
def foldLeft[B](z: B)(op: (B, A) => B): B
```

A simple use of this technique is folding a constant set sequence to perform repeated
operations with different parameters. In the example below, three (or more) cell towers
are given in three dimensional space and then a dataset of individual

```scala
import spark.implicits._

case class Tower(id: String, x: Float, y: Float, z: Float)

// Constant set of towers used to generated `diff` 
// and `dist` columns dynamically for each tower in list
val towers = Seq(
  Tower("A1", -10.2, 40.2, 0.3),
  Tower("B2", 0.245, -23.0, 10.2),
  Tower("C3", 30.24, 0.00, -1.23)
)

// Dataset of cell users with x, y, and z corri
val df: Dataframe = Seq(
  (101, 0.0, 0.0, 0.0), (102, 2.3, -4.5, 4.23), (103, -35.3, 53.0, 35.2),
  (104, 0.456, -23.40, -2.7), (105, )
).toDF("id", "x", "y", "z")

towers.foldLeft(df)(
  (df, t) => df
    .withColumn(s"diff_x_$t", col("x") - lit(t.x))
    .withColumn(s"diff_y_$t", col("y") - lit(t.y))
    .withColumn(s"diff_z_$t", col("z") - lit(t.z))
    .withColumn
)

```

### Example: Column List Generation

One simple example is column list generation for performing

For example, in section 