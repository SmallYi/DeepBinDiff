# DeepBinDiff

This is the official repository for DeepBinDiff, which is a fine-grained binary diffing tool for x86 binaries. We will actively update it.

### Paper
Please consider citing our paper if you find the code useful.

Yue Duan, Xuezixiang Li, Jinghan Wang, and Heng Yin, "DeepBinDiff: Learning Program-Wide Code Representations for Binary Diffing", NDSS'2020


### Requirements:

* tensorflow (2.0 > tensorflow version >= 1.14.0)
* gensim
* angr
* networkx
* lapjv



### Run the tool


```
python3 src/deepbindiff.py --input1 path_to_the_first_binary --input2 /path_to_the_second_binary --outputDir output/
```

* For example, to compare O0 and O1 chroot binaries from coreutils v5.93, you may run:

```
python3 src/deepbindiff.py --input1 /home/DeepBinDiff/experiment_data/coreutils/binaries/coreutils-5.93-O0/chroot --input2 /home/DeepBinDiff/experiment_data/coreutils/binaries/coreutils-5.93-O1/chroot --outputDir output/
```


* You can also use **src/analysis_in_batch.sh** script to perform binary diffing in batches.


### Misc
1. IDA Pro or Angr?

We have both the IDA pro version and the angr version. IDA pro is used in order to directly compare with BinDiff, which uses IDA pro as well. The code here uses Angr.

2. Results?

Results are printed directly on the screen as "matched pairs" once the diffing is done. Each pair represents a matched pair of basic blocks in the two binaries. The numbers are the basic block indices, which can be found in output/nodeIndexToCode file.

3. CPU or GPU?

The current version is using CPU only. 

4. NLP pre-training?

The current version uses an on-the-fly training process, meaning we only use the two input binaries for NLP training. Therefore, we don't need any pre-trained model. This will eliminate the OOV problem but will slow down the process a bit.


### 记录
1. tensorflow2.0版本下需修改导入命令为</br>import tensorflow.compat.v1 as tf</br>tf.disable_v2_behavior()</br>
2. 在根目录运行.src_js/start_test_js.sh 因为有的文件使用相对路径
3. 使用GPU运行时会报错，有些操作只能在cpu进行，不按照以下方式进行，可能会出错。</br>
config = tf.ConfigProto(allow_soft_placement = True)</br>
sess = tf.Session(config = config)</br>
4. 源程序是基本块级别的比较，输出的匹配对是基本块id的匹配对
