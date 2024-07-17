# Amharic Named Entity Recognition

The following transformer models were finetuned using the [amharic-named-entity-recognition](https://huggingface.co/datasets/rasyosef/amharic-named-entity-recognition) dataset. The *finetuning notebooks* can be found in the `notebooks` folder.

The reported precision, recall, and f1 metrics are macro averages.

|Model|Size (# params)| Precision | Recall | F1 |
| --- | ------------- | --------- |------- | -- |
|[bert-medium-amharic](https://huggingface.co/rasyosef/bert-medium-amharic)|40.5M|0.64|0.73|0.68|
|[bert-small-amharic](https://huggingface.co/rasyosef/bert-small-amharic)|27.8M|0.64|0.72|0.68|
|[bert-mini-amharic](https://huggingface.co/rasyosef/bert-mini-amharic)|10.7M|0.60|0.67|0.64|
|[bert-tiny-amharic](https://huggingface.co/rasyosef/bert-tiny-amharic)|4.18M|0.50|0.59|0.54|
|[xlm-roberta-base](https://huggingface.co/FacebookAI/xlm-roberta-base)|279M|0.69|0.79|0.73|
|[am-roberta](https://huggingface.co/uhhlt/am-roberta)|443M|0.67|0.72|0.69|

### Fine-tuned Model
A finetuned `bert-medium-amharic` model is available on HuggingFace:

[rasyosef/bert-medium-amharic-finetuned-ner](https://huggingface.co/rasyosef/bert-medium-amharic-finetuned-ner)

#### How to use

You can use this model directly with a pipeline for token classification:

```python
from transformers import pipeline
checkpoint = "rasyosef/bert-medium-amharic-finetuned-ner"
token_classifier = pipeline("token-classification", model=checkpoint, aggregation_strategy="simple")
token_classifier("አትሌት ኃይሌ ገ/ሥላሴ ኒውዮርክ ውስጥ በሚደረገው የተባበሩት መንግሥታት ድርጅት ልዩ የሰላም ስብሰባ ላይ እንዲገኝ ተጋበዘ።")
```

Output:
```python
[{'entity_group': 'TTL',
  'score': 0.9841112,
  'word': 'አትሌት',
  'start': 0,
  'end': 4},
 {'entity_group': 'PER',
  'score': 0.99379075,
  'word': 'ኃይሌ ገ / ሥላሴ',
  'start': 5,
  'end': 14},
 {'entity_group': 'LOC',
  'score': 0.8818362,
  'word': 'ኒውዮርክ',
  'start': 15,
  'end': 20},
 {'entity_group': 'ORG',
  'score': 0.99056435,
  'word': 'የተባበሩት መንግሥታት ድርጅት',
  'start': 32,
  'end': 50}]
```

### References

- [Token classification](https://huggingface.co/learn/nlp-course/chapter7/2?fw=pt)