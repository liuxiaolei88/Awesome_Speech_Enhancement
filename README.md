# Awesome_Speech_Enhancement
[![Awesome](https://cdn.rawgit.com/sindresorhus/awesome/d7305f38d29fed78fa85652e3a63e154dd8e8829/media/badge.svg)](https://github.com/sindresorhus/awesome) [![PRs Welcome](https://img.shields.io/badge/PRs-welcome-brightgreen.svg?style=flat-square)](http://makeapullrequest.com) 

## Overviews
This repository collects papers on speech enhancement.

## Related papers
<!--  -->
[Fspen: an Ultra-Lightweight Network for Real Time Speech Enahncment](https://ieeexplore.ieee.org/document/10446016/authors#authors)  ICASSP 2024

[Code](https://github.com/gitwukeyi/FSPEN)

Method: 分成三个部分，（全/子频带编码，TF编码模块，全/子频带解码）。
step1：全/子频带编码：
- 全频带：频谱卷积3层捕获局部F维度信息 + 1x1卷积捕获全f信息。
- 子带：分成M个子带，低频子带密集，高频子带宽松。把子带再划分成N个组，每个组包含的F bin大小相同，即低频每个组包含更多的子带。每个Group接一个Conv1d，concat到一起。
- 把全频带特征和子带特征在通道维度cat。

step2：TF编码
- dprnn，F维度使用BiGRU，T维度分P组，每一组一个GRU

step3：全/子频带解码：
- 按通道分开子带和全频带
- 全频带：反卷积得出Complex Mask，直接和原始spec相乘得到est spec1，把est spec1分成est mag1和est phase1。
- 子带：线性层再concat，预测得出幅度mask，乘上原始幅度得到est mag2
- est mag = （est mag1 + est mag2）/2， 用est mag和est phase1相乘得到est


<!--  -->
