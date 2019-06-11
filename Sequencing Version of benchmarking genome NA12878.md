## Sequencing Version of benchmarking genome NA12878

#### [DeepVariants](https://console.cloud.google.com/storage/browser/deepvariant/public-training-data?pli=1)

>"Creating a universal
SNP and small indel variant caller with deep neural
networks“ From **Nature**

这个文章是Google团队利用CNN训练的模型，用于call snp，在文章中为了与GATK做对比，使用NA12878做benchmarking。

#### [数据描述](https://www.biorxiv.org/content/biorxiv/suppl/2018/01/09/092890.DC5/092890-1.pdf)：

>Sequencing was
performed using a 2x150 paired-end runs on Illumina HiSeq X sequencers with a targeted
sequencing depth of 30x per sample.

#### [数据地址](https://console.cloud.google.com/storage/browser/deepvariant/public-training-data?pli=1):

![数据截图](https://raw.githubusercontent.com/BigfatC/Daily_use_pic/master/Screen%20Shot%202019-06-11%20at%209.37.53%20AM.png)

上面是Google cloud上面的存储情况，有6个公共数据，在deepVariant的GitHub页面，看到了以下的信息。
这个文件来自于Precision FDA Truth Challenge，根据文章附件描述是30X，而这里显示的bam文件大小也是60X的一半。另外他们还给了其他的5个数据集，根据文章描述，这些全部都是30X的。

![shuju](https://raw.githubusercontent.com/BigfatC/Daily_use_pic/master/Screen%20Shot%202019-06-11%20at%209.45.33%20AM.png)

#### [Giab](ftp://ftp-trace.ncbi.nlm.nih.gov/giab/ftp/data/NA12878/NIST_NA12878_HG001_HiSeq_300x)

这个数据集的话是300X，然后downsampling到30X。如果上面的数据不可用，就使用下面这个。
