# Chapter 4: Handling Errors Without Exceptions

The authors summarize chapter four as such:

_The big idea is that we can represent failures and exceptions 
with ordinary value, and we can write higher-order functions that
abstract our common patterns of error handling and recovery._

The chapter is structured similar to Chapter 3 by re-creating
Scala native classes, in this case `Option` and `Either`. Working
through this chapter not only improves knowledge of these commonly
used Scala objects, but is critical in creating **complete** Spark
UDFs and error resistant pipelines.

TODO partial vs complete description

Taken from the book directly, we reject creating **partial** functions
for the following reasons:

- It allows errors to silently propagate
- It results in a fair amount of boiler plate at call sights
- It's not applicable to polymorphic code
- It demands a special policy or calling convention of callers

## Option Handling for Nulls

In the case of UDFs, often the `Option` trait is essential to creating
a **complete** function by enabling the handing of 

## Using Either for Exception Handling

TODO

## Parsing Unstructured Data Structures

TODO