# 🇩🇪 Mein Wortschatz

A web app for learning German vocabulary with flashcards and spaced repetition. The dictionary contains
5,112 German words with pronunciation, grammar information, an English translation and an example sentence.
The words are ordered by level (A1 → B2) and, inside each level, by how often they are used.

**Production:** https://jana-dads.github.io/mein-wortschatz/
**Testing (DEV):** https://jana-dads.github.io/mein-wortschatz/dev/

The app is the German sister of [Mon Vocab](https://github.com/Jana-DADS/french-vocab-data) and shares its features:
flashcards, writing practice, spaced repetition, filters by level and topic, pronunciation, automatic vocabulary updates.
German specifics: capital letters count when you type a German word, and buttons for ä ö ü ß Ä Ö Ü are next to the input field.
A noun can be typed with its article (`das Haus`); a wrong article counts as a mistake. On the Update Progress page you can
make the article compulsory.
On a phone the menu hides behind the ☰ button and the app can be added to the home screen. Progress is saved in the browser
of each device separately.

## CSV structure (`german_vocab.csv`)

| Column | Description |
|---|---|
| `id` | Word id. Never renumber: the learner's progress is stored by id. Cards added later get new ids (5001+). |
| `de` | German word (lemma) |
| `pron` | IPA pronunciation |
| `info` | Word class and forms: `n. — das Haus, pl. Häuser`, `v. — geht, ging, ist gegangen`, `adj. — größer, am größten` |
| `en` | English translation |
| `de_sentence` | Example sentence in German |
| `en_sentence` | Example sentence in English |
| `level` | CEFR level: A1 (848), A2 (822), B1 (2039), B2 (1403) |
| `category` | Thematic category (General, Verbs, Food & Drink, Travel, …) |
| `order` | Learning order (1 = first). A card added later stands next to the card it belongs to |
| `added` | Vocabulary version that added the card (empty for the cards of the first release) |

## How the word list was made

1. **Frequency.** A hybrid ranking of spoken and written German: the geometric mean of the relative lemma
   frequencies in film subtitles and in news texts.
2. **Levels.** Words listed in the Goethe-Institut word lists for A1, A2 and B1 have that level. Other words:
   A2 up to hybrid rank 1000, B1 up to rank 2500, B2 beyond.
3. **Basic sets** (numbers, colours, days, months, family, greetings) are placed between positions 100 and 300.
4. **Review.** Every card was read and corrected by hand; proper names, regional (Austrian / Swiss) variants and
   separate feminine job titles were left out.
5. **Version 1.1.** Cards with two unrelated meanings were split into two cards (the new one right after the original
   in the learning order), sentences whose English translation missed the card's meaning were replaced, and some
   English meanings were widened with a synonym.

## Sources and licences

- Word frequencies (spoken): [FrequencyWords](https://github.com/hermitdave/FrequencyWords) from OpenSubtitles, CC BY-SA 4.0
- Word frequencies (written): [Leipzig Corpora Collection](https://wortschatz.uni-leipzig.de/en/download), German news 2025, CC BY 4.0
- Pronunciation, grammar information, translations: [Wiktionary](https://en.wiktionary.org/) via [kaikki.org](https://kaikki.org/), CC BY-SA
- Levels A1–B1: word lists of the Goethe-Institut (used for the level only)
- Example sentences: [Tatoeba](https://tatoeba.org/), CC BY 2.0 FR; 138 sentences were written for this list
- Review of all cards, 138 example sentences, part of the pronunciations and the app itself:
  [Claude](https://claude.ai) (Anthropic) together with the project author

Because Wiktionary and FrequencyWords are share-alike sources, `german_vocab.csv` is published under **CC BY-SA 4.0**.
The app itself (`index.html`: code and design) is © 2026 Jana Dolečková, all rights reserved. See [LICENSE.md](LICENSE.md).

## Versioning

`version.json` has two sections: `vocab` (the CSV) and `app` (the HTML file with its change log). On start the app
compares the stored versions with the ones on GitHub and offers an update. New features are tested in `dev/` first.
