# Sequencing Version of benchmarking genome NA12878


## 1.来自其他Call SNP软件的数据
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

### 原始Fastq乘数探究（到底是不是downsampling得到的？）
#### [第一个原始数据fastq来源](https://precision.fda.gov/challenges/truth)

>但是仅供有government-authorization使用，个人无法获取fastq数据。FDA challenge的fastq显示是50X，PCR-free。也就是说上文使用的数据集还是downsampling得到的30X而不是原始测序30X。

#### [第二个原始数据DNAnexus](https://dnanexus-rnd.s3.amazonaws.com/NA12878-xten.html )

>所有的数据都在这里，但是通过fastqc计算，是41X，不是30X，也就是说还是进行了一定程度的downsampling。


#### [Giab](https://jimb.stanford.edu/giab-resources)

[下载地址]
(ftp://ftp-trace.ncbi.nlm.nih.gov/giab/ftp/data/NA12878/NIST_NA12878_HG001_HiSeq_300x)

>这个数据集的话是300X，然后downsampling到30X。如果上面的数据不可用，就使用下面这个。


### 小结
这些数据全部都是进行了一定程度的downsampling。。。并没有公开的原始测序就是30X的这样子的数据。但是像deepvarints这样子的项目所使用的数据，我认为还是比较可信的，即使他们已经downsampling过了。但是数据是值得信赖的，毕竟是做新的call snp软件也是使用这样子的数据集。

### 操作方法
因为我们要测试的是BWA+GATK，所以必须使用30X的fastq数据，那么怎么办？可以从bam文件转回fastq文件。
[转换方法](http://www.metagenomics.wiki/tools/samtools/converting-bam-to-fastq)


## 2.其他同质产品的数据

同样是对BWA+GATK做加速这样子的工作，找到了[Edico Genome](http://www.edicogenome.com/wp-content/uploads/2015/02/Genome-Pipeline-Brief.pdf)和格列生物做的工作。都使用的是30X的SRA056922的数据。

SRA056922的数据在DDBJ上面有 
[存储路径]
(ftp://ftp.ddbj.nig.ac.jp/ddbj_database/dra/fastq/SRA056/SRA056922/)

```

Name	Size	Date Modified
SRX180717/		4/1/13, 8:00:00 AM
SRX181476/		4/3/13, 8:00:00 AM
SRX181477/		4/3/13, 8:00:00 AM
SRX181478/		4/3/13, 8:00:00 AM
SRX181479/		4/3/13, 8:00:00 AM
SRX181480/		4/3/13, 8:00:00 AM
SRX181481/		4/3/13, 8:00:00 AM
```

使用ascp+prefetch已经全部下载完毕~

```
-rw-r--r--  1 caiyiran  staff   3.5G Aug 30  2012 SRR548274.sra
-rw-r--r--  1 caiyiran  staff   1.0G Aug 30  2012 SRR548275.sra
-rw-r--r--  1 caiyiran  staff   1.0G Aug 30  2012 SRR548268.sra
-rw-r--r--  1 caiyiran  staff   1.0G Aug 30  2012 SRR548269.sra
-rw-r--r--  1 caiyiran  staff   807M Aug 30  2012 SRR548271.sra
-rw-r--r--  1 caiyiran  staff   441M Aug 30  2012 SRR548270.sra
-rw-r--r--  1 caiyiran  staff   347M Aug 30  2012 SRR548273.sra
-rw-r--r--  1 caiyiran  staff   205M Aug 30  2012 SRR548272.sra
-rw-r--r--  1 caiyiran  staff   196M Aug 24  2012 SRR546694.sra
```

现在来估计一下这个是不是原本就是30X的数据，还是被downsampling后的。

|文件名称|reads长度|reads数目|reads总数|
|:-----:|:------:|:------:|:-------:|
|SRR546694_1.fastq & 2.fastq|25bp|	5,348,963|267,448,150|
|SRR548268_1.fastq & 2.fastq|101bp|8,601,499|1,737,502,798|
|SRR548269_1.fastq & 2.fastq|101bp|8,574,009|1,731,949,818|
|SRR548270_1.fastq & 2.fastq|101bp|4,144,375|837,163,750|
|SRR548271_1.fastq & 2.fastq|76bp|8,717,653|1,325,083,256|
|SRR548272_1.fastq & 2.fastq|101bp|2,090,626|422,306,452|
|SRR548273_1.fastq & 2.fastq|101bp|3,411,835|689,190,670|
|SRR548274_1.fastq & 2.fastq|25bp|99,802,040|4,990,102,000|
|SRR548275_1.fastq & 2.fastq|101bp|8,296,870|1,675,967,740|
|总数|13,676,714,634|人类基因组长度|300，000，000|
|||覆盖乘数|45X|
### 小结
无论是Edico Genome还是格列生物都宣称使用的是30X的SRA056922的数据，但是实际上全部下载下来进行统计，是45X的数量，也就是说他们都预先Downsampling过了。BGI使用的是自己测的数据，这个无法使用。
## 3.结论

目前没有找到原始测的30X的数据，基本都是降采样到30X。可以对标其他的产品，使用SRA056922的数据进行降采样，也可以使用已经降采样过的bam文件转回原始的fastq。
