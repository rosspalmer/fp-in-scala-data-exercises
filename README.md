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

![Book Cover](https://external-content.duckduckgo.com/iu/?u=https%3A%2F%2Ftse2.mm.bing.net%2Fth%3Fid%3DOIP.epb0grWt_qc59nd-0hwPTAHaJS%26pid%3DApi&f=1&ipt=eb1bf7575e4575481b6b6d3bf93ff2f80a2408c319c019476e9825d29431950a&ipo=images)

Official Link: [_Functional Programming in Scala_ by Chiusano and Bjarnason](https://www.manning.com/books/functional-programming-in-scala)

Github Link: [fpinscala Project](https://github.com/fpinscala/fpinscala)

The first edition of this book, released in 2014, is now available for free at the link above.
The concepts are still relevant and widely used in any major Scala package, especially
for Spark engineers, who as of this writing are still using Scala 2 like in the book. 

Working through both the reading material and exercises is difficult and slow but
extremely rewarding. Individual chapters can be worked in rough isolation with
the authors providing detailed answers and accompanying code in the Github link above.

### Book Chapters


1. What is Functional Programming?
2. Getting Started with Functional Programming in Scala
3. Functional Data Structures
4. Handling Errors with Expressions
5. Strictness and Laziness
6. Purely Functional State
7. Purely Functional Parallelism
8. Property-based testing
9. Parser Combinators
10. Monoids
11. Monads
12. Applicative and Transversable Functors
13. External Effects and I/O
14. Local Effects and Mutable State
15. Steam Processing and Incremental I/O

### Benefits for Spark Users

- Great for improving knowledge of core Scala syntax and code patterns
- `Option` handling critical to NULL and exception processing in UDFs
- Higher order function patterns can be used to automate complex 
transformations on Dataframe and Datasets
- Error from specific operations can be more robustly using `Either`
- Understand and utilize native Scala to safely parallelize data jobs or tasks

## Using with Spark Docs

3. [Chapter 3: Functional Data Structures](./docs/chap-3-functional-data-structures.md)
4. [Chapter 4: Handling Errors without Exceptions](./docs/chap-4-handling-errors-without-exceptions.md)