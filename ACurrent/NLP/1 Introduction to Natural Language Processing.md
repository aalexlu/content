David Bamman

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
**Annotation project (AP)**
- course covers many of the methods / existing tasks in NLP
- most exciting applications of NLP eyt to be invented
- design a new NLP task and annotate data to support it
- Examples
	- Respect: predictive model mapping text to respect
	- Time: how much literary time is passing in the text of a novel
	- Dogmatism: how much in a reddit comment
- Deliverables
	- AP1: design a new task and gather data to support it
	- AP2: annotate the data, creating labeled examples and guidelines
	- AP3: different group will annotate your data using your guidelines
	- AP4: build a classifier to automatically predict the labelsusing the data you've annotated
**Weekly quizzes**
Midterm
- max(Midterm 1, Midterm 2)
**NLP Subfield survey** (instead of final)
- 4 page survey for a specific NLP subfield of your choice synthesizing at least 25 papers
- give newcomer to the field context

3 late days
cite ChatGPT or Copilot and be clear what code/text came from it