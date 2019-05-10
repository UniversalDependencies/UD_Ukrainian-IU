# Summary

Gold standard Universal Dependencies corpus for Ukrainian, developed for UD originally, by [Institute for Ukrainian](https://mova.institute), NGO.  
[[українською](https://mova.institute/золотий_стандарт)]


# Introduction

UD Ukrainian comprises 122K tokens in 7000 sentences of fiction, news, opinion articles, Wikipedia, legal documents, letters, posts, and comments — from the last 15 years, as well as from the first half of the 20th century.

Consider using [the latest version](https://github.com/UniversalDependencies/UD_Ukrainian-IU/tree/dev) at ‘dev’ branch on GitHub. It contains the latest stable improvements while the official releases are up to 6 month old [[discussion](https://github.com/UniversalDependencies/docs/issues/520)].


# Acknowledgments

Major contributors: Natalia Kotsyba, Bohdan Moskalevskyi, Mykhailo Romanenko.

Large portion of annotation was made by Halyna Samoridna, Ivanka Kosovska, Olha Lytvyn, Oksana Orlenko and by students of Kyiv-Mohyla Academy department of Ukrainian language (headed by Liudmyla Dyka): Hanna Brovko, Bohdana Matushko, Natalia Onyshchuk, Valeriia Pareviazko, Yaroslava Rychyk, Anastasiia Stetsenko, Snizhana Umanets.

We thank Prof. Larysa Masenko for guidance.


# Documentation

**[Project homepage](https://mova.institute/золотий_стандарт)** (in Ukrainian)


### Search

* [Bonito](https://mova.institute/bonito/run.cgi/first_form?corpname=zoloto)
* [Kontext](https://mova.institute/kontext/first_form)
* [Turku depsearch](https://lab.mova.institute/dep_search/)

You can also browse the entire treebank in [Brat](https://lab.mova.institute/brat/#/ud/).


### Stats

| set   | sentences | ~tokens |
| ----- |----------:| -------:|
| train |    5496   |    92K  |
| dev   |     672   |    13K  |
| test  |     892   |    17K  |
| TOTAL |    7060   |   122K  |

See [stats.xml](https://github.com/UniversalDependencies/UD_Ukrainian-IU/blob/dev/stats.xml) for detail.


### Annotation procedure

Morphology is annotated using 2+1 schema. The syntax is single-pass plus supervisor’s check.
Consistency is further enforced by ~300 validation and autofix [rules](https://github.com/mova-institute/lib/blob/master/src/nlp/ud/validation.ts) (see [warnings page](https://lab.mova.institute/files/pomylky_robochoho_tb.html)) and by investigating errors made by a trained parser.


### Data split

Data is split between train/dev/test linearly by hand at 75%/10%/15% to balance in genre and complexity. Some large documents are divided across datasets.


### Format

UD Ukrainian data conforms to [CoNLL-U](http://universaldependencies.org/format.html) format with the following specifics:
* Sentence-level comments:
  * Document boundaries are present as `# newdoc id = xxxx`.
  * Sentence-level paragraph boundaries are present as `# newpar id = xxxx`.
  * Document titles are present as `# doc_title = Назва`.
  * Czech-like translit is present as `# translit = …`.
  * Gaps in the text are marked on the sentences following the gap as:
    * `# annotation_gap` for sentences not exported to CoNLL-U because annotator was unable to parse it with confidence (e.g. new guidelines need to be created);
    * `# gap` for intentional gaps in texts (selected fragments).
* XPOSTAG column contains [MTE](http://nl.ijs.si/ME/V4/msd/html/msd-uk.html) tag with `U` for punctuation. UPOS+FEATS contain all the information in XPOSTAG and more. XPOSTAG is intended for legacy applications.
* DEPS column contains [Enhanced Dependencies](#enhanced-dependencies).
* MISC column:
  * Token-level paragraph boundaries are present as `NewPar=Yes`.
  * Token ids are present as `Id=xxxx`.
  * `SpaceAfter=No` markers are present.
  * Form (`Translit`) and lemma (`LTranslit`) transliterations are present
  * The pipe (`|`) character is escaped with `\p`. Backslash is `\\`. See [issue #569](https://github.com/UniversalDependencies/docs/issues/569).
* Document, paragraph, sentence, and token ids are 4-character base-32 numbers. They survive treebank updates.


### [Enhanced Dependencies](http://universaldependencies.org/u/overview/enhanced-syntax.html)

1. **Ellipsis.** Elided predicates are manually reconstructed with word forms and full morphological info. The TB currently contains ~200 of them.
1. **Propagation of conjuncts.** Conjoined modifiers are propagated automatically. For heterogeneous conjuncts, a relation guesser is employed. Dependents of first conjuncts are propagated only if they are manually marked as shared (40% of such annotation is done).
1. **Controlled/raised subjects.** All `xcomp` subjects are annotated manually as [`nsubj:x`](http://universaldependencies.org/uk/dep/nsubj-x.html)/[`csubj:x`](http://universaldependencies.org/uk/dep/csubj-x.html). Subjects of [`xcomp:sp`](http://universaldependencies.org/uk/dep/xcomp-sp.html) (secondary predication) are [`nsubj:sp`](http://universaldependencies.org/uk/dep/nsubj-sp.html)/[`csubj:sp`](http://universaldependencies.org/uk/dep/csubj-sp.html). The latter are also used for the subjects of [`advcl:sp`](http://universaldependencies.org/uk/dep/advcl-sp.html) (see [#476](https://github.com/UniversalDependencies/docs/issues/476)).
1. **Relative clauses.** All relative clauses are manually annotated with enhanced dependencies. This includes all types mentioned in the [universal docs](http://universaldependencies.org/u/overview/enhanced-syntax.html#relative-clauses) plus Ukrainian clauses that use personal pronouns as relativizers: _вузол, що його не переріжеш_ “the-knot, that it.Acc not you-can-cut”.
1. **Case information.** We don’t case-mark relation names because this doesn’t bring any new information [[discussion](https://github.com/UniversalDependencies/docs/issues/566)].


### Development

Data files are built from sources at [mova-institute/zoloto](https://github.com/mova-institute/zoloto), where the actual development happens.


### Licensing

The data is licensed under [CC BY-NC-SA 4.0](https://creativecommons.org/licenses/by-nc-sa/4.0/) and is free for non-commercial use. For a commercial license, please contact us at [org@mova.institute](mailto:org@mova.institute).


### Contact

[org@mova.institute](mailto:org@mova.institute)


### Changelog

* 2019-05-15 **v2.4**
  * Closed many annotaion gaps: 116K→122K.
  * Fixed annotation errors.
  * Shared more dependents of a first conjunct.
  * Improved consistency by extending annotation guidelines to rarer phenomena.
  * Switched from `ccomp` to `xcomp` where `nsubj:x` is a phantom object.
  * Made clauses with `ADV` relativizers `:relcl`.
  * Added `Polarity=Neg` for conjunctions.
  * Escaped the pipe (`|`) character in `MISC` as `\p`. `\\` is now a backslash.

* 2018-11-15 **v2.3**
  * Added all types of enhanced dependencies except for case-marking, see [Enhanced Dependencies](#enhanced-dependencies) section.
  * Closed many annotation gaps and added new texts: 100→115K.
  * Fixed ~450 annotation errors including _його/її/їх_ `PRON` vs `DET` ambiguity.
  * Improved consistency by extending annotation guidelines to many rarer phenomena.
  * Introduced multitokens for _ні́кого_, _ні́де_ etc.
  * Split words with fused _пів-_ numerals (e.g. _півкласу_) to multitokens.
  * Introduced [`flat:abs`](http://universaldependencies.org/uk/dep/flat-abs.html), [`flat:sibl`](http://universaldependencies.org/uk/dep/flat-sibl.html), [`flat:range`](http://universaldependencies.org/uk/dep/flat-range.html), [`advmod:det`](http://universaldependencies.org/uk/dep/advmod-det.html), [`acl:adv`](http://universaldependencies.org/uk/dep/acl-adv.html), [`parataxis:rel`](http://universaldependencies.org/uk/dep/parataxis-rel.html), [`vocative:cl`](http://universaldependencies.org/uk/dep/vocative-cl.html).
  * Specified `acl:relcl`.
  * Removed `:pass` subtype from relations as it currently can be inferred from the morphology.
  * Added transliteration.
  * Fixed missing `# annotation_gap`s.
  * Updated readme with more description, links.

* 2018-04-15 **v2.2**
  * Renamed the repository from UD_Ukrainian to UD_Ukrainian-IU to match the new UD naming convention.
  * Fixed some validation errors.
  * Added a couple of new sentences.
  * `Orth=Khark` feature renamed to `Orth=Alt`.

* 2017-11-15 **v2.1**
  * Quadrupled the amount of data up to 100K, mostly with nonfiction; improved consistency.
  * Resplitted train/dev/test.

* 2017-02-15 **v2.0**
  * Replaced v1.4 data with 25K tokens of misc genres, mostly fiction.

* 2016-11-01 **v1.4**
  * An initial experimental release containing 1.6K tokens of grammar examples and fiction.

------

```
=== Machine-readable metadata =================================================
Data available since: UD v1.4
License: CC BY-NC-SA 4.0
Includes text: yes
Genre: blog email fiction grammar-examples legal news reviews social web wiki
Lemmas: manual native
UPOS: manual native
XPOS: manual native
Features: manual native
Relations: manual native
Contributors: Kotsyba, Natalia; Moskalevskyi, Bohdan; Romanenko, Mykhailo
Contributing: elsewhere
Contact: org@mova.institute
===============================================================================
```
