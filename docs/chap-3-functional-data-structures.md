# Chapter 3: Functional Data Structures

In Chapter 3, data structures are built and transformed with pure functions
using the example of a constructing simplified `List[+A]` singly linked list.
Working through the exercises will give an inmate understanding of core collection
methods, native Scala List data sharing, and pattern matching.

While this is useful Scala knowledge, the core data structures used in Spark are
completely isolated and different than those of native Scala. Spark users will not
use these techniques on the data itself but on the higher order operations performed
on `Dataframes`. Using 

## Relevant Content

### Mapping and Filtering Arrays

_Reference: Section 3.4.1 - More functions for working with lists_

The concept of applying 

### Folding Operations on a Dataframe

_Reference: Section 3.4 - Recursion over lists and generalizing to higher-order functions_

Often repeated operations are a `Dataframe` lead to long chains of `.withColumn`,
`.withColumnRenamed`, `.select` etc, copied and pasted to iterate over variants.
Using a **fold** on a sequence of values either set by constant or dynamically at runtime,
a sequence of operations on the `Dataframe` can be "automated". This can clean up code
but also allows for more complex operations defined at runtime.

The authors introduce the `.foldRight` primarily to fit with the specific singly linked
list example. Spark engineers will instead use the the `.foldLeft` instead to iterate over
a sequence of information in the expected order of the sequence.

```scala
def foldLeft[B](z: B)(op: (B, A) => B): B
```

By folding a sequence of 

## Example: Dynamically Performing Repeated Actions 

A simple use of this technique is folding a constant set sequence to perform repeated
operations with different parameters. In the example below, three (or more) cell towers
are given in three dimensional space and then a dataset of individual

```scala
import org.apache.spark.sql.{Column, DataFrame}
import org.apache.spark.sql.functions.{col, lit, sqrt}

import spark.implicits._

case class Tower(id: String, x: Double, y: Double, z: Double)

// Constant set of towers used to generated `diff` 
// and `dist` columns dynamically for each tower in list
val towers = Seq(
  Tower("A1", -10.2, 40.2, 0.3),
  Tower("B2", 0.245, -23.0, 10.2),
  Tower("C3", 30.24, 0.00, -1.23)
)

// Dataset of cell users with x, y, and z coordinates
val df: DataFrame = Seq(
  (101, 0.0, 0.0, 0.0), (102, 2.3, -4.5, 4.23), (103, -35.3, 53.0, 35.2),
  (104, 0.456, -23.40, -2.7), (105, 24.3, 56.3, -1.9)
).toDF("id", "x", "y", "z")

// Define distance function 
def distFunction(towerId: String): Column = sqrt(
  Seq("x", "y", "x")
    .map(coord => col(s"diff_${coord}_$towerId") * col(s"diff_${coord}_$towerId"))
    .reduce(_ + _)
)

val dist = towers.foldLeft(df)(
  (df, t) => df
    .withColumn(s"diff_x_${t.id}", col("x") - lit(t.x))
    .withColumn(s"diff_y_${t.id}", col("y") - lit(t.y))
    .withColumn(s"diff_z_${t.id}", col("z") - lit(t.z))
    .withColumn(s"dist_${t.id}", distFunction(t.id))
)

dist.show()

// +---+-----+-----+----+-----------+-------------+-----------+----------+-----------+-----------+------------+----------+------------+---------+-------------------+------------------+
// | id|    x|    y|   z|  diff_x_A1|    diff_y_A1|  diff_z_A1|   dist_A1|  diff_x_B2|  diff_y_B2|   diff_z_B2|   dist_B2|   diff_x_C3|diff_y_C3|          diff_z_C3|           dist_C3|
// +---+-----+-----+----+-----------+-------------+-----------+----------+-----------+-----------+------------+----------+------------+---------+-------------------+------------------+
// |101|  0.0|  0.0| 0.0|       10.2|        -40.2|       -0.3|     42.70|     -0.245|       23.0|       -10.2|      23.0|      -30.24|      0.0|               1.23|42.765818126162394|
// |102|  2.3| -4.5|4.23|       12.5|        -44.7|       3.93|     48.06|       2.05|       18.5|       -5.96|      18.7|      -27.93|     -4.5|  5.460000000000001| 39.76854535936661|
// |103|-35.3| 53.0|35.2|     -25.09|        12.79|       34.9|     37.73|     -35.54|       76.0|        25.0|     91.12|      -65.53|     53.0|              36.43|106.77070384707595|
// |104|0.456|-23.4|-2.7|      10.65|        -63.6|       -3.0|     65.36|      0.211|      -0.39|      -12.89|      0.49|      -29.78|    -23.4|-1.4700000000000002|48.184367921557296|
// |105| 24.3| 56.3|-1.9|       34.5|        16.09|      -2.19|     51.37|     24.055|       79.3|       -12.1|     86.28|      -5.939|     56.3|-0.6699999999999999| 56.92325710990192|
// +---+-----+-----+----+-----------+-------------+-----------+----------+-----------+-----------+------------+----------+------------+---------+-------------------+------------------+
```
