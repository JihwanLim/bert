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

python run_scorer.py \
  --task_name=sts \
  --do_train=true \
  --do_eval=true \
  --data_dir=$GLUE_DIR/STS-B \
  --vocab_file=$BERT_BASE_DIR/vocab.txt \
  --bert_config_file=$BERT_BASE_DIR/bert_config.json \
  --init_checkpoint=$BERT_BASE_DIR/bert_model.ckpt \
  --max_seq_length=128 \
  --train_batch_size=24 \
  --learning_rate=2e-5 \
  --num_train_epochs=3.0 \
  --output_dir=/tmp/sts_output
```

---

## Training and evaluating a Korean model by using KorSTS dataset

### Prerequisites

- [한국어 BERT 언어모델](http://aiopen.etri.re.kr/service_dataset.php)
- [KorNLUDatasets](https://github.com/kakaobrain/KorNLUDatasets)


### How to run

```bash
$ export BERT_BASE_DIR=/path/to/2_bert_download_002_bert_morp_tensorflow/002_bert_morp_tensorflow
$ export KORNLU_DIR=/path/to/KorNLUDatasets

$ cp $BERT_BASE_DIR/src_tokenizer/tokenization_morp.py .

python run_scorer.py \
  --task_name=sts \
  --do_train=true \
  --do_eval=true \
  --do_lower_case=false \
  --data_dir=$KORNLU_DIR/KorSTS \
  --vocab_file=$BERT_BASE_DIR/vocab.korean_morp.list \
  --bert_config_file=$BERT_BASE_DIR/bert_config.json \
  --init_checkpoint=$BERT_BASE_DIR/model.ckpt \
  --max_seq_length=128 \
  --train_batch_size=24 \
  --learning_rate=2e-5 \
  --num_train_epochs=3.0 \
  --output_dir=/tmp/sts_output
```
