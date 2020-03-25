# japanese-names-trans
Translate Japanese Names to / from English

This software uses [PyTorch](https://github.com/pytorch/pytorch)
port of [OpenNMT](https://github.com/OpenNMT/OpenNMT),
an open-source (MIT) neural machine translation system.


## Requirements

Install `OpenNMT-py` from `pip`:
```bash
pip install OpenNMT-py
```

## Japanese Names Parallel Corpus
The names in data\parallel-japanese-corpus are represented (one line per FirstName or LastName) as follow : 
### names-en-train
```
^ln f u n a k o s h i $
^fn s a b u r o $
[...]
```

### names-jp-train
```
^ln 船 越 $
^fn 三 朗 $
[...]
```

## Train ONMT translation model
### ONMT preprocess
Prepare Japanese to English data :
```bash
onmt_preprocess -train_src data/parallel-japanese-corpus/names-jp-train.txt -train_tgt data/parallel-japanese-corpus/names-en-train.txt -valid_src data/parallel-japanese-corpus/names-jp-val.txt -valid_tgt data/parallel-japanese-corpus/names-en-val.txt -save_data data/onmt-model/jp_en_data
```

This will output three files in data/onmt-model : jp_en_data.train.0.pt, jp_en_data.valid.0.pt, jp_en_data.vocab.pt


Prepare English to Japanese data :
```bash
onmt_preprocess -train_src data/parallel-japanese-corpus/names-en-train.txt -train_tgt data/parallel-japanese-corpus/names-jp-train.txt -valid_src data/parallel-japanese-corpus/names-en-val.txt -valid_tgt data/parallel-japanese-corpus/names-jp-val.txt -save_data data/onmt-model/en_jp_data
```

This will output three files in data/onmt-model : en_jp_data.train.0.pt, en_jp_data.valid.0.pt, en_jp_data.vocab.pt
