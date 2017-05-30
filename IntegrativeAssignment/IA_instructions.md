---
layout: tutorial_page
permalink: /integrative_assignemnt
title: BiCG
header1: Bioinformatics for Cancer Genomics 2017
header2: Integrative Assignment using Galaxy
image: /site_images/CBW_cancerDNA_icon-16.jpg
home: https://bioinformaticsdotca.github.io//bicg_2017
---

# Galaxy

The purpose of this integrative assignment is to help you familiarize yourself with the Galaxy environment by performing a differential expression experiment between a set of carnioma samples and normal samples.

To accomplish this goal, we're going to be using the softwares [Hisat](https://ccb.jhu.edu/software/hisat/index.shtml) for alignment of the reads, [Stringtie](https://ccb.jhu.edu/software/stringtie/) for effecient transcript quantification, and [CuffDiff](http://cole-trapnell-lab.github.io/cufflinks/cuffdiff/index.html) to determine differenially expressed genes.

>Note: a published pipeline for the tools above is to finish the differential expression using Ballgown. However, since we're using the tools available on the Galaxy server, we need to make adjustments as necessary.

## Brief explanation on the tools

Hisat is 

Stringtie is 

Cuffdiff is 

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

<img src="https://github.com/bioinformaticsdotca/BiCG_2017/blob/master/IntegrativeAssignment/Images/Download00.JPG?raw=true" alt="Setup 1" width="500" /> 
<img src="https://github.com/bioinformaticsdotca/BiCG_2017/blob/master/IntegrativeAssignment/Images/Download01.JPG?raw=true" alt="Setup 2" width="500" /> 

Since our example data is only a subset of reads that map to chromosome 9, we're going to download a modified reference and gtf file. Please find them attached [here](https://www.dropbox.com/sh/wd93pdob8ac5o51/AAB4MPjwV1tz4O2TfEC0PX7Oa?dl=0).

Once these files have been downloaded, we can begin to upload them onto the Galaxy server. Press on the *Get Data* button on the left hand side, followed by the *Upload File* button. Press on *Choose local file*, and select the fasta files, gtf, and modified reference that were recently downloaded. Alternatively, you can drag and drop the files from your computer onto the window. Leave all options on default.

<img src="" alt="Get data" width="500" /> 
<img src="" alt="Upload file" width="500" /> 
<img src="" alt="Choose local file" width="500" /> 

At the end of this section, we should see 14 files in our history.


## Transcript alignment using Hisat

Now that our data is uploaded, we can begin our analysis. __Normally we'd begin with doing some QC on our rna-sequencing data; unfortunately however, our data is in fasta format, and so we have to forego that step__

Let's begin with our transcript alignment/assembly using Hisat. Navigate to the *NGS: RNA Analysis* button on the left hand side, click it, find *Hisat*, and click on that. Alternatively, you can search for *Hisat* in the search tools bar.

Now to run Hisat, we're going to make a few modifications. Change:
*Input data format* to FASTA
*Single end or paired end?* to Individual paired reads
*Forward reads* to multiple datasets
*Reverse reads* to multiple datasets
*Source for the reference genome to align against* to Use a genome from history
*Select the reference genome* to 14: Homo_sapiens.GRCh38.dna.chromosome.9.fa

Now in the forward reads, we're going to go ahead and select all our read1 reads. For the reverse reads, we're going to select the read2 reads.

<img src="" alt="Get data" width="500" />




