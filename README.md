# gsoc-2019
Ideas for the Google Summer of Code 2019

## Guidelines for submitting ideas

1. See the Google Summer of Code [Defining a Project (Ideas List)](https://google.github.io/gsocguides/mentor/defining-a-project-ideas-list) page for information about how to create a good ideas list.
2. Each idea should list a proposed mentor. The idea does not have to be submitted by the mentor, but it should only be done with the mentor's consent.
3. To add to the list, open a pull request with the idea added to this document. Follow the format in the[ideas template](ideas-template.md).

## Ideas

### Ponylang Language Server


Editor/IDE support is currently limited to syntax highlighting and maybe some ctags-like features.
Lets build a [Language Server](https://microsoft.github.io/language-server-protocol/) for Ponylang to drastically improve IDE support and programming ergonomics, especially for larger codebases.

#### Expected outcomes

The expected outcome is a (not necessarily complete) language server for Pony that is working with at least one commonly used editor (think vim, emacs, sublime, vscode, ...). 

The Pony project and everybody programming Pony or learning it would drastically benefit by lowering the entry barrier. Most people nowadays expect rich IDE support with lots of features, like `GOTO Defintion`, `find usages of a symbol` etc. Bringing some of these Features to Ponylang would make the language way more approachable to newcomers.

The student picking this up would definitely learn a lot about Ponylang and its Grammar and Compiler as she/he will need to access the parsed (and type-checked) AST in whatever form available and expose it to the Language server. A lot of knowledge about language parsing, grammars and compilers can be obtained. She/he would also learn about the Language Server Protocol, as this task means implementing it. Depending on the chosen technology to solve the problem, the student will work in either C, Pony or another language and so gain experience in one or more of these languages. Last but not least, the student will receive all the praise and love from the Pony community for doing such an important and worthwile project.

#### Possible Paths

- Write the Language Server in C by using `libponyc`, which is part of [ponyc](https://github/ponylang/ponyc/tree/master/src/libponyc).
  - Advantage: Access to the same AST as is used for compilation. Typechecking for free.
  - Disadvantage: Compiler might needs some adaptation (which we will gladly help with, if need be). Writing a HTTP Api for the LSP mught not be as convenient in C, but the C code could also be used via FFI from Pony or any other language capable of FFI.

- Use [ponycc](https://github.com/jemc/ponycc) which is a Pony compiler written in Pony. It currently is only limited to constructing an AST (parsing, syntax checking, desugaring), so some more work needs to be put in this to make it fully usable. But it would enable us to write the LSP in pure Pony, that is the extracting information from the source files, the actual server etc.
  - Advantage: Pure Pony
  - Disadvantage: It is uncertain how much work needs to be put into ponycc to make it usable for the purposes of an LSP.

- Use the [ANTLR](https://www.antlr.org/) grammar generated from the grammar in the compiler: https://github.com/ponylang/ponyc/blob/master/pony.g to write the parser in another language that has good support and a rich ecosystem to develop an LSP.
  - Advantage: Plethora of available tools, maybe lots of experience.
  - Disadvantage: no typechecking like in ponyc.

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
