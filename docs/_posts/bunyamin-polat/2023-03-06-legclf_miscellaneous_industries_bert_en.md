---
layout: model
title: Legal Miscellaneous Industries Document Classifier (EURLEX)
author: John Snow Labs
name: legclf_miscellaneous_industries_bert
date: 2023-03-06
tags: [en, legal, classification, clauses, miscellaneous_industries, licensed, tensorflow]
task: Text Classification
language: en
edition: Legal NLP 1.0.0
spark_version: 3.0
supported: true
engine: tensorflow
annotator: LegalClassifierDLModel
article_header:
  type: cover
use_language_switcher: "Python-Scala-Java"
---

## Description

European Union (EU) legislation is published in the EUR-Lex portal. All EU laws are annotated by the EU's Publications Office with multiple concepts from the EuroVoc thesaurus, a multilingual thesaurus maintained by the Publications Office.

Given a document, the legclf_miscellaneous_industries_bert model, it is a Bert Sentence Embeddings Document Classifier, classifies if the document belongs to the class Miscellaneous_Industries or not (Binary Classification) according to EuroVoc labels.

## Predicted Entities

`Miscellaneous_Industries`, `Other`

{:.btn-box}
<button class="button button-orange" disabled>Live Demo</button>
<button class="button button-orange" disabled>Open in Colab</button>
[Download](https://s3.amazonaws.com/auxdata.johnsnowlabs.com/legal/models/legclf_miscellaneous_industries_bert_en_1.0.0_3.0_1678111876363.zip){:.button.button-orange}
[Copy S3 URI](s3://auxdata.johnsnowlabs.com/legal/models/legclf_miscellaneous_industries_bert_en_1.0.0_3.0_1678111876363.zip){:.button.button-orange.button-orange-trans.button-icon.button-copy-s3}

## How to use



<div class="tabs-box" markdown="1">
{% include programmingLanguageSelectScalaPythonNLU.html %}
```python

document_assembler = nlp.DocumentAssembler()\
    .setInputCol("text")\
    .setOutputCol("document")

embeddings = nlp.BertSentenceEmbeddings.pretrained("sent_bert_base_cased", "en")\
    .setInputCols("document")\
    .setOutputCol("sentence_embeddings")

doc_classifier = legal.ClassifierDLModel.pretrained("legclf_miscellaneous_industries_bert", "en", "legal/models")\
    .setInputCols(["sentence_embeddings"])\
    .setOutputCol("category")

nlpPipeline = nlp.Pipeline(stages=[
    document_assembler, 
    embeddings,
    doc_classifier])

df = spark.createDataFrame([["YOUR TEXT HERE"]]).toDF("text")

model = nlpPipeline.fit(df)

result = model.transform(df)

```

</div>

## Results

```bash

+-------+
|result|
+-------+
|[Miscellaneous_Industries]|
|[Other]|
|[Other]|
|[Miscellaneous_Industries]|

```

{:.model-param}
## Model Information

{:.table-model}
|---|---|
|Model Name:|legclf_miscellaneous_industries_bert|
|Compatibility:|Legal NLP 1.0.0+|
|License:|Licensed|
|Edition:|Official|
|Input Labels:|[sentence_embeddings]|
|Output Labels:|[class]|
|Language:|en|
|Size:|21.7 MB|

## References

Train dataset available [here](https://huggingface.co/datasets/lex_glue)

## Benchmarking

```bash

                   label precision recall  f1-score  support
Miscellaneous_Industries      0.82   0.79      0.81       39
                   Other      0.79   0.81      0.80       37
                accuracy         -      -      0.80       76
               macro-avg      0.80   0.80      0.80       76
            weighted-avg      0.80   0.80      0.80       76
```