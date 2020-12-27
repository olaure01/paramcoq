# Paramcoq

[![CI][action-shield]][action-link]
[![Contributing][contributing-shield]][contributing-link]
[![Code of Conduct][conduct-shield]][conduct-link]
[![Zulip][zulip-shield]][zulip-link]
[![DOI][doi-shield]][doi-link]

[action-shield]: https://github.com/coq-community/paramcoq/workflows/CI/badge.svg?branch=v8.13
[action-link]: https://github.com/coq-community/paramcoq/actions?query=workflow%3ACI

[contributing-shield]: https://img.shields.io/badge/contributions-welcome-%23f7931e.svg
[contributing-link]: https://github.com/coq-community/manifesto/blob/master/CONTRIBUTING.md

[conduct-shield]: https://img.shields.io/badge/%E2%9D%A4-code%20of%20conduct-%23f15a24.svg
[conduct-link]: https://github.com/coq-community/manifesto/blob/master/CODE_OF_CONDUCT.md

[zulip-shield]: https://img.shields.io/badge/chat-on%20zulip-%23c1272d.svg
[zulip-link]: https://coq.zulipchat.com/#narrow/stream/237663-coq-community-devs.20.26.20users


[doi-shield]: https://zenodo.org/badge/DOI/10.4230/LIPIcs.CSL.2012.399.svg
[doi-link]: https://doi.org/10.4230/LIPIcs.CSL.2012.399

The plugin is still in an experimental state. It is not very user friendly (lack of good error messages) and still contains bugs. But is useable enough to "translate" a large chunk of standard library.


## Meta

- Author(s):
  - Chantal Keller (initial)
  - Marc Lasson (initial)
  - Abhishek Anand
  - Pierre Roux
  - Emilio Jesús Gallego Arias
  - Cyril Cohen
  - Matthieu Sozeau
- Coq-community maintainer(s):
  - Pierre Roux ([**@proux01**](https://github.com/proux01))
- License: [MIT](LICENSE)
- Compatible Coq versions: The master branch tracks the development version of Coq, see releases for compatibility with released versions of Coq.

- Additional dependencies: none
- Coq namespace: `Param`
- Related publication(s):
  - [Parametricity in an Impredicative Sort](https://hal.archives-ouvertes.fr/hal-00730913/) doi:[10.4230/LIPIcs.CSL.2012.399](https://doi.org/10.4230/LIPIcs.CSL.2012.399)

## Building and installation instructions

The easiest way to install the latest released version of Paramcoq
is via [OPAM](https://opam.ocaml.org/doc/Install.html):

```shell
opam repo add coq-released https://coq.inria.fr/opam/released
opam install coq-paramcoq
```

To instead build and install manually, do:

``` shell
git clone https://github.com/coq-community/paramcoq.git
cd paramcoq
make   # or make -j <number-of-cores-on-your-machine> 
make install
```


Available commands
------------------

The default arity is 2.

- Parametricity *ident* as *name* [arity *n*].

Declare the translation named *name* from the translation of the constant or inductive *ident*.

- Parametricity [Recursive] *ident* [arity *n*] [qualified].

The default name for the translation of the constant or inductive *ident* is automatically generated (from its unqualified name).
You can use the `Recursive` option to recursively translate all the constants and inductives which are used by *ident*.
You can use the `qualified` option to use a qualified default name for the translated constants and inductives. The default name then has the form `Module_o_Submodule_o_ident` if *ident* lies in the `Module.Submodule` namespace.

- Parametricity Translation *term* [as *name*] [arity *n*].

Define a new constant named *name* obtained by computing the parametricity translation of *term*.

- Parametricity Module *modulepath*.

Recursively translate everything in a module.

- Realizer *constant or variable* [as *name*] [arity *n*] := *term*.

Declare *term* to be the translation of a constant.
Useful to translate terms containing section variables, or axioms.

Note that both translating a term or module may lead to proof obligations (for some fixpoints and opaque terms if you did not import `ProofIrrelevence`).

- [Global | Local] Parametricity Tactic := t.

Use the tactic t to solve proof obligations generated by the `Parametricity` command.

