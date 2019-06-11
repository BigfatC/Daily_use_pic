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

#### [Github描述页面](https://github.com/google/deepvariant/blob/r0.8/docs/deepvariant-details-training-data.md#myfootnote1)

#### [参考基因组](https://console.cloud.google.com/storage/browser/genomics-public-data/references/GRCh38_Verily)

#### [第一个原始数据fastq来源](https://precision.fda.gov/challenges/truth)

>但是仅供有government-authorization使用，个人无法获取fastq数据。FDA challenge的fastq显示是50X，PCR-free。也就是说上文使用的数据集还是downsampling得到的30X而不是原始测序30X。

#### [第二个原始数据DNAnexus](https://dnanexus-rnd.s3.amazonaws.com/NA12878-xten.html )

>所有的数据都在这里，但是通过fastqc计算，是41X，不是30X，也就是说还是进行了一定程度的downsampling。


#### [Giab](ftp://ftp-trace.ncbi.nlm.nih.gov/giab/ftp/data/NA12878/NIST_NA12878_HG001_HiSeq_300x)

>这个数据集的话是300X，然后downsampling到30X。如果上面的数据不可用，就使用下面这个。


## 结论
这些数据全部都是进行了一定程度的downsampling。。。并没有公开的原始测序就是30X的这样子的数据。但是像deepvarints这样子的项目所使用的数据，我认为还是比较可信的，即使他们已经downsampling过了。但是数据是值得信赖的，毕竟是做新的call snp软件也是使用这样子的数据集。

## 操作方法
因为我们要测试的是BWA+GATK，所以必须使用30X的fastq数据，那么怎么办？可以从bam文件转回fastq文件。
[转换方法](http://www.metagenomics.wiki/tools/samtools/converting-bam-to-fastq)
还有就是继续寻找一开始就是30X的这些数据。。。。
