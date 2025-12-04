# UNIT II: NATURAL LANGUAGE PROCESSING AND MULTI-AGENT SYSTEMS

## Comprehensive Master's Level Study Material

---

## TABLE OF CONTENTS

1. [Natural Language Processing](#1-natural-language-processing)
   - 1.1 Overview of Linguistics
   - 1.2 Grammar and Language
   - 1.3 Parsing Techniques
   - 1.4 Semantic Analysis
   - 1.5 Pragmatics
2. [Multi-Agent Systems](#2-multi-agent-systems)
   - 2.1 Agents and Objects
   - 2.2 Agents and Expert Systems
   - 2.3 Generic Structure of Multiagent Systems
   - 2.4 Semantic Web
   - 2.5 Agent Communication
   - 2.6 Knowledge Sharing Using Ontologies
   - 2.7 Agent Development Frameworks

---

# 1. NATURAL LANGUAGE PROCESSING

## 1.1 Overview of Linguistics

### 1.1.1 Fundamental Concepts

**Natural Language Processing (NLP)** is the branch of artificial intelligence and computational linguistics concerned with the interaction between computers and human language. NLP aims to enable computers to:

- **Understand**: Comprehend meaning of spoken or written text
- **Interpret**: Derive appropriate interpretations considering context
- **Generate**: Create coherent and meaningful language
- **Translate**: Convert between different languages
- **Analyze**: Extract information and structure from language

**Linguistics** is the scientific study of human language, including its structure, use, evolution, and cognitive processing. Linguistics provides theoretical foundations for NLP by describing how language works.

### 1.1.2 Levels of Linguistic Analysis

Linguistic analysis operates at multiple interconnected levels, from individual sounds to discourse structure:

#### 1.1.2.1 Phonology and Phonetics

**Phonology** (Sound Systems):

```
Definition: Study of how sounds are organized systematically in language

Key Concepts:
├── Phoneme: Smallest unit of sound that distinguishes meaning
│   ├── /p/ and /b/ are different phonemes
│   ├── Changing /p/ to /b/ changes meaning (pat → bat)
│   └── Variation within phoneme (allophone): /t/ sounds different in "city" vs "stop"
│
├── Prosody: Suprasegmental features above individual sounds
│   ├── Stress: Emphasis on syllables (COMment vs coMMENT)
│   ├── Intonation: Pitch variation (Statement vs Question?)
│   └── Timing: Duration and pacing of speech
│
└── Phonological Rules: Systematic patterns of sound organization
    ├── Assimilation: sounds become more similar (in+possible → impossible)
    ├── Dissimilation: sounds become more different
    └── Coarticulation: sounds influenced by neighboring sounds
```

**Phonetics** (Physical Sound Properties):

```
Study of actual physical properties of sounds:

├── Articulation: How sounds are produced
│   ├── Place: Where in vocal tract (labial, dental, velar)
│   ├── Manner: How air flows (stops, fricatives, liquids)
│   └── Voicing: Whether vocal cords vibrate
│
├── Acoustic Properties:
│   ├── Frequency: Pitch (fundamental frequency)
│   ├── Duration: Length of sound
│   └── Amplitude: Loudness
│
└── Formants: Resonant frequencies in vowel sounds
    ├── F1: Tongue height (high/low vowel)
    ├── F2: Tongue front/back position
    └── F3: Additional fine detail
```

**Application in NLP**:
- Speech recognition (converting sound to phonemes)
- Text-to-speech synthesis (converting phonemes to sound)
- Accent and dialect analysis
- Confidence in speech processing

#### 1.1.2.2 Morphology

**Definition**: Study of word structure and formation; how words are built from meaningful units.

**Core Concepts**:

```
1. Morpheme: Smallest meaningful unit of language
   
   Free Morphemes (can stand alone):
   ├── Lexical: "cat", "run", "blue" (carry semantic content)
   └── Grammatical: "the", "and", "to" (grammatical function)
   
   Bound Morphemes (cannot stand alone):
   ├── Prefix: re-, un-, pre- (before root)
   ├── Suffix: -ing, -ed, -ness, -tion (after root)
   └── Infix: -um- in "l-um-imit" in Tagalog (within root)

2. Morphological Processes:
   
   Inflection (Change grammatical properties):
   ├── Verb tense: walk → walked, walking
   ├── Noun number: cat → cats
   ├── Adjective agreement: big → bigger, biggest
   └── Doesn't create new word, same word with variation
   
   Derivation (Create new words):
   ├── Add derivational affixes: happy → unhappy
   ├── friend + -ship → friendship (new word, different meaning/part-of-speech)
   ├── compute + -er → computer (new word)
   └── Creates genuinely new lexical items
   
   Compounding (Combine words):
   ├── Combining two independent words
   ├── Examples: blackboard, notebook, wheelchair
   ├── May have single stress or dual stress
   └── Meaning may be compositional or non-compositional
   
   Conversion (Shift word class without affixation):
   ├── "Google" (noun) → "Google it" (verb)
   ├── "walk" (verb) → "take a walk" (noun)
   └── Implicit morphological change

3. Allomorphy: Variant forms of same morpheme
   ├── Plural morpheme: cat-s, dog-s, church-es, ox-en
   ├── Past tense: walk-ed, stop-ped, cut-Ø
   └── Context-dependent pronunciation/spelling
```

**Morphological Typology** (Language Classification):

```
Languages classified by how morphemes combine:

Analytic Languages:
├── Minimal morphemes per word (often 1)
├── Information expressed through word order and function words
├── Examples: English (somewhat), Chinese (very analytic)
└── Sentence: "The cat is sleeping"
    Each concept separate word

Synthetic Languages:
├── Multiple morphemes per word
├── Information packed into single words
├── Examples: Latin, Finnish, Turkish
└── Divided into:

   Agglutinative Languages:
   ├── Each morpheme = single function
   ├── Morphemes clearly separable
   ├── Example (Turkish):
   │   ev-ler-im-de (house-PL-1st.POSS-LOC)
   │   "in my houses" - each suffix is distinct
   └── Examples: Japanese, Korean, Finnish, Turkish
   
   Fusional/Inflectional Languages:
   ├── Morphemes fused, hard to separate
   ├── Single morpheme = multiple functions
   ├── Example (Latin):
   │   reg-ina (queen) contains:
   │   - "reg" = root
   │   - "-ina" = singular + nominative (both functions)
   └── Examples: Latin, Spanish, Russian
```

**Application in NLP**:
- Stemming: Reducing words to root form (running → run)
- Lemmatization: Reducing to dictionary form (better → good)
- Named entity recognition: Identifying morphological patterns
- Language generation: Correct morphological inflection
- Spell checking: Recognizing morphologically valid words

#### 1.1.2.3 Syntax

**Definition**: Study of how words combine into phrases and sentences; structure of sentences.

**Core Concepts**:

```
Syntax Studies:

1. Phrase Structure:
   How words organize into increasingly larger units
   
   Hierarchical Structure:
   
       Sentence
          |
      ┌───┴───┐
     NP      VP
    (Noun   (Verb
    Phrase) Phrase)
     |       |
    Det N   V NP
    |  |    |  |
   "The cat ate fish"
   
   Tree captures grammatical relationships:
   ├── Subject (the cat) vs. Predicate (ate fish)
   ├── Object of verb (fish)
   └── Hierarchical structure more important than linear order

2. Constituents and Dependencies:
   
   Constituent Structures (constituency parsing):
   ├── Groups of words form meaningful units
   ├── Units can be moved/replaced as block
   ├── Example: "The cat" can replace "It" (both are NPs)
   └── Recursive: NPs contain other constituents
   
   Dependency Structures (dependency parsing):
   ├── Focus on head-dependent relationships
   ├── Every word depends on exactly one head
   ├── Example: "quickly" depends on "ran" (modifies verb)
   └── May be faster to compute than full parsing

3. Grammatical Relations:
   ├── Subject: Who/what performing action
   ├── Object: Who/what receiving action
   ├── Indirect Object: Recipient (give book to Mary)
   ├── Modifier: Words that modify other words
   └── Different languages encode differently
```

**Syntactic Properties**:

```
1. Word Order:
   ├── SVO (Subject-Verb-Object): English, Chinese
   │   "The cat ate fish"
   ├── SOV (Subject-Object-Verb): Japanese, Korean, Turkish
   │   "The cat fish ate"
   ├── VSO (Verb-Subject-Object): Arabic, Irish
   │   "Ate the cat fish"
   └── Other orderings possible

2. Agreement:
   Elements must match in grammatical properties
   ├── Subject-Verb Agreement:
   │   "The cat runs" (verb agrees with singular subject)
   │   NOT "The cat run"
   ├── Gender/Number Agreement (many languages):
   │   Spanish: "el gato negro" (masc.sing. agreement)
   └── Case Agreement (many languages)

3. Recursion:
   Structures can contain same structure type
   ├── Sentence can contain sentence
   ├── "John said [that Mary believes [that dogs bark]]"
   ├── Enables infinite generative capacity
   └── Key property enabling productivity of language

4. Ambiguity:
   Single string can have multiple parses
   
   Structural Ambiguity:
   ├── "I saw the man with the telescope"
   ├── Parse 1: "I saw [the man with the telescope]"
   │   (man has telescope)
   ├── Parse 2: "I [saw the man] with the telescope"
   │   (I used telescope to see man)
   └── Context and world knowledge resolve
```

**Application in NLP**:
- Parsing: Determining sentence structure
- Grammar checking: Ensuring proper syntax
- Machine translation: Mapping between syntactic structures
- Information extraction: Using syntax to find relationships
- Question answering: Understanding syntactic structure of query

#### 1.1.2.4 Semantics

**Definition**: Study of meaning; how expressions convey meaning.

**Levels of Semantic Analysis**:

```
1. Lexical Semantics (Word Meaning):
   
   Semantic Relations:
   ├── Synonymy: Similar meaning
   │   (big, large, huge - degrees of similarity)
   │
   ├── Antonymy: Opposite meaning
   │   (big ↔ small, good ↔ bad)
   │
   ├── Polysemy: Single word, multiple related meanings
   │   "bank" = financial institution OR side of river
   │   Meanings related (place where things accumulate)
   │
   ├── Homonymy: Same form, completely different meanings
   │   "bank" (financial) vs. "bark" (tree covering)
   │   Historically unrelated
   │
   ├── Hypernymy/Hyponymy: General to specific
   │   Hypernym: animal (general)
   │   Hyponym: dog, cat (specific types)
   │   "dog" is a type of "animal"
   │
   └── Meronymy/Holonymy: Part-whole relation
       Meronym: finger (part)
       Holonym: hand (whole)
       "finger" is part of "hand"

2. Sentence Semantics (Compositional Meaning):
   
   How word meanings combine:
   ├── Compositionality Principle:
   │   Meaning of whole = meaning of parts + how combined
   │   "The dog ate the bone"
   │   = [dog] + [eat] + [bone] + [agent-patient relation]
   │
   ├── Semantic Roles (Thematic Roles):
   │   "John gave Mary a book"
   │   - John: AGENT (giver)
   │   - Mary: RECIPIENT (receiver)
   │   - book: THEME (object transferred)
   │
   ├── Truth Conditions:
   │   Statement's meaning partly defined by when it's true
   │   "Snow is white" true iff snow actually is white
   │
   └── Reference and Sense:
       Reference: What word refers to
       Sense: Meaning/definition
       "Morning star" and "Evening star"
       Same reference (Venus), different sense

3. Textual Semantics (Discourse Meaning):
   
   How meaning emerges across multiple sentences
   ├── Coherence: Logical flow and sense
   ├── Reference Resolution: What pronouns refer to
   ├── Temporal Structure: Events in time sequence
   └── Causal Relations: Why things happen

4. Semantic Features:
   Decompose meaning into features:
   
   Example: "woman"
   ├── [+human]
   ├── [+adult]
   ├── [-male]
   └── [+female]
   
   Used for semantic anomaly detection:
   "I saw a colorless green idea"
   - Violates semantic features (colorless but green?)
```

**Application in NLP**:
- Word sense disambiguation: Determining which meaning intended
- Semantic role labeling: Identifying participants in events
- Paraphrase detection: Recognizing same meaning different words
- Information extraction: Understanding relationships
- Question answering: Matching question to appropriate answer

#### 1.1.2.5 Pragmatics

**Definition**: Study of how context affects interpretation; how language is used in communication.

**Key Concepts**:

```
1. Speech Acts (Performatives):
   
   Utterances perform actions beyond literally stating facts:
   
   ├── Assertives: Stating something as fact
   │   "Snow is white" (committing to truth)
   │
   ├── Directives: Requesting action
   │   "Pass the salt" (request, not question about ability)
   │   "Can you open the window?" (polite request)
   │
   ├── Commissives: Committing to future action
   │   "I promise to help" (committing to action)
   │
   ├── Expressives: Expressing emotional state
   │   "I'm delighted!" (expressing emotion)
   │
   └── Declaratives: Changing state of world
       "I pronounce you married" (creates state)
       "You're fired" (changes employment status)

2. Conversational Implicature:
   
   Meaning beyond literal words, derived from context:
   
   Gricean Maxims (Cooperative Principle):
   ├── Quantity: Provide appropriate information
   │   Not too little: "Would you like tea or coffee?"
   │             → "Coffee" (full response expected)
   │   Not too much: "What time is it?" 
   │             → "3 o'clock" (not whole family history)
   │
   ├── Quality: Be truthful
   │   "The weather is beautiful" 
   │   Speaker believes this (or else violates maxim)
   │
   ├── Relation: Be relevant
   │   "What do you think of the president?"
   │   Response about president is relevant
   │   Response about weather violates relevance
   │
   └── Manner: Be clear and orderly
       Use clear vocabulary and organization
       Avoid unnecessary obscurity
   
   Violating Maxims Can Convey Meaning:
   ├── Flouting: Violate for effect
   │   "John has been working very hard: he's very tired"
   │   Violates Relation (seems unrelated)
   │   Implicates: Hard work causes tiredness
   │
   ├── Sarcasm: Violating Quality
   │   "Oh, that's a great idea!" (when actually bad)
   │   Ironic violation signals opposite meaning
   │
   └── Understatement:
       "That's not bad" (when actually excellent)
       Violates Quantity to create emphasis

3. Reference Resolution:
   
   What do pronouns and definite descriptions refer to?
   
   Coreference:
   ├── "John met Mary. He was happy"
   │   "He" refers to John
   │   Both refer to same entity (coreferent)
   │
   ├── "The bank is on the corner. It has ATMs"
   │   "It" refers to "the bank"
   │
   ├── Ambiguity Resolution:
   │   "John and Mary went to market. He bought milk"
   │   Who is "he"?
   │   → Context suggests John (subject of first sentence)
   │
   └── Complex Cases:
       "John gave Mary a book. It was red"
       "It" = book (object passed)
       NOT John or Mary

4. Discourse Structure:
   
   How utterances relate across conversation:
   
   ├── Turn-taking: Speaker switch patterns
   ├── Topic: What being discussed and changes
   ├── Focus: What's in current attention
   ├── Coherence Relations:
   │   - Explanation: "Why?"
   │   - Contrast: "But"
   │   - Elaboration: "For example"
   │   - Narration: Temporal sequence
   └── Discourse Particles: "Well", "Now", "However"

5. Presupposition:
   
   Assumed background information:
   
   ├── "The king of France is bald"
   │   Presupposes: France has a king
   │   Asserts: That king is bald
   │
   ├── "John stopped smoking"
   │   Presupposes: John was smoking before
   │
   └── Presupposition Failure:
       If presupposition false, sentence odd
       (Not simply false, but pragmatically strange)
```

**Application in NLP**:
- Dialogue systems: Understanding speaker intentions
- Intent recognition: Determining what user wants
- Question answering: Understanding genuine question intent
- Sentiment analysis: Understanding implied opinions
- Machine translation: Preserving pragmatic force
- Coreference resolution: Linking pronouns to referents

---

## 1.2 Grammar and Language

### 1.2.1 Grammatical Frameworks

**Grammar** is a formal specification of rules that define valid sentences in a language.

#### 1.2.1.1 Context-Free Grammars (CFG)

**Definition and Notation**:

```
Context-Free Grammar (CFG):
- Consists of production rules
- Format: A → α where:
  * A = non-terminal (left side of rule)
  * α = string of terminals and non-terminals (right side)

Non-terminals: Abstract categories
├── S (Sentence)
├── NP (Noun Phrase)
├── VP (Verb Phrase)
├── N (Noun)
└── V (Verb)

Terminals: Actual words
├── "cat"
├── "dog"
├── "runs"
└── "chased"

Grammar Example:
S → NP VP                     (Sentence = NP + VP)
NP → Det N                    (Noun phrase = Determiner + Noun)
NP → Det Adj N
VP → V NP                     (Verb phrase = Verb + NP)
VP → V                        (Verb phrase = just Verb)
Det → "the" | "a"             (Determiner = "the" OR "a")
N → "cat" | "dog"
V → "chased" | "saw"
Adj → "big" | "small"
```

**Deriving Sentences**:

```
Derivation of "the cat chased a dog":

Start: S

Apply S → NP VP
  NP VP

Apply NP → Det N to first NP
  Det N VP

Apply Det → "the"
  "the" N VP

Apply N → "cat"
  "the" "cat" VP

Apply VP → V NP
  "the" "cat" V NP

Apply V → "chased"
  "the" "cat" "chased" NP

Apply NP → Det N
  "the" "cat" "chased" Det N

Apply Det → "a"
  "the" "cat" "chased" "a" N

Apply N → "dog"
  "the" "cat" "chased" "a" "dog"

Result: Valid sentence derived from grammar
```

**Parse Tree Representation**:

```
                    S
                   / \
                  /   \
                NP     VP
               / \     / \
              /   \   /   \
            Det    N  V     NP
            |      |  |    / \
           "the"  "cat" "chased" Det  N
                              |      |
                             "a"   "dog"
```

**Properties**:

```
Advantages:
├── Simple and intuitive
├── Well-understood mathematically
├── Efficient parsing algorithms exist
├── Can represent many English constructions
└── Formal foundation with clear semantics

Limitations:
├── Cannot capture context-sensitive phenomena
│   Example: Number/gender agreement across sentences
├── Overgenerate: Produce ungrammatical sentences
│   Example: "Colorless green ideas sleep furiously"
│   (Grammatically valid but semantically odd)
├── Undergenerate: Fail to produce grammatical sentences
│   Example: MV-NP-V construction in Dutch
├── Center embedding creates combinatorial explosion
│   "The rat the cat chased attacked the mouse"
│   (Grammatically valid but very hard to parse)
└── Frame/garden-path problems hard to model
```

#### 1.2.1.2 Dependency Grammars

**Core Concept**:

```
Words related through grammatical dependencies rather than phrases

Example Structure:
Sentence: "The dog chased the cat"

Dependency Graph:
        chased (ROOT)
        /  |  \
      dog the cat
      |       |
     The     The

Each word depends on one head (except root)
Multiple dependencies from single head possible
Shows grammatical functions directly
```

**Advantages and Applications**:

```
Advantages:
├── More directly shows grammatical relations
├── Flexible for free word-order languages
├── Often easier to extract relations from
├── Can be faster to compute than constituent parsing
└── Natural for many linguistic phenomena

Applications:
├── Information extraction (finding relationships)
├── Machine translation (aligning dependencies across languages)
├── Question answering (finding relevant semantic relations)
└── Semantic role labeling
```

#### 1.2.1.3 Feature-Based Grammars

```
Grammars with features/attributes on constituents

Example:
NP [number: singular] → Det[number: sg] N[number: sg]
NP [number: plural] → Det[number: pl] N[number: pl]

Features Can Encode:
├── Morphological: number, person, tense, case
├── Syntactic: category, agreement requirements
├── Semantic: selection restrictions
└── Pragmatic: information status (given/new)

Advantages:
├── Elegant way to handle agreement
├── Encodes linguistic constraints
├── Reduces rule proliferation
├── Natural for many linguistic phenomena
└── Foundation for more sophisticated formalisms
```

#### 1.2.1.4 Transformational Grammar

```
Proposes two levels of structure:

Deep Structure (Underlying):
- Logical structure reflecting meaning
- Active voice, straightforward relations

Surface Structure (Actual):
- What's actually said/written
- After transformations applied

Example - Passive:
Deep: [Subject: dog] [Verb: chase] [Object: cat]
Transformation: Passive transformation applied
Surface: "The cat was chased by the dog"

Transformations Can:
├── Rearrange word order
├── Add/remove elements
├── Change grammatical category
└── Are reversible (mostly)

Advantages:
├── Captures generalizations across constructions
├── Explains why certain transformations possible
├── Provides unified account of related sentences

Disadvantages:
├── Complex and hard to formalize computationally
├── Psychological reality questioned
├── More specific to particular language theories
└── Hard to implement in NLP systems
```

---

## 1.3 Parsing Techniques

### 1.3.1 Parsing Overview

**Definition**: Process of analyzing sequence of words to determine grammatical structure according to formal grammar.

**General Process**:

```
Input: Sequence of words
       "The cat chased the dog"
         ↓
Tokenization: Breaking into tokens
       ["The", "cat", "chased", "the", "dog"]
         ↓
Lexical Analysis: Look up word properties
       [Det, N, V, Det, N]
         ↓
Syntactic Parsing: Determine structure
       (Parse tree or dependency structure)
         ↓
Output: Grammatical structure
       S(NP(Det N) VP(V NP(Det N)))
```

**Parsing Challenges**:

```
1. Ambiguity:
   Multiple valid parses for same input
   "I saw the man with the telescope"
   
   Parse 1:        Parse 2:
   S               S
   / \             / \
  NP  VP          NP  VP
  |   / \         |   / \
  I  V   NP       I  (V  NP)_with_telescope
        / \              / \
      NP  PP            NP  PP
       |  |              |  |
      man with          man with
           |                 |
      the telescope    the telescope
   
   Must select most likely parse

2. Garden-path sentences:
   "The horse raced past the barn fell"
   - Initially appears incomplete (raced past barn falls)
   - Actually grammatical: "The horse [raced past the barn] fell"
   - Parser initially takes wrong path, must backtrack

3. Computational complexity:
   Number of parses can exponentially grow
   Parsing can be NP-hard for worst-case grammars
   Must use heuristics and restrictions
```

### 1.3.2 Top-Down Parsing

**Principle**: Start with start symbol (S), expand using grammar rules toward leaf nodes (words).

**Algorithm**:

```pseudocode
function TopDownParse(words, grammar):
    stack ← [S]                          // Start with start symbol
    position ← 0                         // Position in word sequence
    
    while stack not empty:
        top ← stack.pop()
        
        if top is terminal:              // Actual word
            if top == words[position]:
                position ← position + 1
            else:
                BACKTRACK or FAIL
        
        else:                            // Non-terminal (category)
            get rules for non-terminal
            for each rule top → rule_body:
                try expanding with this rule
                push rule_body onto stack
                if parse succeeds:
                    return success
            BACKTRACK
    
    if position == length(words):
        return SUCCESS (complete parse)
    else:
        return FAILURE
```

**Example Trace**:

```
Grammar:
  S → NP VP
  NP → Det N
  VP → V NP
  Det → "the"
  N → "cat" | "dog"
  V → "chased"

Input: "the cat chased the dog"
Tokens: [the, cat, chased, the, dog]

Step 1: Start with S
  Stack: [S]

Step 2: Expand S using S → NP VP
  Stack: [NP, VP]
  Push order: VP first (top), then NP

Step 3: Try expanding NP using NP → Det N
  Stack: [Det, N, VP]

Step 4: Check Det matches "the"
  Matches! Consume token
  Position: 0 → 1
  Stack: [N, VP]

Step 5: Check N matches "cat"
  Matches! Consume token
  Position: 1 → 2
  Stack: [VP]

Step 6: Expand VP using VP → V NP
  Stack: [V, NP]

Step 7: Check V matches "chased"
  Matches! Consume token
  Position: 2 → 3
  Stack: [NP]

Step 8: Expand NP using NP → Det N
  Stack: [Det, N]

Step 9: Check Det matches "the"
  Matches! Consume token
  Position: 3 → 4
  Stack: [N]

Step 10: Check N matches "dog"
  Matches! Consume token
  Position: 4 → 5
  Stack: []

All tokens consumed! Parse successful.
```

**Characteristics**:

```
Advantages:
├── Intuitive: Directly implements grammar
├── Can incorporate semantic information early
├── Can use goal information to focus search
└── Natural for hand-written parsers

Disadvantages:
├── Backtracking required for ambiguity
├── Can explore dead ends extensively
├── Inefficient for ambiguous grammars
├── Left recursion causes infinite loops
└── Left factoring required to avoid backtracking
```

### 1.3.3 Bottom-Up Parsing (Shift-Reduce)

**Principle**: Start with leaf nodes (words), build up tree toward root (S) using grammar rules.

**Algorithm**:

```pseudocode
function BottomUpParse(words, grammar):
    stack ← []                          // Will hold terminals and non-terminals
    buffer ← words                      // Words to process
    
    while buffer not empty or can reduce:
        if grammar_rule matches stack_top:
            REDUCE: Pop rule's RHS, push LHS
        else:
            SHIFT: Pop word from buffer, push onto stack
    
    if stack.size == 1 and stack[0] == S:
        return SUCCESS
    else:
        return FAILURE
```

**Detailed Algorithm**:

```pseudocode
Stack: Initially empty
Buffer: Sequence of words to process

repeat:
    if top of stack matches RHS of some rule:
        REDUCE:
            Pop N elements (RHS of rule)
            Push LHS of rule
    else:
        SHIFT:
            If buffer not empty:
                Pop word from buffer
                Push onto stack
            else:
                Error

until:
    Stack contains S and buffer empty
    (Success)
    OR
    No applicable rule and cannot shift
    (Failure)
```

**Example Trace**:

```
Grammar (same as before):
  S → NP VP
  NP → Det N
  VP → V NP
  Det → "the"
  N → "cat" | "dog"
  V → "chased"

Input: "the cat chased the dog"
Tokens: [the, cat, chased, the, dog]

Step 1: Shift "the"
  Stack: [the]
  Buffer: [cat, chased, the, dog]

Step 2: Shift "cat"
  Stack: [the, cat]
  Buffer: [chased, the, dog]

Step 3: Reduce by Det → "the"
  Stack: [Det, cat]
  Buffer: [chased, the, dog]

Step 4: Reduce by N → "cat"
  Stack: [Det, N]
  Buffer: [chased, the, dog]

Step 5: Reduce by NP → Det N
  Stack: [NP]
  Buffer: [chased, the, dog]

Step 6: Shift "chased"
  Stack: [NP, chased]
  Buffer: [the, dog]

Step 7: Reduce by V → "chased"
  Stack: [NP, V]
  Buffer: [the, dog]

Step 8: Shift "the"
  Stack: [NP, V, the]
  Buffer: [dog]

Step 9: Shift "dog"
  Stack: [NP, V, the, dog]
  Buffer: []

Step 10: Reduce by N → "dog"
  Stack: [NP, V, N]
  Buffer: []

Step 11: Reduce by NP → Det N
  Wait, need Det first...
  Actually: Reduce by Det → "the" first? But it's not on top...
  (This shows bottom-up parsing complexity)
```

**Characteristics**:

```
Advantages:
├── Can handle more grammar classes efficiently
├── LR parsing more powerful than LL
├── Can incorporate semantic actions during reduction
├── Good for precedence-based parsing
└── No left recursion problems

Disadvantages:
├── Shift-Reduce conflicts: Don't know when to reduce
├── Reduce-Reduce conflicts: Multiple applicable rules
├── Requires lookahead to decide
├── More complex than top-down
├── Harder to implement without parser generator
```

### 1.3.4 Predictive Parsing (LL Parsing)

**Principle**: Use lookahead to predict which rule to apply without backtracking.

**Requirements**:

```
LL(k) Grammar (Left-to-right, Leftmost derivation, k-symbol lookahead):

Requires:
├── No ambiguity in predicting rule from lookahead
├── No left recursion
├── Left factoring completed
└── Grammar formatted for predictive parsing

FIRST Sets: First terminals of rule RHS
  FIRST(NP → Det N) = {terminals that Det can start}
  FIRST(Det → "the" | "a") = {"the", "a"}

FOLLOW Sets: Terminals that can follow a non-terminal
  FOLLOW(NP) = terminals that can follow NP in any rule
  If S → NP VP, and VP starts with V
  Then V ∈ FOLLOW(NP)
```

**Algorithm**:

```pseudocode
function PredictiveParser(words, parsing_table):
    stack ← [EOF_MARKER, S]             // Start symbol on stack
    input ← words + [EOF_MARKER]
    current_pos ← 0
    
    while stack not empty:
        top ← stack.pop()
        current ← input[current_pos]
        
        if top is terminal:
            if top == current:
                current_pos ← current_pos + 1
            else:
                error("Expected " + top)
        
        else:                           // top is non-terminal
            if (top, current) in parsing_table:
                rule ← parsing_table[top][current]
                push rule.RHS onto stack (in reverse order)
            else:
                error("No rule for " + top + ", " + current)
    
    if current_pos == length(input):
        return SUCCESS
    else:
        return FAILURE
```

**Parsing Table Construction**:

```
For each rule A → α:
  For each terminal in FIRST(α):
    Add rule A → α to M[A, terminal]
  If ε ∈ FIRST(α):
    For each terminal in FOLLOW(A):
      Add rule A → α to M[A, terminal]

Example:
Grammar:
  S → NP VP
  NP → "the" N
  VP → V NP
  N → "cat" | "dog"
  V → "chased"

Parsing Table:
        |  "the" | "chased" | EOF
--------|--------|----------|------
  S     | NP VP  |    -     |  -
  NP    |Det N   |    -     |  -
  VP    |   -    |  V NP    |  -
  N     | "cat"  |    -     |  -
        | "dog"  |    -     |  -
  V     |   -    |"chased"  |  -

No ambiguity: Each cell has at most one entry
```

**Characteristics**:

```
Advantages:
├── Deterministic: No backtracking needed
├── Linear time: O(n) where n = input length
├── Efficient implementation
├── Can directly build parse tree or AST
└── Good for many languages

Disadvantages:
├── LL(1) grammars limited expressiveness
├── May require left factoring (artificial transformation)
├── Cannot handle left recursion
├── Some natural grammars not LL(1)
└── Requires lookahead information
```

### 1.3.5 LR Parsing

**Principle**: Shift-Reduce parsing with precomputed state machine (parsing tables).

**LR Parser Characteristics**:

```
LR = Left-to-right scan, Right-most derivation (in reverse)

LR(k) Parsers:
├── LR(0): No lookahead (simplest)
├── SLR(1): Simple LR with 1-token lookahead
├── LALR(1): Look-Ahead LR (practical middle ground)
└── LR(1): Full LR with 1-token lookahead (most powerful)

Key Advantage:
├── Can handle wider class of grammars
├── More powerful than LL
├── Still linear time O(n)
├── Practical for real programming languages
└── Used in yacc/bison parser generators
```

**Algorithm Structure**:

```
Components:
├── State Stack: Track parsing states
├── Input Buffer: Words to parse
├── Action Table: Whether to shift/reduce based on state & lookahead
├── Goto Table: Next state after reduce

Parser Actions:
├── Shift: Push input token onto stack
├── Reduce: Pop RHS of rule, push LHS
├── Accept: Parse complete
└── Error: Invalid input
```

**Characteristics**:

```
Advantages:
├── More powerful grammar class
├── Efficient: Linear time
├── Deterministic parsing
├── Few grammar restrictions
├── Standard in practice (yacc, bison)
└── Can handle complex languages

Disadvantages:
├── Complex to understand
├── Difficult to build tables manually
├── Requires parser generator tools
├── Table construction can be slow
├── Error recovery more complex
└── Debugging harder than top-down
```

### 1.3.6 Chart Parsing

**Principle**: Dynamic programming approach tracking completed and partial parses.

**Algorithm**:

```
Chart: Matrix storing partial and complete parses
  Rows: Starting position
  Columns: Ending position
  Cells: Parses spanning that range

Example: Parsing "the cat chased"
Chart:
         0    1    2    3
       ┌─────────────────┐
     0 │ the  cat chased │
     1 │     [Det] [N]   │
     2 │     [NP]        │
     3 │     [V]         │
     4 │              [?]│
       └─────────────────┘

Entries:
- (0,1): "the" = Det
- (1,2): "cat" = N
- (2,3): "chased" = V
- (0,2): "the cat" = NP (from Det + N)
```

**Advantages**:

```
├── Handles ambiguity efficiently
├── Can reuse computation
├── Natural for all parsing strategies
├── Good for speech recognition
├── Can track multiple hypotheses
└── Efficient for ambiguous grammars
```

---

## 1.4 Semantic Analysis

### 1.4.1 From Syntax to Meaning

**Process**:

```
Syntactic Structure → Semantic Representation
    Parse tree      →    Meaning

Two approaches:

1. Syntax-Driven Semantics:
   ├── Compute meaning based on syntactic structure
   ├── Each syntactic rule has associated semantic rule
   ├── Meaning built compositionally as parse tree built
   └── Most common approach

2. Direct Semantic Interpretation:
   ├── Parse and interpret simultaneously
   ├── Don't build explicit parse tree
   ├── More efficient for simple sentences
   └── Harder to debug and explain
```

### 1.4.2 Semantic Representations

#### 1.4.2.1 First-Order Logic Representations

```
Translating natural language to logical form:

Example: "Every dog has a master"
Logical form: ∀x [Dog(x) → ∃y (Master(y, x))]
             For all x: if x is dog, then there exists y who masters x

Translation Process:
- "every" → ∀ (universal quantifier)
- "a" → ∃ (existential quantifier)
- "dog" → Dog(x) (predicate)
- "master" → Master(y, x) (relation)
- "has" → indicates relationship

Complex Example: "Some student passed every exam"

Ambiguous! Two interpretations:

Reading 1 (Existential inside):
  ∃x [Student(x) ∧ ∀y (Exam(y) → Passed(x, y))]
  There exists a student who passed all exams

Reading 2 (Existential outside):
  ∀y [Exam(y) → ∃x (Student(x) ∧ Passed(x, y))]
  For each exam, some student passed it (may be different)

Scope ambiguity: Order of quantifiers matters!
```

**Advantages and Limitations**:

```
Advantages:
├── Formal semantics: Precise meaning
├── Can use logical inference engines
├── Truth conditions clearly defined
├── Enables inference

Limitations:
├── Human language often ambiguous
├── Difficult to capture all nuances
├── Common sense reasoning hard to express
├── Performance/time complexity issues
├── Grounding problem: How connect symbols to world?
```

#### 1.4.2.2 Semantic Role Representations

```
Focus on who does what to whom (thematic roles):

Semantic Roles:
├── Agent: Typically subject; doer of action
├── Patient: Typically object; affected by action
├── Instrument: Tool or means of action
├── Location: Where action occurs
├── Beneficiary: Who benefits from action
├── Source: Origin of action/change
├── Goal: Destination or endpoint
└── Experiencer: Conscious participant in event

Example: "John used a hammer to build a house"
- John: Agent (does action)
- hammer: Instrument (tool used)
- house: Patient/Theme (thing built)
- to build: Action
- Location: Could be implicit

Semantic Role Labeling (SRL):
Task of automatically identifying roles

Example Input: "The ball was kicked by John in the park"
Output:
- The ball: Patient (kicked)
- John: Agent (did kicking)
- park: Location

Applications:
├── Information extraction
├── Question answering
├── Machine translation
└── Event extraction
```

#### 1.4.2.3 Conceptual Representations

```
Conceptual Graphs (hybrid of logic and semantic networks):

Example: "John gave Mary a book"

Representation:
    [GIVE]-
            ->(AGENT)->[PERSON: John]
            ->(RECIPIENT)->[PERSON: Mary]
            ->(OBJECT)->[BOOK]
            ->(TIME)->[NOW]

Nodes: Concepts (GIVE, PERSON, BOOK)
Edges: Conceptual Relations (AGENT, RECIPIENT, OBJECT)
Values in brackets: Specific instances

Advantages:
├── Hybrid: Combines logic and networks
├── Interpretable: Graphical representation
├── Efficient inference
└── Good for knowledge representation

Example: "A cat is on a mat"

    [CAT]->(ON)->[MAT]
         ->(INSTANCE OF)->[FELINE]
         ->(COLOR)->[COLOR: black]
```

### 1.4.3 Semantic Analysis Tasks

#### 1.4.3.1 Word Sense Disambiguation

**Problem**: Words have multiple meanings; determine which meaning intended.

```
Example: "bank"
Sense 1: Financial institution
Sense 2: Side of river

Sentence: "I went to the bank today"
Context needed to determine which sense

Methods:
├── Knowledge-Based:
│   ├── Use word relationships in lexical database
│   ├── Similar-sense neighbors help disambiguate
│   └── Example: "river", "water" suggest riverside
│
├── Supervised Learning:
│   ├── Train classifier with labeled examples
│   ├── Features from context
│   └── Can be accurate but requires labeled data
│
└── Unsupervised Learning:
    ├── Cluster contexts where word appears
    ├── Each cluster = likely word sense
    └── No training data needed but less accurate

Lesk Algorithm (Knowledge-based):
1. Get word's definitions from dictionary
2. Get definitions of nearby words in text
3. Count overlaps between definitions
4. Choose sense with highest overlap

Example:
Word: "bank", Sentence: "I went to the bank by the river"

bank Sense 1 definition: "financial institution where money is deposited"
bank Sense 2 definition: "side of river or stream"

Nearby words: river (supports Sense 2)

Compare overlaps:
- Sense 1 definition vs. nearby words: low overlap
- Sense 2 definition mentions "river": high overlap!

Result: Sense 2 (riverside) selected
```

#### 1.4.3.2 Semantic Role Labeling

```
Automatically identify predicate and its arguments:

Example: "John baked a cake yesterday"

Predicate: "bake"
Arguments:
  - John: A0 (Agent)
  - cake: A1 (Patient)
  - yesterday: ARGM-TMP (Temporal modifier)

Machine Learning Approach:
1. Identify predicate (verb)
2. Identify arguments (noun phrases)
3. Label each argument with semantic role

Features used:
├── Syntax: Position in parse tree relative to verb
├── Verb: Which verb determines possible roles
├── Argument: What argument type (NP, PP, etc.)
├── Context: Surrounding words
└── Voice: Active vs. passive affects roles

Applications:
├── Information extraction: "Who did what?"
├── Machine translation: Map roles between languages
├── Question answering: Find arguments matching query
└── Summarization: Extract key participant roles
```

---

## 1.5 Pragmatics

### 1.5.1 Pragmatic Phenomena in NLP

#### 1.5.1.1 Reference Resolution (Coreference)

**Problem**: Determine what entities pronouns and descriptions refer to.

```
Example:
"John met Mary. He told her he was leaving."

Coreference:
- "He" refers to "John" (same entity)
- "her" refers to "Mary"
- Second "he" refers to "John"

Coreference Links:
John (1st mention) --(coreference)-- He, he (pronouns)
Mary (1st mention) --(coreference)-- her (pronoun)

Challenges:

1. Multiple Candidates:
   "The doctor examined the patient. She was satisfied."
   Who is "she"?
   - doctor (female doctor) → 50% probability
   - patient (female patient) → 50% probability
   
   Use: Gender, number, semantic plausibility

2. Bridging References:
   "We went to a restaurant. The waiter was rude."
   - "waiter" not previously mentioned
   - But "waiter" bridges from "restaurant"
   - Establishment-related people associated with place

3. Discourse-New References:
   "I got in a car. The steering wheel was broken."
   - "steering wheel" not previously mentioned
   - Part-of relationship: steering wheel part of car
   - Inferred from world knowledge

Methods:

Decision-Tree Based:
├── Priority to closest mention (recency)
├── Matching agreement (number, gender)
├── Semantic plausibility (must make sense)
└── Salience (main characters mentioned first)

Machine Learning:
├── Pairwise linking: Probability anaphor refers to antecedent
├── Features: distance, agreement, semantic
├── Clustering: Group coreferent mentions
└── Modern: Neural networks with attention
```

#### 1.5.1.2 Implicature and Figurative Language

```
Non-Literal Meaning:

1. Sarcasm:
   "Oh, that's just great!" (when actually bad)
   Surface: Positive statement
   Implied: Negative opinion
   
   Detection:
   ├── Sentiment contradiction (positive words, negative context)
   ├── Incongruity with situation
   ├── Speaker tone (if voice data available)
   └── World knowledge

2. Metaphor:
   "Time is money" 
   Surface: Equation (nonsensical literally)
   Implied: Time has value like money
   
   Understanding:
   ├── Map properties from source (money) to target (time)
   ├── Money can be spent → time can be spent
   ├── Money is valuable → time is valuable
   └── Money can be saved → time can be saved

3. Hyperbole:
   "I'm dying of hunger"
   Surface: Death from hunger (literally false)
   Implied: Extremely hungry
   
   Recognition:
   ├── Obvious exaggeration
   ├── Intensification for effect
   └── Part of normal speech

4. Idioms:
   "Kick the bucket" (means die, not literal action)
   "Break a leg" (means good luck, not injury)
   
   Processing:
   ├── Cannot be understood word-by-word
   ├── Require lookup in idiom dictionary
   ├── Often language/culture specific
   └── Challenging for NLP systems

Recognition Methods:
├── Pattern matching: Match known phrasings
├── Semantic inconsistency detection
├── Context analysis: What makes sense?
└── Learning: Train on examples
```

#### 1.5.1.3 Discourse and Coherence

```
How utterances relate across document:

Discourse Relations:

1. Explanation:
   "John was sick. That's why he didn't come."
   - Second sentence explains first
   - Causal relation

2. Contrast:
   "John is tall. Mary is short."
   - Sentences describe opposite properties
   - Comparison relation

3. Elaboration:
   "John likes cars. He especially loves sports cars."
   - Second provides detail about first
   - Refinement relation

4. Narration:
   "John went to the store. He bought milk."
   - Sequence of events
   - Temporal ordering

5. Parallel:
   "John plays violin. Mary plays piano."
   - Similar structure but different details
   - Analogical relation

Discourse Markers Signal Relations:
├── "because" → Explanation
├── "but" → Contrast
├── "for example" → Elaboration
├── "then" → Narration (temporal)
├── "similarly" → Parallel
└── Absence of marker requires inference

Coherence:
Make discourse "hang together"

Local Coherence (sentence to sentence):
├── Topic continuity: What being discussed?
├── Entity chains: Same entities mentioned repeatedly
├── Temporal continuity: Events in sensible order
└── Causal chains: Events connected causally

Global Coherence (whole document):
├── Document structure: Introduction, body, conclusion
├── Theme/thesis: Main point clear
├── Progression: Ideas developed logically
└── Unity: All parts support main point

Measuring Coherence:
├── Entity grid: Track entity mentions across sentences
├── Discourse graph: Relations between segments
├── LSA (Latent Semantic Analysis): Semantic similarity
└── Neural methods: Learn coherence patterns
```

---

# 2. MULTI-AGENT SYSTEMS

## 2.1 Agents and Objects

### 2.1.1 Defining Agents

**Agent** in AI: Autonomous entity that perceives environment and acts to achieve goals.

#### 2.1.1.1 Key Agent Properties

```
1. Autonomy:
   ├── Operates without direct human intervention
   ├── Makes decisions independently
   ├── Has own goals/objectives
   └── Can take initiative

2. Perception:
   ├── Senses environment through sensors
   ├── Receives perceptual input
   ├── May have incomplete/uncertain information
   └── Builds internal model of world

3. Action:
   ├── Can perform actions in environment
   ├── Actions affect world state
   ├── May have limited action repertoire
   └── Consequences of actions impact future perception

4. Reactivity:
   ├── Responds to environmental changes
   ├── Sensitivity to dynamic conditions
   ├── Can adapt to new situations
   └── Real-time response capability

5. Proactivity:
   ├── Takes initiative toward goals
   ├── Not just reactive to stimuli
   ├── Plans future actions
   ├── Anticipates problems
   └── Goal-directed behavior

6. Social Ability:
   ├── Can communicate with other agents
   ├── Can cooperate with others
   ├── Negotiates when interests differ
   └── Follows protocols for interaction

7. Learning Capacity:
   ├── Improves performance over time
   ├── Learns from experience
   ├── Adapts to new situations
   └── Develops new strategies

8. Intentionality:
   ├── Has beliefs about world
   ├── Has desires/goals
   ├── Has intentions (commitment to action)
   └── Mental states drive behavior
```

#### 2.1.1.2 Agent vs. Object

```
Fundamental Distinction:

Object (Traditional OOP):
├── Passive: Responds when methods called
├── Encapsulation: Data + methods bundled
├── No inherent goals
├── Communication: Method invocation (request-response)
├── Control: External (caller determines sequence)
├── Example: Window object in GUI
│   - hasSize(), hasColor() properties
│   - draw(), refresh() methods
│   - Passively waits for method calls

Agent:
├── Active: Takes initiative
├── Autonomy: Independent decision-making
├── Has goals: Pursues objectives
├── Communication: Autonomous messaging
├── Control: Internal (agent decides next action)
├── Example: Software agent managing email
│   - Perceives: New emails arrive
│   - Decides: Which to process first
│   - Acts: Filters, prioritizes, forwards
│   - Initiates actions without external trigger

Code Example:

Object Approach:
```
class Account {
    money: double
    
    withdraw(amount) {
        if (amount <= money)
            money -= amount
    }
}

user.account.withdraw(100)  // User must explicitly call
```

Agent Approach:
```
class MoneyAgent {
    goal: maintain(balance > MIN)
    
    perceive() {
        sense_current_balance()
    }
    
    decide() {
        if balance < MIN:
            raise_alert()
    }
    
    act() {
        if alert:
            notify_user()
    }
    
    // Agent independently monitors without external calls
}
```

Key Differences:

| Aspect | Object | Agent |
|--------|--------|-------|
| Invocation | External (called) | Self-initiated |
| Goals | None | Has objectives |
| Initiative | None (passive) | Proactive |
| Persistence | Per method call | Continuous |
| Decision-making | Simple | Complex reasoning |
| Communication | Synchronous method calls | Asynchronous messages |
| Control flow | Caller determines | Agent determines |
```

### 2.1.2 Agent Architectures

#### 2.1.2.1 Reactive Architecture

```
Simplest agent type: Direct stimulus-response

Structure:
    Environment
        ↓ (Perception)
    Sensors/Percepts
        ↓
    [IF-THEN Rules]
        ↓
    Action Selection
        ↓ (Action)
    Effectors/Actions
        ↓
    Environment Changed

No memory: Doesn't remember past states
No planning: Responds immediately to current stimulus
No reasoning: Simple rule matching

Example: Obstacle-avoiding robot

Rule 1: IF obstacle_ahead THEN turn_left
Rule 2: IF clear_path THEN move_forward
Rule 3: IF target_found THEN move_toward_target

Simple reflex agent behavior:
1. Perceive obstacle
2. Match to Rule 1
3. Execute: Turn left
4. Perceive new situation
5. Repeat

Characteristics:
├── Advantage: Very fast
├── Advantage: Simple to implement
├── Advantage: Predictable behavior
├── Disadvantage: Cannot handle complex situations
├── Disadvantage: Easily fooled (e.g., infinite loop)
├── Disadvantage: No learning
├── Disadvantage: No planning ahead

When to Use:
├── Real-time systems requiring immediate response
├── Simple tasks with clear condition-action mapping
├── Resource-constrained environments
└── Safety-critical systems where complexity risky
```

#### 2.1.2.2 Deliberative Architecture

```
Complex reasoning-based agents

Structure:
    Environment
        ↓ (Perception)
    Sensors/Percepts
        ↓
    Internal World Model
        ↓
    [Goal Setting]
    [Planning/Reasoning]
    [Decision Making]
        ↓
    Action Selection
        ↓ (Action)
    Effectors/Actions
        ↓
    Environment Changed
    (Cycle repeats, model updated)

Key Components:

1. World Model:
   ├── Internal representation of environment
   ├── Beliefs about state and relationships
   ├── Historical information
   └── Updated as new percepts arrive

2. Planning:
   ├── Generate sequence of actions toward goal
   ├── Consider multiple alternatives
   ├── Evaluate expected outcomes
   └── Select best plan

3. Reasoning:
   ├── Logical inference about world
   ├── Predict consequences of actions
   ├── Evaluate validity of beliefs
   └── Handle uncertainty

Example: Medical diagnosis agent

1. Perceive: Patient symptoms
2. Model: Consult knowledge base of diseases
3. Reason: Which disease consistent with symptoms?
4. Plan: What tests would distinguish candidates?
5. Decide: Which test order most informative?
6. Act: Request test

Characteristics:
├── Advantage: Handles complex situations
├── Advantage: Can plan ahead
├── Advantage: Flexible (can change goals)
├── Advantage: Can learn/improve models
├── Disadvantage: Slower (requires reasoning)
├── Disadvantage: More complex to implement
├── Disadvantage: Requires domain knowledge
├── Disadvantage: May miss time-critical responses

When to Use:
├── Complex problem-solving required
├── Multiple interacting goals
├── Long-term planning needed
├── Flexibility and adaptation important
└── Time not strictly critical
```

**BDI Architecture** (Belief-Desire-Intention):

```
Specific deliberative approach combining:

├── Beliefs:
│   ├── Agent's knowledge about world
│   ├── May be uncertain/incorrect
│   ├── Updated by perception
│   └── Support reasoning

├── Desires:
│   ├── What agent wants to achieve
│   ├── May conflict (wants both X and Y, contradictory)
│   ├── Prioritized/weighted
│   └── Motivation for action

└── Intentions:
    ├── Commitments to particular goals
    ├── Subset of desires agent committed to
    ├── Guide behavior over time
    ├── More specific than desires
    └── Chosen after deliberation

Reasoning Process:

1. Perceive world → Update beliefs
2. Recognize opportunities/problems
3. Deliberate: Which desires pursue?
4. Determine: Which desires can be fulfilled?
5. Decide: Commit to specific goals (intentions)
6. Plan: How to achieve intentions?
7. Execute: Attempt plan
8. Monitor: Are intentions still valid?
9. If plan fails: Revise plan
10. If intention impossible: Abandon, reconsider desires

Example: Robot with BDI

Beliefs:
├── Location: At home
├── Battery level: 30%
├── Charger location: Kitchen
└── Task assigned: Clean room

Desires:
├── Charge battery (energy level > 70%)
├── Clean room (complete assigned task)
├── Socialize with other robots
├── Minimize energy use

Deliberation:
├── Goal conflict: Clean room vs. charging
├── Constraint: Battery at 30%, cleaning needs ~60%
├── Decision: Charge first (necessary), then clean

Intentions:
├── I will go to kitchen
├── I will charge
├── Once charged, I will clean room

Execution:
└── Follow plan until completion or events change situation
```

#### 2.1.2.3 Hybrid Architecture

```
Combines reactive and deliberative components

Structure:
    Environment
         ↓
    Perception Layer
         ↓
    ┌────────────────────┐
    │ REACTIVE LAYER     │ ← Fast immediate responses
    │ (Rules, reflexes)  │
    └────────────────────┘
         ↓
    ┌────────────────────┐
    │ DELIBERATIVE LAYER │ ← Strategic planning
    │ (Planning, reasoning)
    └────────────────────┘
         ↓
    Action Selection
    (Coordinate both layers)
         ↓
    Effectors
         ↓
    Environment

Interaction Between Layers:

1. Normal Operation:
   ├── Deliberative layer plans long-term strategy
   ├── Reactive layer handles routine situations
   └── Both contribute to action selection

2. Emergency:
   ├── Reactive layer takes over immediately
   ├── Bypasses slow deliberative layer
   ├── Example: Obstacle detected → immediate avoidance
   └── Deliberative layer resumes once crisis passes

3. Goal Modification:
   ├── Deliberative layer may override reactive rules
   ├── New strategic decision requires fresh plan
   ├── Reactive layer adapts to new strategy
   └── Continuous dialogue between layers

Example: Autonomous vehicle

Reactive Layer Rules:
├── IF obstacle_detected → brake immediately
├── IF pedestrian_crossing → slow down
├── IF traffic_light_red → stop
└── IF stopped_vehicle_ahead → maintain distance

Deliberative Layer (Planning):
├── Route planning: A to B most efficiently
├── Fuel management: Where to refuel
├── Schedule management: Arriving on time
└── Risk assessment: Avoid dangerous areas

Coordination:
├── Deliberative layer sets route
├── Reactive layer handles moment-to-moment safety
├── If accident ahead: Reactive overrides planned route
├── Deliberative recalculates once emergency passed

Characteristics:
├── Advantage: Fast responses when needed
├── Advantage: Long-term planning capability
├── Advantage: Graceful degradation (works even if deliberative fails)
├── Advantage: Can learn from experience
├── Disadvantage: Complex implementation
├── Disadvantage: Coordination between layers tricky
├── Disadvantage: Debugging harder
├── Disadvantage: Tuning layer interaction difficult
```

---

## 2.2 Agents and Expert Systems

### 2.2.1 Integration of Agent Capabilities with Expert Systems

**Expert Systems** (Rule-Based Knowledge Systems):
```
Traditional Expert System:
├── Static knowledge base
├── Inference engine
├── User interacts through interface
├── System passive until queried
└── No goal-directed behavior
```

**Agent-Based Expert Systems**:
```
Enhanced Expert System with Agent Capabilities:
├── Proactive problem-solving
├── Autonomous operation
├── Goal-directed reasoning
├── Can communicate with other agents
├── Learns from experience
└── Adapts to changing environments
```

### 2.2.2 Knowledge Management in Agent Systems

```
Agent Using Expert System Knowledge:

Agent Architecture:
    Perception
         ↓
    Knowledge Base (Expert System Knowledge)
         ↓
    Inference Engine (Forward/Backward Chaining)
         ↓
    Decision Making (Which conclusion most relevant to goal?)
         ↓
    Action Selection
         ↓
    Environment

Example: Diagnostic Agent

Knowledge Base:
├── Rule1: IF fever AND cough THEN respiratory_infection (CF:0.8)
├── Rule2: IF fever AND cough AND chest_pain THEN pneumonia (CF:0.9)
└── ... (hundreds more)

Agent Operation:
1. Goal: Diagnose patient
2. Perceive: Patient symptoms (fever, cough)
3. Reason: Apply relevant rules from knowledge base
4. Conclude: Most likely diagnosis (pneumonia)
5. Act: Recommend treatment based on diagnosis
6. Learn: Track outcomes, refine rules if needed

Agent Value Over Static Expert System:
├── Can proactively monitor multiple patients
├── Can coordinate with other diagnostic agents
├── Can prioritize cases (critically ill first)
├── Can improve through experience
├── Can adapt as new treatments discovered
└── Can operate independently
```

---

## 2.3 Generic Structure of Multiagent Systems

### 2.3.1 System Components

```
Multi-Agent System (MAS) Architecture:

┌────────────────────────────────────────────┐
│         Multi-Agent Platform               │
├────────────────────────────────────────────┤
│  Platform Services                         │
│  ├── Agent Management (lifecycle)          │
│  ├── Service Directory (agent discovery)   │
│  ├── Communication Infrastructure          │
│  └── Execution Environment                 │
├────────────────────────────────────────────┤
│  ┌──────────┐ ┌──────────┐ ┌──────────┐  │
│  │ Agent 1  │ │ Agent 2  │ │ Agent 3  │  │ Autonomous Agents
│  │┌────────┐│ │┌────────┐│ │┌────────┐│  │
│  ││ Goal   ││ ││ Goal   ││ ││ Goal   ││  │
│  ││ Reason ││ ││ Reason ││ ││ Reason ││  │
│  ││ Act    ││ ││ Act    ││ ││ Act    ││  │
│  │└────────┘│ │└────────┘│ │└────────┘│  │
│  └──────────┘ └──────────┘ └──────────┘  │
├────────────────────────────────────────────┤
│  Communication & Coordination Layer        │
│  ├── Message passing                       │
│  ├── Protocol management                   │
│  ├── Coordination mechanisms                │
│  └── Conflict resolution                   │
├────────────────────────────────────────────┤
│  Shared Resources / Environment            │
│  ├── Databases / Knowledge stores          │
│  ├── Physical environment (for robots)     │
│  └── Shared tools/services                 │
└────────────────────────────────────────────┘
```

### 2.3.2 Agent Communication and Coordination

#### 2.3.2.1 Basic Concepts

```
Agent Types:
├── Manager/Coordinator: Oversees others
├── Specialist: Domain expertise
├── Information: Gathers/provides data
├── Interface: User interaction
└── Resource: Controls external resources

System Organizations:

1. Flat (Peer-to-Peer):
   All agents at same level
   ┌─── Agent1
   ├─── Agent2
   ├─── Agent3
   └─── Agent4
   
   Characteristics:
   ├── No central control
   ├── Peer negotiation
   ├── Scalable but complex coordination
   └── Robust (no single point of failure)

2. Hierarchical:
   Manager oversees subordinates
         Manager
        /   |   \
      Sub1 Sub2 Sub3
   
   Characteristics:
   ├── Clear authority
   ├── Easier coordination
   ├── Bottleneck at top
   └── Single point of failure

3. Heterogeneous:
   Mixed agent types with different roles
   
   Specialists:
   ├── Negotiator (handles agreements)
   ├── Mediator (resolves disputes)
   ├── Monitor (tracks performance)
   └── Facilitator (enables communication)
```

#### 2.3.2.2 Agent Interaction Patterns

```
Interaction Types:

1. Cooperation:
   Agents work toward shared goal
   
   Example: Emergency Response
   ├── Police agent: Traffic control
   ├── Fire agent: Rescue operations
   ├── Medical agent: Emergency care
   └── Shared goal: Minimize harm
   
   Challenge: Coordinate without conflicts

2. Coordination:
   Agents synchronize to achieve efficiency
   
   Example: Manufacturing
   ├── Shipping agent: Package orders
   ├── Warehouse agent: Prepare goods
   ├── Billing agent: Issue invoices
   └── Goal: Seamless order fulfillment
   
   Challenge: Right sequence, no bottlenecks

3. Negotiation:
   Agents exchange offers to reach agreement
   
   Example: Resource Allocation
   ├── Agent A: "I need 10 CPUs for 1 hour"
   ├── Agent B: "I have 8 CPUs available"
   ├── Agent A: "Can you get 2 more from elsewhere?"
   ├── Agent B: "Yes, for double price"
   ├── Agent A: "Acceptable"
   └── Agreement: 10 CPUs for 2x cost
   
   Challenge: Fair outcomes, converging to agreement

4. Competition:
   Agents compete for limited resources
   
   Example: Auction System
   ├── Item for sale
   ├── Bidder1: $100
   ├── Bidder2: $120
   ├── Bidder1: $130
   ├── Winner: Bidder1 at $130
   └── Goal: Maximize selling price / get item cheaply
   
   Challenge: Fair mechanisms, no collusion
```

---

## 2.4 Semantic Web

### 2.4.1 Semantic Web Vision

**Goal**: Machine-understandable web where:
- Information has explicit meaning
- Computers can process information meaningfully
- Automated reasoning and integration possible
- Better integration across heterogeneous sources

### 2.4.2 Resource Description Framework (RDF)

#### 2.4.2.1 Core Concepts

**RDF Triple**: Fundamental statement unit

```
Subject - Predicate - Object
│        │          │
└─Resource  Relation  Value

Examples:

Triple 1:
  Subject: http://example.org/person/john
  Predicate: http://xmlns.com/foaf/0.1/name
  Object: "John Smith"

English: "John Smith's name is John Smith" (simplified)

Triple 2:
  Subject: http://example.org/person/john
  Predicate: http://xmlns.com/foaf/0.1/knows
  Object: http://example.org/person/mary

English: "John knows Mary"

Triple 3:
  Subject: http://example.org/person/john
  Predicate: http://purl.org/dc/terms/created
  Object: "2024-01-15" (literal value)

English: "John created something on 2024-01-15"
```

#### 2.4.2.2 RDF Graph Structure

```
RDF is directed graph: vertices (subjects/objects) and edges (predicates)

Example: Person Information

    http://example.org/john
    /                |              \
   /                 |               \
name="John"   knows→mary         age="35"

Represented as triples:
1. (john, name, "John")
2. (john, knows, mary)
3. (john, age, "35")

More Complex:
              ┌─── name="John"
              ├─── age="35"
john ─────────┤
              ├─── knows ──→ mary
              │
              └─── hasFriend ──→ bob

Multiple graphs can merge by shared URIs:
Graph1 from source A: (john, name, "John"), (john, age, "35")
Graph2 from source B: (john, knows, mary)
Merged: All three triples, john node connects them
```

#### 2.4.2.3 RDF/XML Serialization

```
Same triples represented in XML:

<?xml version="1.0"?>
<rdf:RDF xmlns:rdf="http://www.w3.org/1999/02/22-rdf-syntax-ns#"
         xmlns:foaf="http://xmlns.com/foaf/0.1/">

  <rdf:Description rdf:about="http://example.org/john">
    <foaf:name>John Smith</foaf:name>
    <foaf:age>35</foaf:age>
    <foaf:knows rdf:resource="http://example.org/mary"/>
  </rdf:Description>

  <rdf:Description rdf:about="http://example.org/mary">
    <foaf:name>Mary Jones</foaf:name>
    <foaf:knows rdf:resource="http://example.org/john"/>
  </rdf:Description>

</rdf:RDF>

Structure:
├── rdf:Description: Statement about resource
├── rdf:about: URI of subject resource
├── Nested elements: Property-value pairs
├── rdf:resource: URI-valued properties
└── Text content: Literal values
```

#### 2.4.2.4 RDF Inference

```
Based on RDF triples, inference can derive new facts:

Given Facts:
1. (john, type, Student)
2. (Student, subClassOf, Person)
3. (Person, hasProperty, Mortal)

Inference Rules:

Rule 1 (subclass transitivity):
  IF (X, type, Y) AND (Y, subClassOf, Z)
  THEN (X, type, Z)

Rule 2 (property inheritance):
  IF (X, type, Y) AND (Y, hasProperty, P)
  THEN (X, hasProperty, P)

Derived Facts:
1. From Rule 1: (john, type, Person)
2. From Rule 2: (john, hasProperty, Mortal)

Conclusion: John is mortal (derived from types/classes)
```

### 2.4.3 Web Ontology Language (OWL)

#### 2.4.3.1 OWL Extensions to RDF

**OWL** adds more expressive power to RDF:

```
OWL Allows:

1. Class Definitions:
   Class: Doctor
   SubClassOf: Person
   Properties:
   ├── hasPatientsCount: integer
   ├── hasSpecialty: string
   └── treatsDisease: Disease

2. Property Restrictions:
   Class: Parent
   SubClassOf:
   ├── Person AND
   ├── hasChild some Person

   "A parent is a person who has at least one child"

3. Cardinality Constraints:
   Class: Country
   Properties:
   └── hasCapital: exactly 1 City

   "Every country has exactly one capital"

4. Disjointness:
   Class: Male
   DisjointWith: Female
   
   "No individual can be both male and female"

5. Equivalence:
   Class: Doctor
   EquivalentTo: Physician
   
   "Doctor and Physician refer to same class"

6. Property Characteristics:
   Property: isPartOf
   Characteristics:
   ├── Transitive: IF X partOf Y AND Y partOf Z THEN X partOf Z
   ├── Symmetric: IF X sibling Y THEN Y sibling X
   └── Functional: Each subject has at most one object
```

#### 2.4.3.2 OWL Example: Medical Domain

```
Ontology: MedicalOntology

Classes:
├── Disease
│   ├── InfectiousDisease
│   │   ├── ViralDisease
│   │   │   ├── Influenza
│   │   │   ├── COVID19
│   │   │   └── CommonCold
│   │   └── BacterialDisease
│   │       ├── Pneumonia
│   │       ├── Strep
│   │       └── UTI
│   └── NonInfectiousDisease
│       ├── Diabetes
│       ├── Cancer
│       └── HeartDisease
│
├── Symptom
│   ├── Fever
│   ├── Cough
│   ├── Fatigue
│   └── ChestPain
│
├── Treatment
│   ├── Medication
│   ├── Surgery
│   └── Therapy
│
└── Patient
    ├── hasAge: int
    ├── hasSymptoms: Symptom
    └── hasDiagnosis: Disease

Properties:
├── causes: Disease → Symptom
│   Influenza causes Fever
│   Influenza causes Cough
│
├── treatedBy: Disease → Treatment
│   Pneumonia treatedBy Antibiotic
│
├── hasContraindication: Medication → Condition
│   AntibioticX contraindicated for PregnantPatient
│
└── hasInteraction: Medication → Medication
    DrugA interactions DrugB

Rules (Restrictions):
├── Patient with Fever AND Cough likely has InfectiousDisease
├── COVID19 requires immediate referral if elderly
├── Certain medications contraindicated with allergies
└── Double-dosing medication if weight > 100kg

Reasoning:
1. Patient presents: Fever=yes, Cough=yes, ChestPain=yes
2. Rule application: Disease causes these symptoms?
3. Inference: Pneumonia is most likely (high confidence match)
4. Treatment lookup: Pneumonia treatedBy Antibiotic
5. Safety check: Patient allergies? Contraindications?
6. Conclusion: Recommend Antibiotic X, dosage Y
```

### 2.4.4 Integration in Multi-Agent Systems

```
Semantic Web in MAS:

Agent 1 (Hospital Database):
├── Knowledge: Patient records in medical ontology format
├── Semantic Web: Exposes patient data as RDF/OWL
└── Shares: Standard medical ontology vocabulary

Agent 2 (Insurance System):
├── Knowledge: Coverage information
├── Semantic Web: Uses same medical ontology
└── Understands: Patient conditions using shared vocabulary

Agent 3 (Pharmacy):
├── Knowledge: Drug information
├── Semantic Web: Drug interactions in standard format
└── Coordinates: With hospital and insurance

Benefits:
├── Shared Understanding: All agents use same vocabulary
├── Automated Integration: Machines understand meaning
├── Reasoning: Can infer relationships
├── Scalability: Add new agents with standard ontology
└── Interoperability: Different systems work together
```

---

## 2.5 Agent Communication

### 2.5.1 FIPA Agent Communication Language (FIPA-ACL)

**FIPA-ACL**: Foundation for Intelligent Physical Agents - Agent Communication Language

#### 2.5.1.1 Message Structure

```
FIPA-ACL Message: Structured message between agents

Basic Components:

1. Performative (Mandatory):
   Type of communicative act
   ├── inform: Assert information
   ├── request: Ask to do something
   ├── propose: Suggest action
   ├── accept: Accept proposal
   ├── refuse: Reject request
   ├── ask-if: Query yes/no
   ├── ask-one: Query single answer
   ├── ask-all: Query all answers
   ├── query-if: Query with reply
   └── cancel: Cancel request

2. Sender:
   Agent initiating communication
   Example: "hospitalAgent"

3. Receiver:
   Agent(s) receiving message
   Example: ["insuranceAgent", "pharmacyAgent"]

4. Content:
   Actual message content/information
   Example: "Patient John needs Antibiotic X"

5. Language:
   How to interpret content
   Examples: "Prolog", "FIPA-SL", "RDF"

6. Ontology:
   Vocabulary/shared meaning
   Example: "MedicalOntology"

7. Conversation-ID:
   Track related messages
   Example: "patient_diagnosis_2024_01"

8. Reply-With:
   Identifier for this message
   Used when responding
   Example: "request_123"

9. In-Reply-To:
   References message being replied to
   Example: "request_123" (responding to that message)

10. Reply-By:
    Deadline for response
    Example: "2024-01-15T14:30:00Z"
```

#### 2.5.1.2 FIPA-ACL Example Messages

```
Example 1: REQUEST (Agent asking another to do something)

(request
  :sender Agent-A
  :receiver Agent-B
  :language Prolog
  :ontology MedicalOntology
  :content (diagnose-patient patient-123)
  :reply-with req-1
)

Translation: "Agent-A asks Agent-B to diagnose patient 123"


Example 2: INFORM (Agent providing information)

(inform
  :sender Agent-B
  :receiver Agent-A
  :language Prolog
  :ontology MedicalOntology
  :content (diagnosis patient-123 pneumonia)
  :in-reply-to req-1
)

Translation: "Agent-B informs Agent-A that patient 123 has pneumonia"


Example 3: PROPOSE (Agent suggesting action)

(propose
  :sender Agent-B
  :receiver Agent-C
  :language Prolog
  :ontology MedicalOntology
  :content (treatment patient-123 antibiotic-X dosage-500mg)
  :reply-with prop-1
)

Translation: "Agent-B proposes treating patient 123 with Antibiotic-X at 500mg"


Example 4: REFUSE (Agent declining request)

(refuse
  :sender Agent-C
  :receiver Agent-A
  :language Prolog
  :ontology MedicalOntology
  :content (reason patient-123 allergic-to-antibiotic-X)
  :in-reply-to req-1
)

Translation: "Agent-C refuses because patient 123 is allergic to Antibiotic-X"
```

#### 2.5.1.3 Speech Act Theory

**Underlying Theory**: FIPA-ACL based on speech acts

```
Speech Act (Performative):
Utterance that performs action (beyond just stating fact)

Components:

1. Locutionary Act:
   Physical act of speaking/writing
   "I promise to help"

2. Illocutionary Act:
   Intended effect on listener
   "I promise" = commitment to future action

3. Perlocutionary Act:
   Effect on listener
   Listener feels assured/confident

FIPA Performatives as Speech Acts:

inform:
├── Illocutionary: Assert proposition as true
├── Precondition: Sender believes it's true
└── Effect: Receiver should believe it too

request:
├── Illocutionary: Get agent to perform action
├── Precondition: Sender believes necessary/wanted
└── Effect: Receiver should perform action

propose:
├── Illocutionary: Suggest course of action
├── Precondition: Might be mutually beneficial
└── Effect: Receiver considers the proposal

refuse:
├── Illocutionary: Decline to perform action
├── Precondition: Action requested but unwilling/unable
└── Effect: Requestor knows refusal and reason

Semantics:
Each performative has formal definition of:
├── When appropriate to use (feasibility conditions)
├── What propositions involved
├── What mental states required
└── What effects intended
```

### 2.5.2 Communication Protocols

**Protocol**: Sequence and format of messages in structured interaction

#### 2.5.2.1 Contract Net Protocol

Used for task allocation through bidding:

```
Scenario: Manager has task, contractors bid to do it

Phases:

1. Announcement Phase:
   Manager → All Potential Contractors
   
   (cfp        ;call-for-proposals
    :sender manager
    :receiver (contractor-1 contractor-2 contractor-3)
    :content (task-1 deadline-today)
    :reply-with announcement-1
   )
   
   Manager broadcasts: "Who can do Task-1 by today?"

2. Bid Submission Phase:
   Contractors → Manager
   
   Contractor-1 (capable, low cost):
   (propose
    :sender contractor-1
    :receiver manager
    :content (bid task-1 cost-100 days-1)
    :in-reply-to announcement-1
   )
   
   Contractor-2 (capable, higher cost):
   (propose
    :sender contractor-2
    :receiver manager
    :content (bid task-1 cost-150 days-0.5)
    :in-reply-to announcement-1
   )
   
   Contractor-3 (not capable):
   (refuse
    :sender contractor-3
    :receiver manager
    :content (reason not-capable insufficient-expertise)
    :in-reply-to announcement-1
   )

3. Evaluation Phase:
   Manager evaluates bids
   ├── Cost
   ├── Quality
   ├── Timeline
   ├── Contractor reputation
   └── Selects best bid

4. Award/Reject Phase:
   Manager → Winners/Losers
   
   Winner (Contractor-2):
   (accept-proposal
    :sender manager
    :receiver contractor-2
    :content (award task-1)
   )
   
   Loser (Contractor-1):
   (reject-proposal
    :sender manager
    :receiver contractor-1
    :content (bid task-1 rejected-higher-bidder)
   )

5. Execution Phase:
   Winner executes task
   Reports completion

6. Completion Phase:
   Winner → Manager: Results
   
   (inform
    :sender contractor-2
    :receiver manager
    :content (task-1 completed successfully)
   )
   
   Manager verifies and closes contract

Benefits:
├── Fair competition among contractors
├── Manager gets best proposal
├── Distributed task allocation
├── Market-like mechanism
├── Scalable (new contractors can join)
└── Can be applied to resource allocation, etc.
```

#### 2.5.2.2 Publish-Subscribe Protocol

Topics and subscribers:

```
Scenario: Agents interested in news topics subscribe

1. Publisher announces it has information
   Publisher: "I publish stock_prices topic"

2. Subscribers express interest
   (subscribe
    :sender stock-trader-agent
    :receiver stock-price-publisher
    :language Prolog
    :ontology financial-ontology
    :content topic-stock_prices
    :reply-with sub-1
   )

3. Publisher confirms subscription
   (inform
    :sender stock-price-publisher
    :receiver stock-trader-agent
    :content (subscribed topic-stock_prices)
    :in-reply-to sub-1
   )

4. When new information, publisher sends to all subscribers
   (inform
    :sender stock-price-publisher
    :receiver (subscriber-1 subscriber-2 subscriber-3)
    :content (stock APPL price-$150 timestamp-14:30)
    :ontology financial-ontology
   )

5. Unsubscribe when no longer interested
   (unsubscribe
    :sender stock-trader-agent
    :receiver stock-price-publisher
    :content topic-stock_prices
   )

Benefits:
├── Scalable: Many subscribers for one publisher
├── Loose coupling: Publishers/subscribers don't know each other
├── Asynchronous: No blocking calls
├── Selective: Only interested parties receive
├── Event-driven: Reactive to information
└── Clean separation of concerns
```

---

## 2.6 Knowledge Sharing Using Ontologies

### 2.6.1 Role of Ontologies in Multi-Agent Systems

**Ontology**: Formal representation of concepts and relationships in domain

#### 2.6.1.1 Semantic Interoperability

**Problem**: Agents with different internal representations cannot understand each other.

```
Agent A Internal Representation:
  Patient record:
  ├── name: "John Smith"
  ├── age: 45
  ├── condition: "High Blood Pressure"
  └── treatment: "Beta Blocker"

Agent B Internal Representation:
  Patient data:
  ├── patient_id: "P123"
  ├── years_old: 45
  ├── diagnosis: "Hypertension"
  └── medication: "Propranolol"

Problem: Both agents have same patient info, but representations differ
├── Different field names (name vs. patient_id)
├── Different terminology (age vs. years_old)
├── Different diagnoses (High Blood Pressure vs. Hypertension)
├── Different medication names (Beta Blocker vs. Propranolol)

Solution: Shared Ontology

Ontology: Medical Information Ontology
├── Concept: PatientIdentification
│   ├── has-name: string
│   ├── has-age: integer
│   └── has-id: string
│
├── Concept: Diagnosis
│   ├── has-name: string
│   └── has-code: ICD9
│   └── SYN[Hypertension, HighBloodPressure]
│
├── Concept: Medication
│   ├── has-generic-name: string
│   └── has-brand-names: string[]
│   └── Propranolol isa BetaBlocker

Mapping:
Agent A → Ontology:
├── "High Blood Pressure" → Hypertension concept
├── "Beta Blocker" → BetaBlocker class
└── Maps to shared ontology

Agent B → Ontology:
├── "Hypertension" → Hypertension concept
├── "Propranolol" → BetaBlocker class
└── Maps to shared ontology

Result: Both agents understand they discuss same patient, same conditions
```

#### 2.6.1.2 Ontology-Based Communication

```
Using Ontology in FIPA-ACL Messages:

Message Structure:
(inform
  :sender Agent-A
  :receiver Agent-B
  :content "Patient has Hypertension"
  :ontology MedicalOntology  ← Specifies shared vocabulary
  :language FIPA-SL           ← Formal language
)

Content Interpretation:
Agent B receives message
├── Sees ontology: MedicalOntology
├── Looks up: Hypertension definition
├── Interprets: Patient condition = arterial blood pressure ≥ 140/90 mmHg
├── Further action: Consult treatment guidelines for hypertension
└── Responds: With informed decision

Benefits:
├── Unambiguous interpretation: Definition in ontology
├── Automatic: Machines can process without human intervention
├── Consistent: Both agents interpret same way
├── Extensible: New concepts added to ontology
└── Transferable: Same ontology used across many agent pairs
```

### 2.6.2 Ontology Construction and Sharing

```
Creating Shared Ontology:

Step 1: Identify Domain Concepts
Example Medical Domain:
├── Patient (attributes: name, age, medical_history)
├── Disease (attributes: name, symptoms, treatment)
├── Medication (attributes: name, dosage, side_effects)
├── Treatment (attributes: type, duration, effectiveness)
└── Symptom (attributes: severity, duration)

Step 2: Define Relationships
├── Patient has Disease
├── Disease causes Symptom
├── Disease treated by Medication/Treatment
├── Medication has SideEffect
├── Patient takes Medication
└── Treatment includes Medication

Step 3: Specify Properties
For each concept, define:
├── Data type (string, integer, date)
├── Cardinality (1:1, 1:N, N:N)
├── Range (minimum/maximum)
├── Required vs. optional
└── Default values

Step 4: Define Rules
├── Business rules
├── Constraints
├── Inference rules
└── Integration rules

Example Rule:
"If Patient has Disease AND
 Disease treated-by Medication AND
 Patient allergic-to Medication
 THEN flag as contraindication"

Step 5: Version and Distribute
├── Version number: MedicalOntology v2.0
├── Format: OWL, RDF, XML
├── Repository: Central location
├── Documentation: Usage guide
└── Registration: Agents declare support
```

### 2.6.3 Ontology Evolution and Alignment

```
Challenge: Agents with different ontology versions

Scenario:
├── Agent A: Uses MedicalOntology v1.0
│   └── Hypertension = high blood pressure
├── Agent B: Uses MedicalOntology v2.0
│   └── Hypertension = arterial pressure ≥ 140/90
└── Communication: Do they understand each other?

Solution: Ontology Mapping/Alignment

1. Identify Correspondences:
   MedOnt v1.0 Concept ↔ MedOnt v2.0 Concept
   ├── Patient ↔ Patient (identical)
   ├── Disease ↔ DiseaseCondition (rename)
   ├── BloodPressureHigh ↔ Hypertension (consolidation)
   └── Treatment ↔ TherapeuticIntervention (specialization)

2. Define Mappings:
   v1.0.Patient = v2.0.Patient
   v1.0.BloodPressureHigh ≈ v2.0.Hypertension (similar)
   v1.0.Treatment ⊂ v2.0.TherapeuticIntervention (subset)

3. Translation Functions:
   When v1.0 agent sends message with v1.0 concepts:
   └── Translator converts to v2.0 concepts
   └── v2.0 agent understands v1.0 message
   └── Response translated back to v1.0

Benefits of Alignment:
├── Backward compatibility
├── Gradual migration to new versions
├── Support for heterogeneous ontologies
├── Interoperability across versions
└── Long-term system stability
```

---

## 2.7 Agent Development Frameworks

### 2.7.1 Framework Characteristics

**Agent Framework** (Platform): Software infrastructure for building and running agents

```
Framework Provides:

1. Agent Container:
   ├── Hosting environment for agents
   ├── Agent creation and lifecycle management
   ├── Message passing infrastructure
   └── Resource management

2. Agent Communication:
   ├── Message sending/receiving
   ├── Protocol support
   ├── Asynchronous messaging
   └── Service discovery

3. Services:
   ├── Agent registration
   ├── Service directory
   ├── Naming services
   ├── Time synchronization
   └── Logging

4. Development Support:
   ├── APIs for agent development
   ├── Debugging tools
   ├── Monitoring/profiling
   ├── Testing frameworks
   └── Documentation

5. Runtime Environment:
   ├── Multi-threading
   ├── Concurrency control
   ├── Distributed execution
   └── Persistence
```

### 2.7.2 Framework Categories

#### 2.7.2.1 Standalone Frameworks

```
Complete frameworks for building MAS from scratch

Examples:
├── Agent Tooling Environment (ATE)
├── Agent Development Kit (ADK)
└── Multi-Agent Platform (MAP)

Characteristics:
├── Comprehensive agent management
├── Built-in communication protocols
├── Agent lifecycle support
├── Service discovery mechanisms
└── Complete ecosystem

Structure:
    Framework Core
    ├── Agent Container
    ├── Agent Manager
    ├── Communication Layer
    ├── Service Registry
    └── Utility Services
         │
         └─→ Agent1, Agent2, Agent3, ...
```

#### 2.7.2.2 Lightweight Frameworks

```
Minimal core, extended through libraries

Characteristics:
├── Simple core
├── Flexible architecture
├── Library-based extensions
├── Suitable for specific domains
├── Less overhead

Structure:
    Lightweight Core
    ├── Basic Message Passing
    ├── Agent Container
    └── Extension Points
         │
         ├─→ Communication Library
         ├─→ Protocol Library
         ├─→ Service Library
         └─→ Custom Code
```

#### 2.7.2.3 Middleware Approach

```
Built on existing middleware (not a complete framework)

Characteristics:
├── Leverages existing infrastructure
├── Can be integrated into other systems
├── More interoperability
├── Less development from scratch

Examples:
├── Agent Abstraction Layer (AAL)
├── Service-Oriented Architecture (SOA) agents
└── REST-based agent communication
```

### 2.7.3 Key Features and Capabilities

```
Essential Features:

1. Agent Lifecycle Management:
   ├── Creation: How to instantiate agents
   ├── Initialization: Setup with parameters
   ├── Execution: Running the agent
   ├── Monitoring: Track performance
   └── Termination: Cleanup and shutdown

2. Communication Infrastructure:
   ├── Message transport
   ├── Protocol support (FIPA-ACL, etc.)
   ├── Asynchronous messaging
   ├── Message queuing
   └── Routing

3. Service Discovery:
   ├── Register services provided
   ├── Query available services
   ├── Dynamic discovery
   ├── Service metadata
   └── Service versioning

4. Concurrency and Synchronization:
   ├── Thread management
   ├── Mutual exclusion
   ├── Semaphores/monitors
   ├── Deadlock prevention
   └── Race condition handling

5. Persistence:
   ├── Agent state persistence
   ├── Database integration
   ├── Configuration management
   ├── Logging
   └── Recovery from failures

6. Security:
   ├── Authentication (who is agent?)
   ├── Authorization (what can agent do?)
   ├── Encryption (protect messages)
   ├── Audit trails
   └── Threat detection

7. Monitoring and Debugging:
   ├── Agent status queries
   ├── Performance metrics
   ├── Message tracing
   ├── Breakpoints
   └── Profiling

8. Scalability Support:
   ├── Multiple containers
   ├── Distribution across machines
   ├── Load balancing
   ├── Clustering
   └── Resource management
```

### 2.7.4 Framework Selection Considerations

```
Factors in Choosing Framework:

1. Agent Model:
   ├── Does framework support needed architecture?
   ├── BDI, reactive, hybrid?
   ├── Learning capabilities needed?
   └── Mobility support?

2. Communication:
   ├── FIPA-ACL support?
   ├── Other protocols?
   ├── Performance requirements?
   └── Security requirements?

3. Scalability:
   ├── Number of agents?
   ├── Distributed needed?
   ├── Message volume?
   └── Latency requirements?

4. Development Effort:
   ├── Learning curve?
   ├── Development speed?
   ├── Debugging support?
   └── Documentation quality?

5. Integration:
   ├── Legacy system integration?
   ├── Middleware compatibility?
   ├── Database connectivity?
   └── Service integration?

6. Cost:
   ├── Commercial or open-source?
   ├── License terms?
   ├── Support availability?
   └── Training requirements?

7. Community and Support:
   ├── Active user community?
   ├── Professional support available?
   ├── Frequent updates?
   └── Maturity/stability?
```

---

## CONCLUSION

Unit II covers Natural Language Processing and Multi-Agent Systems, two critical areas of AI:

### Key Takeaways - NLP:

1. **Linguistics Foundation**: AI systems need to understand multiple levels of language (phonology, morphology, syntax, semantics, pragmatics).

2. **Parsing**: Converting text to structured form requires sophisticated algorithms (top-down, bottom-up, chart parsing).

3. **Meaning**: From syntax to semantics requires capturing concepts, roles, and relationships.

4. **Context**: Pragmatics adds interpretation based on context, intent, and world knowledge.

### Key Takeaways - MAS:

1. **Agent Characteristics**: Autonomy, reactivity, proactivity, social ability distinguish agents from objects.

2. **Architectures**: Reactive, deliberative, and hybrid architectures suit different problems.

3. **Communication**: FIPA-ACL provides standard message format and protocols coordinate agent interaction.

4. **Semantic Web**: RDF, OWL, and ontologies enable machines to understand shared meaning.

5. **Coordination**: Various protocols (Contract Net, Publish-Subscribe) enable effective multi-agent collaboration.

6. **Frameworks**: Platforms provide infrastructure for building and managing multi-agent systems.

---

# REFERENCES

**Primary Textbooks:**
1. Dan W. Patterson, "Introduction to Artificial Intelligence and Expert Systems" (Prentice-Hall, India)
2. P. H. Winston, "Artificial Intelligence" (Addison Wesley)

**Reference Materials:**
1. A. Rich and K. Knight, "Artificial Intelligence" (Tate McGraw Hill)
2. E. Charnaik and D. McDermott, "Introduction to Artificial Intelligence" (Addison-Wesley)
3. N. J. Nilsson, "Artificial Intelligence: A New Synthesis" (Morgan Kaufmann)
4. T. Dean, J. Allen, Y. Aloimonos, "Artificial Intelligence: Theory and Practice" (Benjamin/Cummings)
5. S. Russell and P. Norvig, "Artificial Intelligence: A Modern Approach" (Prentice Hall)

---

**END OF UNIT II COMPREHENSIVE STUDY MATERIAL**
