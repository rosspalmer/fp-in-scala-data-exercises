# Functional Programming in Scala: Spark Examples

This repo contains examples using patterns outlined in Functional Programming in Scala
to handle common issues encountered in a Spark data setup. These examples use either
Scala native with Spark, Spark SQL functions enabling FP, or Python with Pyspark.

## Functional Programming in Data

Spark users, or any data engineers using Scala, will generally not use a
purely functional patterns like a `cats` user or general Scala developer.
Dealing with an external data platform(s) and common conventions often
make this impractical to have hard FP enforcement but Spark users can still
benefit greatly from using FP approaches when appropriate.

- Purely functional transforms and UDFs are easy to maintain, test, and extend
- Scala's functional syntax allows for handling exceptions in a much cleaner way
- Functional code improves re-usability by forcing developers to isolate
  and identify contextual data for data operations

## Book: Functional Programming in Scala

Official Link: [_Functional Programming in Scala_ by Chiusano and Bjarnason](https://www.manning.com/books/functional-programming-in-scala)

The first edition of this book, released in 2014, is now available for free at the link above.
The concepts are still relevant and widely used in any major Scala package, especially
for Spark engineers, who as of this writing are still using Scala 2 like in the book. 

Working through both the reading material and exercises is difficult and slow but
extremely rewarding. Individual chapters can be worked in rough isolation with
the authors providing detailed answers and accompanying code in the Github link above.

### Benefits for Spark Users

- Great for improving knowledge of core Scala syntax and code patterns
- `Option` handling critical to NULL and exception processing in UDFs
- Higher order function patterns can be used to automate complex 
transformations on Dataframe and Datasets
- Error from specific operations can be more robustly using `Either`

### Book Chapters

TODO

## Using with Spark Docs

3. [Chapter 3: Functional Data Structures](./docs/chap-3-functional-data-structures.md)
4. [Chapter 4: Handling Errors without Exceptions](./docs/chap-4-handling-errors-without-exceptions.md)