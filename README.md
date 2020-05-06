# BERT

Original [README.md](https://github.com/google-research/bert/blob/master/README.md) here.


# STS (Semantic Textual Similarity) tasks

## Training and evaluating an English model by using STS-B dataset

### Prerequisites

- [Pretrained English model](https://storage.googleapis.com/bert_models/2018_10_18/uncased_L-12_H-768_A-12.zip)
- [GLUE data](https://gist.github.com/W4ngatang/60c2bdb54d156a41194446737ce03e2e)

You can download GLUE data by running the following command:

    $ python download_glue_data.py


### How to run

```bash
$ export BERT_BASE_DIR=/path/to/bert/uncased_L-12_H-768_A-12
$ export GLUE_DIR=/path/to/glue_data

$ python run_scorer.py \
  --task_name=stsb \
  --do_train=true \
  --do_eval=true \
  --data_dir=$GLUE_DIR/STS-B \
  --vocab_file=$BERT_BASE_DIR/vocab.txt \
  --bert_config_file=$BERT_BASE_DIR/bert_config.json \
  --init_checkpoint=$BERT_BASE_DIR/bert_model.ckpt \
  --max_seq_length=128 \
  --train_batch_size=32 \
  --learning_rate=2e-5 \
  --num_train_epochs=3.0 \
  --output_dir=/tmp/stsb_output
```

---

## Training and evaluating a Korean model by using KorSTS dataset

### Prerequisites

- [한국어 BERT 언어모델](http://aiopen.etri.re.kr/service_dataset.php?category=bert)
- [KorNLUDatasets](https://github.com/kakaobrain/KorNLUDatasets)


### How to run

```bash
$ export BERT_BASE_DIR=/path/to/002_bert_morp_tensorflow
$ export KORNLU_DIR=/path/to/KorNLUDatasets

$ cp $BERT_BASE_DIR/src_tokenizer/tokenization_morp.py .

$ python run_scorer.py \
  --task_name=korsts \
  --do_train=true \
  --do_eval=true \
  --do_lower_case=false \
  --tokenize_morp=true \
  --data_dir=$KORNLU_DIR/KorSTS \
  --vocab_file=$BERT_BASE_DIR/vocab.korean_morp.list \
  --bert_config_file=$BERT_BASE_DIR/bert_config.json \
  --init_checkpoint=$BERT_BASE_DIR/model.ckpt \
  --max_seq_length=128 \
  --train_batch_size=32 \
  --learning_rate=2e-5 \
  --num_train_epochs=3.0 \
  --output_dir=/tmp/korsts_output
```

### Result

```
MSE = 0.75299835
global_step = 718
label_ids = [5.   4.75 5.   ... 2.   0.   0.  ]
loss = 0.75290865
pearson = 0.8368647
pred = [4.8212824  4.553252   4.624973   ... 1.07251    0.36170498 1.33655   ]
spearman = 0.68977606
```


## Reference

- https://github.com/google-research/bert
- https://github.com/google-research/bert/issues/74
- http://aiopen.etri.re.kr/service_dataset.php
- https://github.com/kakaobrain/KorNLUDatasets
