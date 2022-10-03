# Japanese BART Pretrained Modelについて

BARTの事前学習済みモデルは、[京大が公開している]("https://nlp.ist.i.kyoto-u.ac.jp/?BART%E6%97%A5%E6%9C%AC%E8%AA%9EPretrained%E3%83%A2%E3%83%87%E3%83%AB")。

Tokenizer（単語分割）はJuman++(v2.0.0-rc3)に依存してるため、Hugginfaceでは使用不可。

fairseqのライブラリを使用して、事前学習を行っている。
手厚く日本語サポートREADMEも作成してある。
<https://github.com/utanaka2000/fairseq/blob/japanese_bart_pretrained_model/JAPANESE_BART_README.md>

## 環境構築について

Dockerで環境構築する。

## 使用方法

```environment/ubuntu/volume```内に移動し、```wget http://lotus.kuee.kyoto-u.ac.jp/nl-resource/JapaneseBARTPretrainedModel/japanese_bart_base_2.0.tar.gz```を実行する。```tar -zxvf japanese_bart_base_2.0.tar.gz```で解答することができる。
