# Rules vs. Constraints

## 1 Non-derivational Approaches to Phonology

Derivational approaches to phonology largely abandoned in favor of non-derivational approaches

- cognitively more plausible

## 1.1 The Constraint

***XAY**  -  where A is the <u>target</u> of the constraint and X and Y are the <u>environment</u>

- ex: *** [-voice] [+voice]**  -  *Surface strings in which a voiceless segment precedes a voiced segment are ill-formed*

Big difference between constraints and rules: **constraints** only determine whether a string is well or ill-formed

- do not themselves specify repairs that should be made to ill-formed strings

## 2 Rules

**Rules:** specify (change) feature values of segments in a string

- ex: **[-cont -voice] → [+ spread glottis] / # _**  -  *Word-initial voiceless plosives are made aspirated*

## 3 Constraints

**Constraints:** prohibit particular structures

- ex: *** [-voice +son]**  -  *A common feature co-occurrence constraint: sonorants should be voiced*
- ex: *** [+cons αvoice] [+cons -αvoice]** - *Adjacent consonants should agree in voicing*

Make **positive well-formedness** statements

- ex: In Hausa the maximal syllable is **CVX**, where X is either C or V

Make **implicational well-formedness** statements

- ex: If syllable-final, then [+sonorant]

## 4 Good Rule / Constraint

1. **Naturalness:** The alternation that a rule performs should be natural; it enforces a surface-true generalization (constraint) or that it is phonetically natural
2. **Locality:** Well-formed rules display locality between trigger and target; segmental adjacency is always local; nonadjacent material can sometimes obey locality from the right perspective

# Optimality Theory

### Traditional Generative Phonology

Input/output mappings are governed by rules (with a few constraints mixed in)

- Input (UR) → { ordered rules } → Output (Surface)

### Optimality Theory

Rules are replaced by universal **constraints** which directly state marked or unmarked patterns

- ex: "front vowels are unrounded" "syllables are open" "voiced obstruents do not occur in codas"

**Markedness:** <u>unmarked</u> preferred; <u>marked</u> values avoided (unmarked)

| Some markedness constraints                    |      |
| ---------------------------------------------- | ---- |
| Syllables must not have codas                  |      |
| Sonorants must be voiced                       |      |
| Vowels must not be nasal                       |      |
| Obstruents must not be voiced in coda position |      |

All constraints are **violable** - does not necessarily cause ungrammaticality

- intinsically in **conflict**
- regulating the outcome of constraint conflicts is based on the relative **ranking** of universal constraints

**Faithfulness:** serves to *preserve lexical contrasts* in the face of pressures from markedness (don't change)

- markedness and faithfulness are inherently **conflicting**

| Some faithfulness constraints                                |          |
| ------------------------------------------------------------ | -------- |
| Deletion of segments is prohibited                           | MAX-IO   |
| Insertion of segments is prohibited                          | DEP-IO   |
| A segment in the input is identical to the corresponding segment in the output | IDENT-IO |
| Output segments and input segments must share values for a feature | AGREE    |

## Implementation of OT: formalism

an *input-output device*

``````
Input → candidates {a, b, c, …} → C1 {a, c, …} → C2 → C3 → Output
``````

- **">>"** connecting two constraints reads as "dominates" - C1 >> C2 >> C3
- Richness of the base: any input is possible
- Parallel evalution: all candidates evaluated in a single pass
- Optimality: a candidate is 'optimal' when it incurs the least serious violations in a set of constraints

### Architecture of an OT grammar

- LEXICON
- GENERATOR (Gen)
- EVALUATOR (Eval)

- **"*"** shows violation marks incurred by each candidate
- **"!"** signals fatal violation

### Dutch and English Example

- *Neutralization of the voicing contrast in Dutch*
  - [bɛt] emerges as the optimal: ***VOICED-CODA >> IDENT-IO(voice)**
- *Preservation of voicing contrast in English*
  - [bɛd] emerges as the optimal: **IDENT-IO(voice) >> *VOICED-CODA**

