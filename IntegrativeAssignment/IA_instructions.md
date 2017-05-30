---
layout: workshop_main_5day
permalink: /bicg_2017
title: BiCG
header1: Integrative Assignment using Galaxy
header2: Bioinformatics for Cancer Genomics 2017
image: /site_images/CBW_cancerDNA_icon-16.jpg
---

# Galaxy

The purpose of this integrative assignment is to help you familiarize yourself with the Galaxy environment by performing a differential expression experiment between a set of carnioma samples and normal samples.

To accomplish this goal, we're going to be using the softwares [Hisat2] (https://ccb.jhu.edu/software/hisat2/index.shtml) for alignment of the reads, [Stringtie] (https://ccb.jhu.edu/software/stringtie/) for effecient transcript quantification, and CuffDiff to determine differenially expressed genes.

>Note: a published pipeline for the tools above is to finish the differential expression using Ballgown. However, we're limited to the softwares currently available on the Galaxy Server, and so need to make adjustments as necessary.

## Uploading our data

Let's begin by downloading and subsequently uploading our data onto the Galaxy server. Login into the AWS instance through either terminal or PuTTy, and make a link to where the data is stored:

```
cd workspace;
ln -s /home/ubuntu/CourseData/CG_data/IntegrativeAssignment/
```

Now open a web browser and go to the address:

```
cbwXX.dyndns.info/IntegrativeAssignment/
```

where XX is your student number. Navigate into the _fasta_ folder and download the files present:

*Insert image Download00 and Download01 here*

Since our example data is only a subset of reads that map to chromosome 9, we're going to download a modified reference and gtf file. Please find them attached [here] (link to files).



