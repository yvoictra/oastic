---
title: 'How to benchmark a Linux System (CPU, File IO, MySQL, Network...)'
date: 
draft: true
tags: ['Linux']
categories: ['Linux']
---

To```
sudo apt-get update
sudo apt-get install fio
``````
sudo apt-get update
sudo apt-get install sysbench
``````
fio --name=randwrite --ioengine=libaio --iodepth=1 --rw=randwrite --bs=4k --direct=0 --size=256M --numjobs=8 --runtime=60 --group\_reporting
``````
sysbench --test=fileio --file-total-size=2G --file-num=64 prepare
``````
sysbench --test=fileio --file-total-size=2G --file-test-mode=rndrd --max-time=240 --max-requests=0 --file-block-size=4K --file-num=64 --num-threads=32 run
``````
sysbench --test=cpu --cpu-max-prime=20000 --num-threads=1 run
``````
sysbench --test=cpu --cpu-max-prime=20000 --num-threads=2 run
```
