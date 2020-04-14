# Sous-title
[![Build Status](https://travis-ci.org/mdauthentic/sous-title.svg?branch=master)](https://travis-ci.org/mdauthentic/sous-title)


Read and convert `.srt` file to `csv` or `List`


## build.sbt
```scala
libraryDependencies += "io.github.mdauthentic" % "sous-title_2.13" % "0.3.0"
```

## Getting started

### Import
```scala
import io.github.mdauthentic.core._
```
### Reading example
```scala
scala> val reader = SRTReader.open("file.srt")
reader: List(SRT(1, 00:00:33.599, 00:00:35.270, List(Soy Amelia Folch.)))

```
### Inline reader example
Inline reader returns a list of `.srt` type

```scala
scala> val srt =
      """1
        |00:00:33,599 --> 00:00:35,270
        |(NARRA) "Soy Amelia Folch.
        |
        |2
        |00:00:36,199 --> 00:00:39,870
        |Tengo 23 años y sin embargo
        |he salvado la vida del Empecinado.""".stripMargin
```

```scala
scala> val inlineReader = SRTReader.readInLine(srt)
inlineReader: List(SRT(1,00:00:33.599,00:00:35.270,List((NARRA) "Soy Amelia Folch.)), SRT(2,00:00:36.199,00:00:39.870,List(Tengo 23 años y sin embargo, he salvado la vida del Empecinado.)))
```

### Writing example
There are two ways to write to file;
- writing without header
```scala
scala> val reader = SRTReader.open("file.srt")
reader: List(SRT(1, 00:00:33.599, 00:00:35.270, List(Soy Amelia Folch.)))

scala> SRTWriter.write(reader, "output.csv")
```
using file path directly
```scala
scala> SRTWriter.write("inputFileName.srt", "outputFileName.csv")
```
- with user-defined header
```scala
scala> SRTWriter.write("input.srt", "output.csv", List("id", "start_time", "end_time", "subtitle"))
```

## Motivation
In `Scandal` (a TV series), `wine` was mentioned several times and I was curious to know the number of times the word was used in the entire series (from seasons 1 - 7).

## License
[Apache 2.0](http://www.apache.org/licenses/LICENSE-2.0)
