# Ingush frequency dictionary (PaydaDosh) — version 2026.11

A lemma frequency list of **Ingush** (ГӀалгӀай мотт, ISO 639-3 `inh`), a Nakh language of the North Caucasus,
computed from the PaydaDosh corpus of Ingush texts. Online version with examples: <https://paydadosh.ru/frequency>.

**27,774 words** (lemma + part of speech), ranked by frequency × dispersion across five genres.
The first 1,000 words cover **62–70 %** of the 2.53 million Ingush tokens of the corpus (including unparsed ones), the
first 5,000 — **77–86 %** (lower bound: only tokens resolved unambiguously or by translation; upper: all counted tokens).

| File | Rows | What |
|---|---|---|
| `data/ingush_frequency_2026_11.tsv` | 27,774 | full list |
| `data/ingush_frequency_2026_11_top5000.tsv` | 5,000 | the first 5,000 words (same columns) |

UTF-8, tab-separated, one header row. Ingush text uses the Cyrillic palochka **Ӏ** (U+04C0) everywhere
(the lowercase variant U+04CF does not occur).

## Columns

| Column | Meaning |
|---|---|
| `rank` | place in the list (1 = most important) |
| `lemma` | dictionary form; class verbs are given in their д-form («дала», not «вала/яла/бала») |
| `pos` | part of speech, tag of the PaydaDosh morphological analyzer: `NOUN`, `VERB`, `ADJ`, `ADV`, `PRON`, `NUM`, `MASD` (masdar, verbal noun), `VERB_CAUS` (causative), `VERB_POT` (potential), `CONV` (converb), `ADP` (postposition), `PART` (particle), `CONJ` (conjunction), `INTJ` (interjection), `COP` (copula), `AUX` (auxiliary), `COMPOUND` (hyphenated combination), `X` (not determined) |
| `ipm_balanced` | mean of the per-genre frequencies (per million tokens) × dispersion across genres (Juilland's D); **the list is sorted by this value** |
| `ipm` | raw frequency per million Ingush word tokens of the whole corpus |
| `freq` | token count; ambiguous tokens are split between candidate lemmas, so the value is fractional |
| `freq_sure` | tokens where this lemma was the only analysis |
| `freq_known` | `freq_sure` + tokens resolved by the Russian translation of the sentence (lower bound) |
| `genres` | in how many of the five genres the word occurs (= number of non-zero `ipm_<genre>` columns) |
| `ipm_press`, `ipm_prose`, `ipm_folklore`, `ipm_translation`, `ipm_reference` | frequency per million tokens inside each genre |
| `class_variants` | class forms merged into this lemma, with counts (e.g. «бе:44054, е:6468, ве:3018» for «де») |

## Corpus (snapshot of 20 November 2026)

3,608,027 tokens, of them **2,463,032 Ingush word tokens** (Russian words, numbers and unparsed tokens are
excluded from the counts; proper names are excluded from the list).

| Genre | Ingush tokens | Share |
|---|---|---|
| press | 1,329,032 | 54 % |
| prose | 706,451 | 29 % |
| reference (examples from dictionaries and grammars) | 166,559 | 7 % |
| translation | 162,030 | 7 % |
| folklore | 98,960 | 4 % |

The texts themselves are **not** part of this dataset — only counts.

## Method

1. Every token of the corpus is analysed by the PaydaDosh morphological analyzer (all analyses are kept).
2. **Unit = lemma + part of speech.** Homonyms with the same spelling and part of speech are counted together;
   meanings are not separated.
3. **Ambiguous tokens** (several lemmas with the top analysis confidence) are resolved, in this order:
   by the Russian translation of the sentence when it is available (178,120 sentences have one) — the candidate whose
   dictionary glosses overlap the translation more gets the token; then by the share of the same spelling among
   resolved sentences; otherwise proportionally to how often each candidate occurs unambiguously.
   This makes `freq` of frequent ambiguous lemmas an upper bound — `freq_known` is the lower bound.
4. **Class variants** of verbs with gender/class agreement («вала», «яла», «бала») are merged into the д-form («дала»).
5. **Ranking = frequency × dispersion.** The press is 54 % of the corpus, so raw frequency over-ranks newspaper words.
   The rank uses the mean frequency over genres multiplied by Juilland's D across genres: a word frequent in every
   genre keeps its frequency, a word of one genre goes down.
6. Words of the analyzer lexicon that have a dictionary entry win over form-like pseudo-headwords; Russian words
   without an entry in the dictionary are dropped; proper names recognised by the analyzer and the PaydaDosh onomasticon
   are listed separately on the site and are not here.
7. Cleaning for this release (2,426 items removed and 8 merged; none of the site's first 5,000 words was removed):
   items with digits or Latin letters («1-ча», «u-23», «qr-код»); hyphenated personal and place names and
   route chains («мухьмад-Башир», «Эбарг-Юрт»); hyphenated Russian adjective compounds; items with dictionary
   markup («X / Y», brackets) and multi-word descriptive phrases. Stress marks copied from printed dictionaries are
   removed; lemmas that differed only in palochka case are merged; a sentence-initial capital is lowered unless the word
   is written only with a capital in the dictionary («Даьла», «Тушоли»).

## Known limitations

- No word-sense disambiguation: frequencies of homographs of the same part of speech are joint.
- A few rare proper names may remain in the list; multi-word verbs are kept only as light-verb combinations
  («цӀи тилла», «ладийгӀа дала»).
- `COMPOUND` items are hyphenated combinations as written in the texts («да-нана»); some are fixed expressions,
  some are pairs of words.
- The corpus is dominated by the press; folklore and translations come from a small number of sources.
- This is a snapshot: texts added to the corpus after 20 November 2026 are not counted yet. A new version will follow
  the next rebuild of the corpus index.

## License

**CC BY 4.0** — <https://creativecommons.org/licenses/by/4.0/> (legal code:
<https://creativecommons.org/licenses/by/4.0/legalcode>). Free to use, share and adapt with attribution:
“PaydaDosh Ingush frequency dictionary, version 2026.11, https://paydadosh.ru”.

## How to cite

See `CITATION.cff`, or:

> PaydaDosh (2026). *Ingush frequency dictionary*, version 2026.11. https://github.com/paydadosh/ingush-frequency

## Contact

Questions and corrections: admin@paydadosh.ru · <https://paydadosh.ru> · Telegram <https://t.me/paydadosh>.
Related: [paydadosh-mcp](https://github.com/paydadosh/paydadosh-mcp) — the dictionary as an MCP server for AI assistants.

---

## Кратко по-русски

Частотный словарь ингушского языка PaydaDosh: 27 774 слова (лемма + часть речи) по корпусу из 2,46 млн ингушских
словоупотреблений, место слова — частота × равномерность по пяти жанрам. Первая тысяча слов покрывает 62–70 %
текста. Сами тексты в набор не входят — только числа. Лицензия CC BY 4.0, ссылка на PaydaDosh обязательна.
Онлайн-версия с примерами — <https://paydadosh.ru/frequency>.
