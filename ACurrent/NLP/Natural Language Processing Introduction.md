### Core Ideas

---

## NLP

Interdisciplinary
- AI, ML, Linguistics (rep of language), Social sciences
Processing language with computers
- 'processing' as understanding
Turing test: distinguishing human vs. computer only through written language
Where we are now
- Siri: lack of state information / persistence
- ChatGPT

Uses:
- machine translation
- question answering
- information extraction
- conversational agents
- summarization

---

## What makes language hard?

- language is a complex social process
- tremendous ambiguity at every level of representation
- modeling it is AI-complete (requires first solving AI)

Speech acts ("can you pass the salt?")
- statement that does not elicit a response
Conversational implicature ("The opera singer was amazing; she sang all of the notes.")
- describes the bare minimum; implies not that good
- ChatGPT doesn't understand the conversational implicature
Shared knowledge ("Warren ran for president")
- depends on context such as when this was said
Variation/Indexicality ("This homework is wicked hard")

Most difficult aspects to solve:
- Ambiguity ("One morning I shot an elephant in my pajamas")
	- due to syntax
	- "shot" could refer to gun, camera, basketball

---

processing as representation
- NLP generally involves representing language for some end, whether dialogue, translation, speech recognition, or text analysis

views on language models
Information theoretic view
- encode(X) -> decode(encode(X))
- sent along communication channel
Rational speech act view
- Communication involves recursive reasoning: how can X choose words to maximize understanding Y?
Pragmatic view
- Meaning is co-constructed by the interlocutors and the context of the utterance
Whorfian view:
- Weak relativism: structure of language influences thought.

---

## Decoding

*One morning I shot an elephant in my pajamas*
*I didn't shoot an elephant*

Different representations
- discourse, semantics, syntax, morphology, words
- parts of speech, named entities, syntax
syntactic structure useful for sentiment analysis

---

## NLP + X

Computational Social Science
- inferring ideal points of politicians based on voting behavior, speeches
- detecting triggers of censorship in blogs/social media
- inferring power differentials in language use
Computational Journalism
Computational Humanities

---

## Methods

- finite state automata/transducers (tokenization, morphological analysis)
- rule-based systems
- probabilistic models
- naive bayes, logistic regression, HMM, MEMM, CRF, language models
- dynamic programming (combining solutions to subproblems)
- dense representations for features/labels (inputs and outputs)
- neural networks: multiple, highly parameterized layers of (usually non-linear) interactions mediating the input/output
- latent variable models (specify probabilistic strcture between variables and inferring likely latent values)
- pretrained models

---

## This class

- about models and linguistic representation of text

Homeworks
**Annotation project**
- course covers many of the met
**Weekly quizzes**
Midterm
**NLP Subfield survey**
