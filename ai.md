# Überblick

## Knowledge Based Agents

- central component is a __knowledge base (KB)__
- methoden: ask(), tell()


## Propositional Logic (Aussagenlogik)

An __atomic sentence__ (Aussage) consists of a single proposition __symbol__.
- A sentence can be evaluated as _True_ or _False_.
- Symbols start with uppercase letters, such as _P_, _Q_, _R_, _W12_, _North_, _True_, _False_.
- Examples for atomic sentences:
  - "Paris ist die Hauptstadt von Frankreich"
  - "2 + 2 = 4"
  - "Der Agent steht am Ort (2,3)"
- Complex sentences are built from simpler sentences and connectors. 
- Connectors are _not_, _and_, _or_, _=>_, _<=>_
- Symbols are also called __facts__ ???

A __knowledge base (KB)__ is a collection of sentences.

A model is a possile world
- A model fixes the truth value (T/F) for every propositional symbol (assigment)
- Example: the sentences in a KB make use uf the symbols P11, P22 nd P31. Then one possible model is m1 = {P11=False, P22=False, P31=True}.
- Eine Abbildung I, die jeder Aussagevariablen einen Wahrheitswert zuordnet, heißt __Belegung__ oder __Interpretation__ oder auch __Welt__.
- For a KB with n propositional symbols there are 2^n possible models.
- partial model: an assigment to some of the symbols

Inference
- Decide whether `KB |= α` for some sentence `α`
- Meaning of that symbol: _KB entails α_, _α follows logically from KB_, _α folgt aus KB_
- Simple algorithm for inference is a model-checking approach (truth table): enumerate the models, and check that α is true in every model in which KB is true
- logical equivalence: two sentences α and β are logically equivalent if they are true in the same set of models: `α ≡ β` if and only if `α |= β` and `β |= α`
- hier geht's dann weiter mit Modus Ponens, Horn-Klauseln, konjunktive Normalform, Theorembeweisern, SAT-Problemen, ...
- __Sound__ inference algorithms derive only sentences that are entailed; 
- __complete__ algorithms derive all sentences that are entailed
- Satz2.3 (Widerspruchsbeweis): `KB |= Q` gilt genau dann wenn `WB ∧ ¬Q` unerfüllbar ist.

VSU
- _valid_ (_allgemeingültig_, _wahr_) sentence: true in every possible model, for every possible combination of values. Example: `P or (not P)` is always true, for every possible value of P (auch: Tautologien).  `α ⇒ β`
- _satisfiable_ (_erfüllbar_) sentence: true in some models. 
- _unsatisfiable_ (_unerfüllbar_) sentence: false for all models. Example: `P and (not P)`, `α ∧ ¬β` 
- Jede erfüllende Belegung einer Formel heißt __Modell__

Limitations of propositional logic
- no capability to handle uncertainty
- can talk about true/false facts only
- cannot talk about objects that have properties (size, color, ...)
- cannot talk about relations between objects
- no short-cuts (like making statements for all objects)

### Agents based on Propositional Logic
- KB consists of axioms (general knowledge about how the world works) and percept sentences obtained from the agent's experience in a particular world.
- __Fluent__ refers to an aspect of the world that changes. It is a synonym for __state variable__
- frame problem??? 
- effect axioms???
- __belief state__: some representation of the set of all possible current states of the world
- Logical state estimation involves maintaining a logical sentence that describes the set
of possible states consistent with the observation history. 
- Each update step requires inference using the transition model of the environment, which is built from successor-state axioms that specify how each fluent changes.

## First-Oder Logic (Prädikatenlogik 1. Stufe)


## Representation

| | World | Belief |
| --- | --- | --- |
| First Order Logic | relations, objects, functions | T/F/unknown |
| Propositional Logic | facts (symbols) | T/F/unknown |
| Probability Theory | facts (symbols) | [0...1] |


## Planning Graphs

We now define mutex links forboth actions and literals. A mutex relation 
holds between two actions at a given level if any of the following three 
conditions holds:

- Inconsistent effects: one action negates an effect of the other. 
  For example, Eat(Cake)and the persistence of Have(Cake) have 
  inconsistent effects because they disagree on the effect Have(Cake).
- Interference: one of the effects of one action is the negation of a 
  precondition of the other. For example Eat(Cake) interferes with the 
  persistence of Have(Cake) by negating its precondition.
- Competing needs: one of the preconditions of one action is mutually 
  exclusive with a precondition of the other. Forexample, Bake(Cake) and 
  Eat(Cake) are mutex because they compete on the value of the Have(Cake) 
  precondition.

A mutex relation holds between two literals at the same level if one is the 
negation of the other or if each possible pair of actions that could achieve 
the two literals is mutually exclusive.
This condition is called inconsistent support. For example, Have(Cake) and 
Eaten(Cake) are mutex in S 1 because the only way of achieving Have(Cake), 
the persistence action, is mutex with the only way of achieving Eaten(Cake), 
namely Eat(Cake). In S 2 the two literals are not mutex, because there are 
new ways of achieving them, such as Bake(Cake) and the persistence of 
Eaten(Cake), that are not mutex.