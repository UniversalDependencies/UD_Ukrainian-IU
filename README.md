# Summary

Gold standard Universal Dependencies corpus for Ukrainian, developed for UD version 2 originally,
by Institute for Ukrainian, NGO.


# Introduction

UD Ukrainian comprises 100K tokens in 5866 sentences of fiction, news, opinion articles, Wikipedia, legal documents, letters, posts, and comments — from the last 15 years, as well as from the first half of the 20th century.


# Acknowledgments

Major contributors: Natalia Kotsyba, Bohdan Moskalevskyi, Mykhailo Romanenko.

Large portion of anotation was made by Halyna Samoridna, Ivanka Kosovska, Olha Lytvyn, Oksana Orlenko and by students of Kyiv-Mohyla Academy department of Ukrainian language (headed by Liudmyla Dyka): Hanna Brovko, Bohdana Matushko, Natalia Onyshchuk, Valeriia Pareviazko, Yaroslava Rychyk, Anastasiia Stetsenko, Snizhana Umanets.

We thank Prof. Larysa Masenko for guidance.


# Documentation

### Basic stats

| set   | sentences | ~tokens |
| ----- |----------:| -------:|
| train |    4506   |    75K  |
| dev   |     783   |    10K  |
| test  |     577   |    15K  |
| TOTAL |    5866   |   100K  |


### Annotation procedure

Morphology is annotated using 2+1 schema. The syntax is single-pass plus supervisor’s check.
Consistency is further enforced by ~200 validation and autofix rules.


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


### Contact

[org@mova.institute](mailto:org@mova.institute)


### Changelog

* 2018-04-15 **v2.2**
  * Repository renamed from UD_Ukrainian to UD_Ukrainian-IU.

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
