# Elder_Speech_Ontology
[![License: MIT](https://img.shields.io/badge/Code-MIT-yellow.svg)](./LICENSE-CODE)
[![License: CC BY-SA 3.0](https://img.shields.io/badge/Data-CC%20BY--SA%203.0-lightgrey.svg)](./LICENSE-DATA)
[![Python 3.10+](https://img.shields.io/badge/python-3.10%2B-blue.svg)](https://www.python.org/)

An open knowledge graph of lexical parallels between **Elder Speech** (the
constructed language from *The Witcher*) and natural languages such as Welsh,
Irish, Italian, Latin, French, German, Dutch, Swedish, Polish, and Romanian.

The project combines a manually curated CSV dataset, an RDF/OWL ontology, and
Python tooling for extraction, verification, and export. It is intended for
linguistic research, digital humanities coursework, and anyone exploring how
constructed fictional languages borrow from real ones.

> ⚠️ **Disclaimer.** This is a research and educational project. It is not
> affiliated with Andrzej Sapkowski, CD Projekt RED, or the Witcher Wiki.
> "Elder Speech", "The Witcher", and related names are trademarks of their
> respective owners. Hypotheses about etymology in this dataset are
> **candidates for human review**, not established facts.

---

## Table of Contents

- [What is Elder Speech?](#what-is-elder-speech)
- [Project Goals](#project-goals)
- [Repository Structure](#repository-structure)
- [Ontology Model](#ontology-model)
- [Sources & Provenance](#sources--provenance)

---

## What is Elder Speech?

**Elder Speech** (also *Hen Llinge*) is the language of the Elves in Andrzej
Sapkowski's *Witcher* saga and its adaptations. Unlike fully constructed
languages such as Sindarin or Klingon, Elder Speech is a **literary pastiche**
— Sapkowski borrowed heavily from Welsh, Irish, Italian, Latin, and other
European languages without building a complete grammar. Later, for the Netflix
series, David J. Peterson developed a more systematic version called **Hen
Linge**.

This makes Elder Speech an interesting case study for:
- identifying lexical borrowing from natural languages,
- distinguishing authorial borrowing from fan-made etymologies,
- modeling uncertainty in linguistic hypotheses.

---

## Project Goals

1. **Collect** Elder Speech lexemes from books, games, the TV series, and
   published glossaries.
2. **Hypothesize** plausible natural-language parallels (source language +
   corresponding form + confidence).
3. **Model** these hypotheses as a formal OWL ontology, so they can be
   queried, extended, and reasoned over.
4. **Preserve provenance**: every parallel keeps its source, confidence level,
   and a human-readable note.
5. **Avoid overclaiming**: no "etymology" is asserted without a confidence
   value and a reference.

---

## Repository Structure

```text
.
├── data/
│ ├── elder_speech_all.csv # raw lexical units from all sources
│ ├── elder_speech_parallels_with_confidence.csv # curated parallels
│ └── ontology_elder_speech_base_english.csv # merged + translated dataset
│
├── ontology/
│ ├── elder_speech_ontology.ttl # RDF/Turtle (open in Protégé)
│ └── elder_speech_ontology.owl # optional OWL/XML export
│
├── notebooks/
│ ├── elder_speech_lexical_parallel_search.ipynb # LLM-assisted hypothesis generation
│ └── ontology_build.ipynb # CSV → TTL conversion
│
├── scripts/
│ ├── build_ontology.py # main pipeline (CSV → TTL)
│ ├── clean_encoding.py # fix \uXXXX and smart quotes
│ └── translate_notes.py # Russian → English notes
│
├── docs/
│ ├── ontology_diagram.png # visual schema
│ └── methodology.md # how hypotheses are scored
│
├── LICENSE-CODE # MIT
├── LICENSE-DATA # CC BY-SA 3.0
└── README.md

```

---

## Ontology Model

The ontology defines the following classes and object properties:

### Classes

| Class | Description |
|---|---|
| `FictionalLanguage` | The constructed language itself (e.g., Elder Speech) |
| `LexicalUnit` | A word or phrase in Elder Speech |
| `Meaning` | The gloss / translation of a lexical unit |
| `LexicalVariant` | Attested spelling or inflectional variant |
| `NaturalLanguage` | A real-world source language (Welsh, Irish, ...) |
| `Source` | A book, game, or wiki article where the unit is attested |
| `LanguageVariant` | A dialect or regional variant of a language |
| `SpeakerCommunity` | Community associated with a language variant |
| `WritingSystem` | Script used by a natural language |
| `CulturalConcept` | A concept linked to the lexeme (e.g., `geis` → taboo) |
| `ParallelForm` | A concrete form in a natural language (e.g., `ap` for `aep`) |

### Object Properties
FictionalLanguage ──hasLexicalUnit──► LexicalUnit

LexicalUnit ──hasMeaning──────► Meaning

LexicalUnit ──hasVariant─────► LexicalVariant

LexicalUnit ──influencedBy───► NaturalLanguage

LexicalUnit ──appearsIn──────► Source


### Datatype Properties

LexicalUnit ── hasCorrespondingForm──► xsd:string

LexicalUnit ── hasConfidence────────► xsd:string (high | medium | low | not_analyzed)

LexicalUnit ── hasReferenceNote─────► xsd:string

ParallelForm ── hasFormString────────► xsd:string

ParallelForm ── hasFormConfidence────► xsd:string


### Example: `aep → ap → Welsh`

```turtle
ex:lu_aep  a ex:LexicalUnit ;
           rdfs:label "aep"@en ;
           ex:influencedBy ex:lang_Welsh ;
           ex:derivedFrom ex:lang_Welsh ;
           ex:hasParallelForm ex:form_aep_Welsh_0 ;
           ex:hasConfidence "high" .

ex:form_aep_Welsh_0  a ex:ParallelForm ;
                     ex:hasFormString "ap" ;
                     ex:formInLanguage ex:lang_Welsh .

ex:lang_Welsh  a ex:NaturalLanguage ;
               rdfs:label "Welsh"@en .

```

Open ontology/elder_speech_ontology.ttl in Protégé
to explore the graph interactively.


### Sources & Provenance
The dataset aggregates material from:

Witcher Wiki — witcher-games.fandom.com/wiki/Elder_Speech
and the Elder Speech Pocket Dictionary / Phrasebook pages.

Sapkowski's novels (Russian editions used as the source of attestations):
The Last Wish, The Sword of Destiny, Blood of Elves,
Time of Contempt, Baptism of Fire, The Tower of the Swallow,
The Lady of the Lake.

Hen Linge materials by David J. Peterson —
dedalvs.com/work/the-witcher/.

All source names in the Source column are normalized to English titles.
Confidence values are assigned based on the strength of the evidence, not
on how popular or well-known the parallel is.
