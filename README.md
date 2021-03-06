### Paper2vec Implementation

#### Han Tian, Hankz Hankui Zhuo

In this repository we provide open source implementations of paper2vec proposed in the literature. Our implementations learns the paper node embeddings from the paper citation network. (https://arxiv.org/abs/1703.06587)

#### Input File Formats

The input files contains the paper citation network. For efficiency the cited and citing papers of each nod will be described directly in the input file. The format of the input file is as follows, three lines as a unit:
```
  <node id>\n
  <citing nodes ids>\n
  <cited nodes ids>\n
```
For every node, the second line contains the papers it cites and three line the papers that cites it. papers in a line are separated by spaces. For example:
```
  9236192
  9151905 9034141 8976200 
  20865163 9547333 9841919 9743534 10499921 17645788 18577234 12429062
```
Make sure the first line contains all ids used in the input file.

#### Running Ranking Methods

First the input file will be sampled to generate the training corpus. 
```
  python genStairCorpus.py --input adjlistData.txt --output stairCorpus.txt --window 3 --iterate 900 --decay 0.7
```
Then for training:
```
  shuf stairCorpus.txt > shufStairCorpus.txt
  ./paper2vec -train shufStairCorpus.txt -output vectors.bin -size 300 -threads 8 -binary 1 -iter 2 -alpha 0.025
```
#### Licence

All codes are provided under a gnu/gpl licence.

