[![Discord](https://badgen.net/badge/icon/discord?icon=discord&label)](https://discord.gg/JvMQgMkpkm)
[![Compete on EvalAI](https://badgen.net/badge/compete%20on/EvalAI/blue)](https://eval.ai/web/challenges/challenge-page/1689/overview)
[![Win $1000](https://badgen.net/badge/win/%241%2C000.00/yellow)](http://mmsports.multimedia-computing.de/mmsports2022/challenge.html)

# The DeepSportRadar Player Re-Identification Challenge

Welcome to the DeepSportRadar Player Re-Identification Challenge, which is one of the [ACM MMSports 2022 Workshop](http://mmsports.multimedia-computing.de/mmsports2022/index.html) challenges. 
An opportunity to publish, as well as a $1000 prize by competing on [EvalAI](https://eval.ai/web/challenges/challenge-page/1685/overview). 
See [this page](http://mmsports.multimedia-computing.de/mmsports2022/challenge.html) for more details.
In this challenge, participants will have to re-identify basketball players across multiple video frames captured from the same camera viewpoint at various time instants.
For that purpose, we provide our Synergy Re-Identification dataset with image crops of players, referees and coaches.
The dataset is split into a training, test and challenge set. 
Test and challenge sets are both split into queries and galleries, similar to traditional ReID datasets.
The testing-set should be used to evaluate your model, both on the public EvalAI leaderboard that provides the temporary ranking, and when communicating about your method.
The challenge-set will be used for the official challenge ranking.

Maintainer: Vladimir Somers (v.somers@sportradar.com) from Synergy Sports, a division of Sportradar.
Author of this repository: Davide Zambrano from Synergy Sports (d.zambrano@sportradar.com).

**NOTE this code is based on Open-reid repo: https://github.com/Cysu/open-reid.git"**

_Open-ReID is a lightweight library of person re-identification for research
purpose. It aims to provide a uniform interface for different datasets, a full
set of models and evaluation metrics, as well as examples to reproduce (near)
state-of-the-art results._

We want to thank the authors for providing this tool. This version applies some changes to the original code to specifically adapt it to the DeepSportradar Challenge on Person Re-Identification. 

This challenge is a fork of the [player re-identification challenge](https://github.com/VIPriors/vipriors-challenges-toolkit/tree/master/re-identification) proposed in the [2nd VIPriors workshop challenges](https://vipriors.github.io/challenges/)

&nbsp;
<p align="center"><img src="assets/banner.png" width="740"></p>

## Installation

**Note that the file ```setup.py``` specifies the libraries version to use to run the code.**

Install [PyTorch](http://pytorch.org/). 

```shell
git clone https://github.com/DeepSportRadar/player-reidentification-challenge.git
cd player-reidentification-challenge
pip install -e .
```

## Example

Run the following command to train a baseline model:
```shell
python baseline/synergyreid_baseline.py -b 64 -j 2 -a resnet50 --logs-dir logs/synergy-reid/
```

## Data

Person re-identification data are provided by [Synergy Sports](ttps://synergysports.com). 
Data come from short sequences of basketball games, each sequence is composed by 20 frames. 
For the test and challenge sets, the query images are persons taken at the first frame, while the gallery images are identities taken from the 2nd to the last frame.

The idea behind the baseline is to provide a quick introduction to how to handle the re-id data. 
Specifically, attention should be put on the dataset creation and the dataloaders.
The data files are provided under ```baseline/data/synergyreid/raw/synergyreid_data.zip```.

The baseline code extracts the raw files in the same directory and prepares the splits to use for training, test and challenge.

Specifically the dataset is divided as:

```shell
SynergyReID dataset loaded
  subset      | # ids | # images
  ---------------------------
  train       |   436 |     8569
  query test   |    50 |       50
  gallery test |    50 |      910
  traintest    |   486 |     9529
  ---------------------------
  query challenge  |   468 |      468
  gallery challenge |  8703 |     8703
```

Train and test identities can be merged (to improve performance) using the flag ```--combine-traintest```.

The image filename is divided in three numbers: the first one is the person-id; the second one is the sequence where the image was taken; and the third one is the frame number.

The test-set is divided in query and gallery to match the challenge-set format. With the flag ```--evaluate``` the distance matrix for the test set is also saved.
The identities of the gallery are NOT provided; gallery ids are just random.

## Submission on EvalAI
Submit your result through the [challenge page on the EvalAI platform](https://eval.ai/web/challenges/challenge-page/1689/overview).
You need to submit a _.csv_ file as the pairwise distance matrix of size (m+1) x (n+1), where m is the number of query images and n is the number of gallery images. 
The first row and the first column are the query and gallery ids respectively.
Query ids have to be ordered. 
Please check the example provided in the baseline ```baseline/synergyreid_baseline.py``` with the 'write_mat_csv' function.

Please refer to the challenge webpage for complete rules, timelines and awards: [https://deepsportradar.github.io/challenge.html](https://deepsportradar.github.io/challenge.html).

## Questions and remarks
If you have any question or remark regarding the challenge and related materials, please raise a GitHub issue in this repository, or contact us directly on [Discord](https://discord.gg/JvMQgMkpkm).
