# Japanese word frequency

> [!WARNING]
> This is a word-in-progress repository containing data which were not proporly reviewed or cleaned and may contain errors.

## `wordfreq_tatoeba_raw.tsv` file

Contains data obtained from parsing Japanese sentences from [tatoeba.org](https://tatoeba.org/) on 2024-07-04 
using [spaCy](https://spacy.io/) with `ja_core_news_trf` model (slower, more accurate).

Format:

- Tab-separated values
- Header: `lemma<TAB>pos<TAB>count`
- The 1st line after the header contains a special `<total>` value (`pos` set to `-`), representing a total count.
- Format: `{lemma}<TAB>{pos}<TAB>{count}`, where:
  - `lemma` (string) := a lemma of a token, as parsed by the spaCy's parser/lemmatizer. Lemmas can be thought of as "dictionary forms," although they include puctuation, numbers, symbols, etc. For example, nouns "dog" and "dogs" are both lemmatized as "dog" (pos=NOUN), while "dog" in "dog food" would produce a lemma "dog", but with pos=ADJ.
  - `pos` (enum) := part of speech tag, as described in [Universal POS tags](https://universaldependencies.org/u/pos/).
  - `count` (number) := number of occurencies of this lemma.

Notes:

- spaCy's Parser is not 100% accurate, often it produces weird results on phrases with uncommon grammatical structures.
- Lemmas are not necessarily unique, only the pairs of (lemma, pos) are unique.
- Countains proper names, punctuation, symbols, etc.
- Pay special attention to these pos tags when working with this data: PROPN, PUNCT, CURR, SYM, NUM, X.
  - Numerals (pos=NUM) seem to be especially problematic.
  - Proper names (pos=PROPN) include generic names of people often used in sentences on Tatoeba.org, like "Tom" and "Mary".
