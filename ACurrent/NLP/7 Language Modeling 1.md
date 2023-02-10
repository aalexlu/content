*February 7, 2023*
previous: [[6 Annotation]]

---
Building models that can tell us things in NLP

## Language Model
- Language models provide us with a way to quantify the likelihood of a sequence — i.e., plausible sentences.
- Vocabulary *V* is a finite set of discrete sybols (words, characters); V = | *V* |
- *V+* is the infinite set of sequences of symbols from *V*; each sequence ends with STOP
- x ∈ *V+* (a given sentence)
- P(w) = P(w1, …, wn)
	- P("Call me Ishmail") = P(w1 = “call”, w2 = “me”, w3 = “Ishmael”) x P(STOP)


Optical Character Recognition (OCR) – picture of text, what do the characters / pixels look like
Machine translation (MT)
- fidelity (to source text) how much meaning from the English is in the Italian
- fluency (of the translation)
Autocomplete is language modeling
Speech recognition
Dialogue generation (Q -> A)

Start with an X, come out with a Y
- Given X, give me the probability of Y, so I can pick which Y has the highest probability of being my best guess
|     | X               | Y             |
| --- | --------------- | ------------- |
| ASR | speech signal   | transcription |
| MT  | target text     | source text   |
| OCR | pixel densities | transcription |






---




next:
