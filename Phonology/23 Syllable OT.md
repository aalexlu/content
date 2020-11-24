# Syllable Structure in Optimality Theory (OT)

**Universal Grammar (UG)**

- innate ability to learn language; we are born with them
- if there are common patterns in language, they must be part of UG
- if there are uncommon patterns, they must not be a part of UG

constraints are ranked: higher a constraint is ranked, the more important it is for that language

**faithfulness constraints:** seek to preserve underlying structure

**markedness constraints:** seek to avoid certain structures or patterns

- common patterns are <u>unmarked</u>
- uncommon patterns are <u>marked</u>

## Hawaiian, English, Berber, Yawelmani Example

***Conclusion: the difference between the languages is the constraint ranking***

- Systems not found: languages where all…
  1. words are made up of consonant clusters followed by vowels
  2. words begin with consonant clusters
  3. syllables begin with vowels
- <u>Constraints</u> needed
  1. ONSET: syllables must have onsets
  2. NOCODA: syllables are open
  3. *COMPLEX: syllable margins are simple (no consonant clusters at margins)
  4. PEAK: every syllable must have a vocalic peak
  5. IDENTV: do not insert or delete vowels
  6. IDENTC: do not insert or delete consonants

**Yawelmani:** *COMPLEX, IDENTC, PEAK >> IDENTV

- violations of NOCODA are ok, but not violations of *COMPLEX and PEAK

| /logw-hin/        | *COMPLEX | IDENTC | PEAK | IDENTV |
| ----------------- | -------- | ------ | ---- | ------ |
| logw.hin          | *!       |        |      |        |
| log.whin          | *!       |        |      |        |
| log.w.hin         |          |        | *!   |        |
| log.hin           |          | *!     |      |        |
| **log.giw.hin** ⟵ |          |        |      | *      |

*IDENTV is lowest ranked so epenthesis is allowed; dotted lines between first three cols*

**English:** IDENTV, PEAK, IDENTC >> *COMPLEX

| /lɪmp-nɛs/     | IDENTV | PEAK | IDENTC | *COMPLEX |
| -------------- | ------ | ---- | ------ | -------- |
| **lɪmp.nɛs** ⟵ |        |      |        | *        |
| lɪm.nɛs        |        |      | *!     |          |
| lɪm.pɨ.nɛs     | *!     |      |        |          |
| lɪm.p.nɛs      |        | *!   |        |          |

*dotted lines between first three cols*

**Berber:** IDENTV, *COMPLEX, IDENTC >> PEAK

## Bulgarian Example

- <u>Constraints</u> needed
  - DEP: no epenthesis
  - PEAK: every syllable must have a vocalic peak
  - *COMPLEXCODA: complex codas are prohibited
  - *COMPLEXONSET: complex onsets are prohibited

**Bulgarian:** PEAK >> DEP >> *COMPLEXCODA >> *COMPLEXONSET

| /grb/      | PEAK | DEP  | *COMPLEXCODA | *COMPLEXONSET |
| ---------- | ---- | ---- | ------------ | ------------- |
| grb        | *!   |      |              |               |
| gərb       |      | *    | *!           |               |
| **grəb** ⟵ |      | *    |              | *             |

*solid line between DEP and COMPLEXCODA*

## Tagalog Infixation Example

- <u>Constraints</u>
  - NOCODA: syllables are open
  - ALIGN-*um*-L: align the left edge of -um- with the left edge of the Prosodic Word

| {um, gradwet}      | NOCODA | ALIGN-*um*-L   |
| ------------------ | ------ | -------------- |
| **um**.grad.wet    | ***!   |                |
| g**um**.rad.wet    | ***!   | g              |
| gr**u.m**ad.wet  ⟵ | **     | g r            |
| gra.**um**.dwet    | **     | g r a!         |
| gra.d**um**.wet    | **     | g r a! d       |
| grad.w**u.m**et    | **     | g r a! d w     |
| grad.we.**um**t    | **     | g r a! d w e   |
| grad.we.t**um**    | **     | g r a! d w e t |

*each star represents one violation of NOCODA*

