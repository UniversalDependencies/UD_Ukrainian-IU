# Summary

Gold standard Universal Dependencies corpus for Ukrainian, developed for UD originally, by [Institute for Ukrainian](https://mova.institute), NGO.  
[[українською](https://mova.institute/золотий_стандарт)]


# Introduction

UD Ukrainian comprises 100K tokens in 5882 sentences of fiction, news, opinion articles, Wikipedia, legal documents, letters, posts, and comments — from the last 15 years, as well as from the first half of the 20th century.


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
| train |    4518   |    75K  |
| dev   |     577   |    10K  |
| test  |     787   |    15K  |
| TOTAL |    5882   |   100K  |

See [stats.xml](stats.xml) for more detail.


### Annotation procedure

Morphology is annotated using 2+1 schema. The syntax is single-pass plus supervisor’s check.
Consistency is further enforced by ~200 validation and autofix [rules](https://github.com/mova-institute/lib/blob/master/src/nlp/ud/validation.ts) (see [warnings page](https://lab.mova.institute/files/pomylky_robochoho_tb.html)) and by investigating errors made by a trained parser.


### Data split

Data is split between train/dev/test linearly by hand at 75%/10%/15% to balance in genre and complexity. Some large documents are divided across datasets.


### Format

UD Ukrainian data conforms to [CoNLL-U](http://universaldependencies.org/format.html) format with the following specifics:
* Sentence-level comments:
  * Document boundaries are present as `# newdoc id = xxxx`.
  * Sentence-level paragraph boundaries are present as `# newpar id = xxxx`.
  * Document titles are present as `# doc_title = Назва`.
  * Gaps in the text are marked on the sentences following the gap as:
    * `# annotation_gap` for sentences not exported to CoNLL-U because annotator was unable to parse it with confidence (new guidelines need to be created etc.);
    * `# gap` for intentional gaps in texts (selected fragments).
* XPOSTAG column contains [MTE](http://nl.ijs.si/ME/V4/msd/html/msd-uk.html) tag with `U` for punctuation. UPOS+FEATS contain all the information in XPOSTAG and more. XPOSTAG is intended for legacy applications.
* No enhanced dependencies or empty nodes present in DEPS column.
* MISC column:
  * Token-level paragraph boundaries are present as `NewPar=Yes`.
  * Token ids are present as `Id=xxxx`.
  * `SpaceAfter=No` markers are present.
* Document, paragraph, sentence, and token ids are 4-character base-32 numbers. They survive treebank updates.


### Development

Data files are built from sources at [mova-institute/zoloto](https://github.com/mova-institute/zoloto), where actual development happens.


### Licensing

The data is licensed under [CC BY-NC-SA 4.0](https://creativecommons.org/licenses/by-nc-sa/4.0/) and is free for non-commercial use. For a commercial license, please contact us at [org@mova.institute](mailto:org@mova.institute).

### Contact

[org@mova.institute](mailto:org@mova.institute)

### Changelog

* upcoming release
  * Readme updated with more description, links.
  * Removed `:pass` subtype from relations as it currently can be inferred from the morphology.
  * Fixed some annotation errors including _його/її/їх_ `PRON` vs `DET` ambiguity by utilizing a valency dictionary.
  * Closed some annotation holes (added more sentences).
  * Introduced multitokens for ні́де, ні́як.

* 2018-04-15 **v2.2**
  * Repository renamed from UD_Ukrainian to UD_Ukrainian-IU to match the new UD naming convention.
  * `Orth=Khark` feature renamed to `Orth=Alt`.
  * Fixed some validation errors.
  * Added a couple of new sentences.

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
Genre: news fiction legal social wiki web email
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
