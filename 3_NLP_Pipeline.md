
Once tokenization is done the text has surpass number of sequential steps in a pipeline as shown in the image below.

![[NLP_Pipeline_flowdiagram.png]]


An NLP pipeline is a series of steps used to transform raw, unstructured text into a structured format that a machine can understand and analyze. Think of it like a factory assembly line: raw material goes in one end, and refined data comes out the other.


The NLP pipeline is initially empty and has only the Tokenizer

```python

nlp = spacy.blank("en")
doc = nlp("Hey everyone welcome to the NLP pipeline.")

for token in doc:
    print(token)
```

```
#Output
Hey
everyone
welcome
to
the
NLP
pipeline
.
```

```python
nlp.pipe_names
# Output: []
```

We can either add attributes manually into the pipeline or use a pretrained pipeline from spacy.

```python
nlp = spacy.load("en_core_web_sm")
# A pretrained pipeline
```

```python
nlp.pipe_names
# Output: ['tok2vec', 'tagger', 'parser', 'attribute_ruler', 'lemmatizer', 'ner']
```

Loading specific custom attributes into the pipeline

```python
source_nlp = spacy.load("en_core_web_sm")

nlp = spacy.blank("en")
nlp.add_pipe("ner",source = source_nlp) # Thus you can source it form another pipeline 
nlp.pipe_names
# Output: ['ner']
```






