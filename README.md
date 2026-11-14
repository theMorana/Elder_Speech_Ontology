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
- [Installation](#installation)
- [Usage](#usage)
- [Data Format](#data-format)
- [Sources & Provenance](#sources--provenance)
- [Known Issues & Caveats](#known-issues--caveats)
- [Contributing](#contributing)
- [Licensing](#licensing)
- [Acknowledgments](#acknowledgments)

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
