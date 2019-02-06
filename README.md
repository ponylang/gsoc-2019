# gsoc-2019
Ideas for the Google Summer of Code 2019

## Guidelines for submitting ideas

1. See the Google Summer of Code [Defining a Project (Ideas List)](https://google.github.io/gsocguides/mentor/defining-a-project-ideas-list) page for information about how to create a good ideas list.
2. Each idea should list a proposed mentor. The idea does not have to be submitted by the mentor, but it should only be done with the mentor's consent.
3. To add to the list, open a pull request with the idea added to this document. Follow the format in the[ideas template](ideas-template.md).

## Ideas

### Add Generic Type Inference to Ponylang

Ponylang supports generic types and makes heavy use of it e.g. in the [collections](https://stdlib.ponylang.io/collections--index) and [itertools](https://stdlib.ponylang.io/itertools--index).
Type Inference is available for local variables, lambdas and array literals. But as of now Ponylang is missing inference for generic type arguments.
This leads to mild inconveniences as one has to restate type arguments at every place. Code making heavy use of generics is not anymore as readable as it could be.

The idea to fix it already came up a long time ago:

- [RFC](https://github.com/ponylang/rfcs/blob/mod-operator/text/0010-generic-type-inference.md)
- [Ponyc Issue](https://github.com/ponylang/ponyc/issues/1184)

#### Expected outcomes

Adding Generic Type Inference to Ponylang will bring the joyful benefit of having to write less boilerplate when using generic code in.
It will make existing code more readable and more straightforward to write 

The student picking this up will learn a lot about Ponylang, its compiler and type-system (which is one of the most interesting ones i came across) and how it is parsed and type-checked. This work requires to
think about all the cases where and how type-inference of type-arguments should work. This will give very good insight into how Ponylang is parsed, typechecked and compiled.
This will also provide lots of real-world knowledge about implementing compilers in general.

And last but not least the everlasting gratefulness of the Pony community is guaranteed!

#### Skills required

- Experience in programming C
- Basic knowledge of compilers

#### Mentor

- [Matthias Wahl](https://github.com/mfelsche)

#### Difficulty

"medium"

### Ponylang Language Server


Editor/IDE support is currently limited to syntax highlighting and maybe some ctags-like features.
Lets build a [Language Server](https://microsoft.github.io/language-server-protocol/) for Ponylang to drastically improve IDE support and programming ergonomics, especially for larger codebases.

#### Expected outcomes

The expected outcome is a (not necessarily complete) language server for Pony that is working with at least one commonly used editor (think vim, emacs, sublime, vscode, ...). 

The Pony project and everybody programming Pony or learning it would drastically benefit by lowering the entry barrier. Most people nowadays expect rich IDE support with lots of features, like `GOTO Defintion`, `find usages of a symbol` etc. Bringing some of these Features to Ponylang would make the language way more approachable to newcomers.

The student picking this up would definitely learn a lot about Ponylang and its Grammar and Compiler as she/he will need to access the parsed (and type-checked) AST in whatever form available and expose it to the Language server. A lot of knowledge about language parsing, grammars and compilers can be obtained. She/he would also learn about the Language Server Protocol, as this task means implementing it. Depending on the chosen technology to solve the problem, the student will work in either C, Pony or another language and so gain experience in one or more of these languages. Last but not least, the student will receive all the praise and love from the Pony community for doing such an important and worthwile project.

#### Possible Paths

This is just the general ideas to pull this off, I could come up with. Please take these as suggestions and don't let you limit by this.

- Write the Language Server in C by using `libponyc`, which is part of [ponyc](https://github/ponylang/ponyc/tree/master/src/libponyc).
  - Advantage: Access to the same AST as is used for compilation. Typechecking for free.
  - Disadvantage: Compiler might needs some adaptation (which we will gladly help with, if need be). Writing a HTTP Api for the LSP mught not be as convenient in C, but the C code could also be used via FFI from Pony or any other language capable of FFI.

- Use [ponycc](https://github.com/jemc/ponycc) which is a Pony compiler written in Pony. It currently is only limited to constructing an AST (parsing, syntax checking, desugaring), so some more work needs to be put in this to make it fully usable. But it would enable us to write the LSP in pure Pony, that is the extracting information from the source files, the actual server etc.
  - Advantage: Pure Pony
  - Disadvantage: It is uncertain how much work needs to be put into ponycc to make it usable for the purposes of an LSP.

- Use the [ANTLR](https://www.antlr.org/) grammar generated from the grammar in the compiler: https://github.com/ponylang/ponyc/blob/master/pony.g to write the parser in another language that has good support and a rich ecosystem to develop an LSP.
  - Advantage: Plethora of available tools, maybe lots of experience.
  - Disadvantage: no typechecking like in ponyc.

- ...

#### Skills required

- Some basic knowledge in C and compilers. 
- Knowledge of Pony would be greatly helpful, but (I think) is not necessarily required.
- Knowledge of the [LSP](https://microsoft.github.io/language-server-protocol/) is helpful.
- We can help with guidance around any of these.

#### Mentor

[Matthias Wahl](https://github.com/mfelsche)

Maybe someone else wants to help, too?

#### Difficulty

"medium" to "hard" (due to exploratory nature of this project)

### WALLAROO AS BEAM RUNNER

Walaroo would serve as a great "runner" to work with Apache Beam.  Alternatively, Beam would benefit from a non-JVM runner and Walaroo would be well served from the rich ecosystem of IOs, and growing user base.  I'd like to see these two things work together!  


#### Expected outcomes

PONY would gain from Walaroos visibility which would come from being a unique runner for Beam (which has additional reach).  A runner written in PONY would force Beam to think about non-JVM land.  It would also open the door nicely for a PONY SDK (down the road) and write the interface IO in PONY at the other end.    

The Student would benefit from diving into Ponlylang, as well as streaming systems overall (Walaroo and PONY).  Interesting work is going on around a common 'Portability Framework' which this project would have impact in informorming.



#### Skills required

- Knowledge of JAVA (or JVM language)
- Knowledge of Pony would be helpful, but not required
- Knowledge of Apache Beam would be helpful, but not required
- ???


#### Mentor

- [Austin Bennett](https://github.com/brucearctor)
- HOPEFULLY (AND NECESSARILY) others in the PONY/WALAROO COMMUNITY
- I would also pull in people on the Beam side, I'm a heavy advocate and user, and just getting into the nuances and development of it


#### Difficulty

"hard" to get implimented fully.  maybe "medium" to wire and get some basic functionality and reasonable POC put together.  

### Support Finite Recursive Type Aliases

Currently Pony has type aliases but doesn't allow recursive alias such as:

```pony
type JsonNull    is None
type JsonBoolean is Bool
type JsonString  is String
type JsonNumber  is F64
type JsonArray   is Array[JsonEntity]
type JsonObject  is Map[JsonString, JsonEntity]

type JsonEntity is
  ( JsonNull
  | JsonBoolean
  | JsonString
  | JsonNumber
  | JsonArray
  | JsonObject)
```

This makes a number of APIs that have to be constructed to work around this quite painful to use. Any data type that has Arrays etc that can contain its other types (like JSON does) are affected. There's been an issue open for a long time to address this. Someone picking this up and introducing the solution would be great. [ponylang/ponyc#267](https://github.com/ponylang/ponyc/issues/267)

The github issue has been labeled as "major effort" in terms of complexity. This is primarily because it touches many parts of the compiler. As I stated before, this would be a great issue to dig in and learn how the compiler works. Great for someone who wants to dig into compiler work but hasn't done much previously with other compilers (or the Pony compiler).

#### Expected outcomes

Whoever was to take this on, would get an opportunity to dig into the compiler a great deal and in the process learn an awful lot about the Pony type system and the compiler, as well as about type-systems and compilers in general.

The end result of this would the ability to definite relationships like the one @jemc describes in the attached issue. Amongst enabling a lot of interesting language constructs that are currently forbidden, this project would finally enable Ponylang to redefine its [JSON](https://stdlib.ponylang.org/json--index) library and bring it into good shape.

#### Skills Required

- Some experience in C programming.
- Some initial knowledge about compilers and static type systems would be helpful, but is not a must.

#### Mentor

To be announced.

#### Difficulty

"medium" to "hard", mostly depending on your background in compilers and C-programming.

### AWS Lambda runtime for Pony

[Custom AWS Lambda Runtimes](https://docs.aws.amazon.com/lambda/latest/dg/runtimes-custom.html) can be created to allow Lambda functions to be written in any language. This project would be to create the necessary libraries and documentation that would allow someone to write a Lambda function in Pony.

#### Expected outcomes

At the end of this project it will be possible for anyone to create a Lambda function in Pony and run it on AWS. The deliverables would most likely be a Pony library for creating Lambda functions and documentation for using the library and deploying the function.

#### Skills required

- A basic understanding of how AWS Lambda works (easily obtainable from their docs and other sources).

#### Mentor

To be announced.

#### Difficulty

"easy"