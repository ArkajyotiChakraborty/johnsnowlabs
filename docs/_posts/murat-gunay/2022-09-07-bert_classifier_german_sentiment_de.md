---
layout: model
title: German BertForSequenceClassification Cased model (from oliverguhr)
author: John Snow Labs
name: bert_classifier_german_sentiment
date: 2022-09-07
tags: [de, open_source, bert, sequence_classification, classification]
task: Text Classification
language: de
edition: Spark NLP 4.1.0
spark_version: 3.0
supported: true
annotator: BertForSequenceClassification
article_header:
  type: cover
use_language_switcher: "Python-Scala-Java"
---

## Description

Pretrained BertForSequenceClassification model, adapted from Hugging Face and curated to provide scalability and production-readiness using Spark NLP. `german-sentiment-bert` is a German model originally trained by `oliverguhr`.

## Predicted Entities

`neutral`, `positive`, `negative`

{:.btn-box}
<button class="button button-orange" disabled>Live Demo</button>
<button class="button button-orange" disabled>Open in Colab</button>
[Download](https://s3.amazonaws.com/auxdata.johnsnowlabs.com/public/models/bert_classifier_german_sentiment_de_4.1.0_3.0_1662513255290.zip){:.button.button-orange.button-orange-trans.arr.button-icon}
[Copy S3 URI](s3://auxdata.johnsnowlabs.com/public/models/bert_classifier_german_sentiment_de_4.1.0_3.0_1662513255290.zip){:.button.button-orange.button-orange-trans.button-icon.button-copy-s3}

## How to use



<div class="tabs-box" markdown="1">
{% include programmingLanguageSelectScalaPythonNLU.html %}
```python
documentAssembler = DocumentAssembler() \
    .setInputCols(["text"]) \
    .setOutputCols("document")

tokenizer = Tokenizer() \
    .setInputCols("document") \
    .setOutputCol("token")

seq_classifier = BertForSequenceClassification.pretrained("bert_classifier_german_sentiment","de") \
    .setInputCols(["document", "token"]) \
    .setOutputCol("class")
    
pipeline = Pipeline(stages=[documentAssembler, tokenizer, seq_classifier])

data = spark.createDataFrame([["PUT YOUR STRING HERE"]]).toDF("text")

result = pipeline.fit(data).transform(data)
```
```scala
val documentAssembler = new DocumentAssembler() 
      .setInputCols(Array("text")) 
      .setOutputCols(Array("document"))
      
val tokenizer = new Tokenizer()
    .setInputCols("document")
    .setOutputCol("token")
 
val seq_classifier = BertForSequenceClassification.pretrained("bert_classifier_german_sentiment","de") 
    .setInputCols(Array("document", "token")) 
    .setOutputCol("class")
   
val pipeline = new Pipeline().setStages(Array(documentAssembler, tokenizer, seq_classifier))

val data = Seq("PUT YOUR STRING HERE").toDS.toDF("text")

val result = pipeline.fit(data).transform(data)
```
</div>

{:.model-param}
## Model Information

{:.table-model}
|---|---|
|Model Name:|bert_classifier_german_sentiment|
|Compatibility:|Spark NLP 4.1.0+|
|License:|Open Source|
|Edition:|Official|
|Input Labels:|[document, token]|
|Output Labels:|[class]|
|Language:|de|
|Size:|408.7 MB|
|Case sensitive:|true|
|Max sentence length:|256|

## References

- [https://huggingface.co/oliverguhr/german-sentiment-bert](https://huggingface.co/oliverguhr/german-sentiment-bert)
- [https://www.lrec-conf.org/proceedings/lrec2020/pdf/2020.lrec-1.202.pdf](https://www.lrec-conf.org/proceedings/lrec2020/pdf/2020.lrec-1.202.pdf)
- [https://pypi.org/project/germansentiment/](https://pypi.org/project/germansentiment/)
- [https://github.com/oliverguhr/german-sentiment](https://github.com/oliverguhr/german-sentiment)
- [https://www.lrec-conf.org/proceedings/lrec2020/pdf/2020.lrec-1.202.pdf](https://www.lrec-conf.org/proceedings/lrec2020/pdf/2020.lrec-1.202.pdf)
- [https://www.romanklinger.de/scare/](https://www.romanklinger.de/scare/)
- [https://www.aclweb.org/anthology/L16-1181/](https://www.aclweb.org/anthology/L16-1181/)
- [https://www.spinningbytes.com/resources/germansentiment/](https://www.spinningbytes.com/resources/germansentiment/)
- [https://wortschatz.uni-leipzig.de/de/download/german](https://wortschatz.uni-leipzig.de/de/download/german)