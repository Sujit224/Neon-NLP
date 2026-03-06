```python
import spacy
```

```python
nlp = spacy.blank("en")
target_text = "Welcome to Tokenization using spacy in NLP."
doc = nlp(target_text)

for token in doc:
	print(token)
```

```
# Output
Welcome
to
Tokenization
using
spacy
in
NLP
. 
```

![[Blank_Spacy_Object.png]]
Now a blank pipeline is created when nlp = spacy.blank("en") is written. We should add items in the pipeline as we proceed.

```python
type(nlp)
# spacy.lang.en.English
```

```python
type(doc)
# spacy.tokens.doc.Doc
```

```python
type(token)
# spacy.tokens.token.Token
```

```python
# Span is used to slice tokens in spacy
span = doc[1:5]
type(span) 
# spacy.tokens.span.Span
```

We can view all the methods associated with a token using the dir method

```python
dir(token)
```

```
# Output
['_',
 '__bytes__',
 '__class__',
 '__delattr__',
 '__dir__',
 '__doc__',
 '__eq__',
 '__format__',
 '__ge__',
 '__getattribute__',
 '__getstate__',
 '__gt__',
 '__hash__',
 '__init__',
 '__init_subclass__',
 '__le__',
 '__len__',
 '__lt__',
 '__ne__',
 '__new__',
 '__pyx_vtable__',
 '__reduce__',
 '__reduce_ex__',
 '__repr__',
 '__setattr__',
 '__sizeof__',
 '__str__',
 '__subclasshook__',
 '__unicode__',
 'ancestors',
 'check_flag',
 'children',
 'cluster',
 'conjuncts',
 'dep',
 'dep_',
 'doc',
 'ent_id',
 'ent_id_',
 'ent_iob',
 'ent_iob_',
 'ent_kb_id',
 'ent_kb_id_',
 'ent_type',
 'ent_type_',
 'get_extension',
 'has_dep',
 'has_extension',
 'has_head',
 'has_morph',
 'has_vector',
 'head',
 'i',
 'idx',
 'iob_strings',
 'is_alpha',
 'is_ancestor',
 'is_ascii',
 'is_bracket',
 'is_currency',
 'is_digit',
 'is_left_punct',
 'is_lower',
 'is_oov',
 'is_punct',
 'is_quote',
 'is_right_punct',
 'is_sent_end',
 'is_sent_start',
 'is_space',
 'is_stop',
 'is_title',
 'is_upper',
 'lang',
 'lang_',
 'left_edge',
 'lefts',
 'lemma',
 'lemma_',
 'lex',
 'lex_id',
 'like_email',
 'like_num',
 'like_url',
 'lower',
 'lower_',
 'morph',
 'n_lefts',
 'n_rights',
 'nbor',
 'norm',
 'norm_',
 'orth',
 'orth_',
 'pos',
 'pos_',
 'prefix',
 'prefix_',
 'prob',
 'rank',
 'remove_extension',
 'right_edge',
 'rights',
 'sent',
 'sent_start',
 'sentiment',
 'set_extension',
 'set_morph',
 'shape',
 'shape_',
 'similarity',
 'subtree',
 'suffix',
 'suffix_',
 'tag',
 'tag_',
 'tensor',
 'text',
 'text_with_ws',
 'vector',
 'vector_norm',
 'vocab',
 'whitespace_']
```

## Token methods are actually smart!!!
This tokens are actually used to perform complex analysis

```python
target_text = "Dr. Strange loves pav bhaji of mumbai as it costs only 2$ per plate in mumbai."
```

```python
doc = nlp(target_text)
for token in doc:
    print(token, "==>", "index: ",token.i,
         "is_alpha:", token.is_alpha,
         "is_punct:",token.is_punct,
         "like_num:",token.like_num,
         "is_currency:",token.is_currency,
         )
```

These methods are capable of figuring out if the tokens are alphabets or currency or punctuation?
```
# Output
Dr. ==> index:  0 is_alpha: False is_punct: False like_num: False is_currency: False
Strange ==> index:  1 is_alpha: True is_punct: False like_num: False is_currency: False
loves ==> index:  2 is_alpha: True is_punct: False like_num: False is_currency: False
pav ==> index:  3 is_alpha: True is_punct: False like_num: False is_currency: False
bhaji ==> index:  4 is_alpha: True is_punct: False like_num: False is_currency: False
of ==> index:  5 is_alpha: True is_punct: False like_num: False is_currency: False
mumbai ==> index:  6 is_alpha: True is_punct: False like_num: False is_currency: False
as ==> index:  7 is_alpha: True is_punct: False like_num: False is_currency: False
it ==> index:  8 is_alpha: True is_punct: False like_num: False is_currency: False
costs ==> index:  9 is_alpha: True is_punct: False like_num: False is_currency: False
only ==> index:  10 is_alpha: True is_punct: False like_num: False is_currency: False
2 ==> index:  11 is_alpha: False is_punct: False like_num: True is_currency: False
$ ==> index:  12 is_alpha: False is_punct: False like_num: False is_currency: True
per ==> index:  13 is_alpha: True is_punct: False like_num: False is_currency: False
plate ==> index:  14 is_alpha: True is_punct: False like_num: False is_currency: False
. ==> index:  15 is_alpha: False is_punct: True like_num: False is_currency: False
```

---
## Customization using ORTH
```python
doc = nlp("gimme double cheese extra large healthy pizza.")

tokens = [token.text for token in doc]
tokens
# Output: ['gimme', 'double', 'cheese', 'extra', 'large', 'healthy', 'pizza', '.']

# Here gimme = give + me and you would want them as 2 different set of tokens
```


```python
from spacy.symbols import ORTH

nlp.tokenizer.add_special_case("gimme",[
    {ORTH:"gim"},
    {ORTH:"me"}
])

doc = nlp("gimme double cheese extra large healthy pizza.")
tokens = [token.text for token in doc]
tokens

# Output: ['gim', 'me', 'double', 'cheese', 'extra', 'large', 'healthy', 'pizza', '.']
```

---
## Sentence Tokenization

As discussed above the nlp pipeline is initially blank.
```python
nlp.pipe_names
# Output  []
```

```python
# Adding sentencizer into the pipeline
nlp.add_pipe('sentencizer')
```

```python
nlp.pipe_names
# Output: ['sentencizer']
```

```python
doc = nlp("Dr. Strange loves pav bhaji of mumbai. Hulk loves chaat of Delhi")

for sentence in doc.sents:
    print(sentence)

# Output:  Dr. Strange loves pav bhaji of mumbai.
			#Hulk loves chaat of Delhi
```

---
