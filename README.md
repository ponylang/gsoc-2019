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

[Matthias Wahl](https://github.com/mfelsche)

#### Difficulty

"medium"
