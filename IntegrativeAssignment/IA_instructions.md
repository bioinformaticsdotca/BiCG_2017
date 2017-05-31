---
layout: tutorial_page
permalink: /bicg_2017_ia
title: BiCG
header1: Bioinformatics for Cancer Genomics 2017
header2: Integrative Assignment using Galaxy
image: /site_images/CBW_cancerDNA_icon-16.jpg
home: https://bioinformaticsdotca.github.io//bicg_2017
---

# Galaxy

The purpose of this integrative assignment is to help you familiarize yourself with the Galaxy environment by performing a differential expression experiment between a set of carnioma samples and normal samples.

To accomplish this goal, we're going to be using the softwares [Hisat](https://ccb.jhu.edu/software/hisat/index.shtml) for alignment of the reads, [Cufflinks](http://cole-trapnell-lab.github.io/cufflinks/) for efficient transcript quantification, [Cuffmerge](http://cole-trapnell-lab.github.io/cufflinks/cuffmerge/) to combine transcript counts, [Cuffquant](http://cole-trapnell-lab.github.io/cufflinks/cuffquant/) to precompute the gene expression values, and finally [CuffDiff](http://cole-trapnell-lab.github.io/cufflinks/cuffdiff/index.html) to determine differenially expressed genes.

>Note: The tools used for RNA-Sequencing pipelines do vary, so the above tools can be swapped out with others provided that the outputs from one program are compatible with another.

## Uploading our data

Let's begin by downloading and subsequently uploading our data onto the Galaxy server. Login into the AWS instance through either terminal or PuTTy, and make a link to where the data is stored:

```
cd workspace
ln -s /home/ubuntu/CourseData/CG_data/IntegrativeAssignment/
```

Now to be able to download, we need to change the permissions of the reference file by running the following command:

```
chmod ugo+wr IntegrativeAssignemnt/refs/*
```

Now open a web browser and go to the address:

```
cbwXX.dyndns.info/IntegrativeAssignment/
```

where XX is your student number. Navigate into the _IntegrativeAssignment_ folder followed by the _fasta_ folder and download the files present:

<img src="https://github.com/bioinformaticsdotca/BiCG_2017/blob/master/IntegrativeAssignment/Images/Download00.JPG?raw=true" alt="Setup 1" width="500" /> 
<img src="https://github.com/bioinformaticsdotca/BiCG_2017/blob/master/IntegrativeAssignment/Images/Download01.JPG?raw=true" alt="Setup 2" width="500" /> 

Since these reads have been taken to only map to chromosome 9, we're also going to download the chromosome 9 fasta file and the chromosome 9 gtf file.
>The GTF file holds information on the gene structure, and is used to determine the abundance of each gene or transcript.

<img src="https://github.com/bioinformaticsdotca/BiCG_2017/blob/master/IntegrativeAssignment/Images/I_setup_ref1.JPG?raw=true" alt="Setup 3" width="500" />
<img src="https://github.com/bioinformaticsdotca/BiCG_2017/blob/master/IntegrativeAssignment/Images/I_setup_ref2.JPG?raw=true" alt="Setup 3" width="500" />

Once these files have been downloaded, we can begin to upload them onto the Galaxy server. Visit the following link: https://usegalaxy.org. You'll be greeted by the following page, the main contents of which are as follows:

<img src="https://github.com/bioinformaticsdotca/BiCG_2017/blob/master/IntegrativeAssignment/Images/Galaxy01.JPG?raw=true" alt="Setup 3" width="750" />

Press on the *Get Data* button on the left hand side, followed by the *Upload File* button. Press on *Choose local file*, and select the fasta files, gtf, and modified reference that were recently downloaded. Alternatively, you can drag and drop the files from your computer onto the window. Leave all options on default, except __make sure to change the type of file in for our gtf file to a gtf__. Although the order of upload won't make much of a difference, follow the images below and upload the gtf and reference fasta first, and once completed, upload our tumour and normal fasta files.

<img src="https://github.com/bioinformaticsdotca/BiCG_2017/blob/master/IntegrativeAssignment/Images/Galaxy02.JPG?raw=true" alt="Get data" width="750" /> 
<img src="https://github.com/bioinformaticsdotca/BiCG_2017/blob/master/IntegrativeAssignment/Images/Galaxy03.JPG?raw=true" alt="Upload file" width="750" /> 
<img src="https://github.com/bioinformaticsdotca/BiCG_2017/blob/master/IntegrativeAssignment/Images/Galaxy04.JPG?raw=true" alt="Choose local file" width="750" /> 
<img src="https://github.com/bioinformaticsdotca/BiCG_2017/blob/master/IntegrativeAssignment/Images/Galaxy05.JPG?raw=true" alt="Choose local file" width="750" /> 
<img src="https://github.com/bioinformaticsdotca/BiCG_2017/blob/master/IntegrativeAssignment/Images/Galaxy06.JPG?raw=true" alt="Choose local file" width="750" /> 
<img src="https://github.com/bioinformaticsdotca/BiCG_2017/blob/master/IntegrativeAssignment/Images/Galaxy07.JPG?raw=true" alt="Choose local file" width="750" /> 
<img src="https://github.com/bioinformaticsdotca/BiCG_2017/blob/master/IntegrativeAssignment/Images/Galaxy08.JPG?raw=true" alt="Choose local file" width="750" /> 
<img src="https://github.com/bioinformaticsdotca/BiCG_2017/blob/master/IntegrativeAssignment/Images/Galaxy09.JPG?raw=true" alt="Choose local file" width="750" /> 
<img src="https://github.com/bioinformaticsdotca/BiCG_2017/blob/master/IntegrativeAssignment/Images/Galaxy10.JPG?raw=true" alt="Choose local file" width="750" /> 

At the end of this section, we should see 14 files in our history.

<img src="https://github.com/bioinformaticsdotca/BiCG_2017/blob/master/IntegrativeAssignment/Images/Galaxy11.JPG?raw=true" alt="End of load data" width="500" /> 


Now that our data is uploaded, we can begin our analysis. __Normally we'd begin with doing some QC on our rna-sequencing data; unfortunately however, our data is in fasta format, and so we have to forego that step__

## Transcript alignment using Hisat

Let's begin with our transcript alignment/assembly using Hisat. Navigate to the *NGS: RNA Analysis* button on the left hand side, click it, find *Hisat*, and click on that. Alternatively, you can search for *Hisat* in the search tools bar.

<img src="https://github.com/bioinformaticsdotca/BiCG_2017/blob/master/IntegrativeAssignment/Images/Galaxy12.JPG?raw=true" alt="Finding Hisat" width="750" /> 

Now to run Hisat, we're going to make a few modifications. Change:
* *Input data format* to FASTA
* *Single end or paired end?* to Individual paired reads
* *Forward reads* to multiple datasets
* *Reverse reads* to multiple datasets
* *Source for the reference genome to align against* to Use a genome from history
* *Select the reference genome* to 14: Homo_sapiens.GRCh38.dna.chromosome.9.fa

Now in the forward reads, we're going to go ahead and select all our read1 reads. For the reverse reads, we're going to select the read2 reads. The screen should look as follows:

<img src="https://github.com/bioinformaticsdotca/BiCG_2017/blob/master/IntegrativeAssignment/Images/Galaxy14.JPG?raw=true" alt="HiSat modified" width="750" /> 

Now just press run. You should see the following:

<img src="https://github.com/bioinformaticsdotca/BiCG_2017/blob/master/IntegrativeAssignment/Images/Galaxy15.JPG?raw=true" alt="HiSat modified" width="750" /> 

While we wait for Hisat to align our data to our reference, we're going to explore our data and the Galaxy environment to see other features it has. We can look into our fasta file from earlier to see the format of the data. This is accomplished by pressing on the eye button beside the file:

<img src="https://github.com/bioinformaticsdotca/BiCG_2017/blob/master/IntegrativeAssignment/Images/Galaxy17_lookingatdatawhilewaiting.JPG?raw=true" alt="Looking at our fasta" width="750" />

We can also look at the gtf file we uploaded previously. Similarly, press the eye on the gtf file.

<img src="https://github.com/bioinformaticsdotca/BiCG_2017/blob/master/IntegrativeAssignment/Images/Galaxy19_lookingatdatawhilewaiting.JPG?raw=true" alt="Looking at our fasta 2" width="750" />

As we can see, the gtf file is column seperated and contains information about the chromosome, source of the feature, the feature type, start, end, and other information.

If you wanted to test out tools on data that you don't have yet, Galaxy has publicly available datasets for a range of different data types.

<img src="https://github.com/bioinformaticsdotca/BiCG_2017/blob/master/IntegrativeAssignment/Images/Galaxy20_lookingatdatawhilewaiting.jpg?raw=true" alt="Clock on data" width="750" />

For example, if we didn't have RNA seq data, we could grab some by going into the Demonstration Datasets, and navigating into the Human RNA-seq folder, where two cell lines are stored in fastq format while a reference is kept as a fasta file.

<img src="https://github.com/bioinformaticsdotca/BiCG_2017/blob/master/IntegrativeAssignment/Images/Galaxy21_lookingatdatawhilewaiting.JPG?raw=true" alt="Go into demonstration" width="750" />
<img src="https://github.com/bioinformaticsdotca/BiCG_2017/blob/master/IntegrativeAssignment/Images/Galaxy22_lookingatdatawhilewaiting.JPG?raw=true" alt="Go into human rna" width="750" />
<img src="https://github.com/bioinformaticsdotca/BiCG_2017/blob/master/IntegrativeAssignment/Images/Galaxy22_lookingatdatawhilewaiting_2.JPG?raw=true" alt="Look at cell line files" width="750" />

Now instead of looking at example data, we can also look at workflows published by other people for gaining ideas on how to run our other analysis.

<img src="<img src="https://github.com/bioinformaticsdotca/BiCG_2017/blob/master/IntegrativeAssignment/Images/Galaxy23_lookingatdatawhilewaiting.jpg?raw=true" alt="Looking at our gtf file 2" width="750" />
<img src="<img src="https://github.com/bioinformaticsdotca/BiCG_2017/blob/master/IntegrativeAssignment/Images/Galaxy24_lookingatdatawhilewaiting.JPG?raw=true" alt="Looking at our gtf file 2" width="750" />
<img src="<img src="https://github.com/bioinformaticsdotca/BiCG_2017/blob/master/IntegrativeAssignment/Images/Galaxy25_lookingatdatawhilewaiting.JPG?raw=true" alt="Looking at our gtf file 2" width="750" />

Let's go back to the home page and see whether the alignment has finished.

## Transcript assembly and quantification using Cufflinks

Now we're going to run cufflinks to assemble our transcripts and quantify them.

To do this, type _Cufflinks_ in the search bar and click on the program. Once opened, modify the options by changing:
* _SAM or BAM of aligned RNA-Seq reads_ to multiple datasets
* _Use reference annotation_ to use reference annotation
* _Reference annotation_ to 1: Homo_sapiens.GRCh38.86.chr9.gtf

Make sure to select all the outputs in the _SAM or BAM of aligned RNA-Seq reads_. Leave all other options on default, and press run.

<img src="https://github.com/bioinformaticsdotca/BiCG_2017/blob/master/IntegrativeAssignment/Images/Galaxy27.JPG?raw=true" alt="Running Cufflinks" width="750" />

<img src="https://github.com/bioinformaticsdotca/BiCG_2017/blob/master/IntegrativeAssignment/Images/Galaxy28.JPG?raw=true" alt="Running Cufflinks" width="750" />


## Merging transcript quantification from Cufflinks

Next, we're going to combine our transcript abundances from Cufflinks using the Cuffmerge program. Like before, type _Cuffmerge_ in the search options to the left, select the program, and then modify it as follows:
* _GTF file(s) produced by Cufflinks_ to multiple
* _Use reference annotation_ to use reference annotation
* _Reference annotation_ to 1: Homo_sapiens.GRCh38.86.chr9.gtf

Select only the assembled Transcripts in the _GTF file(s) produced by Cufflinks_. Leave all other options on default, and press run.

<img src="https://github.com/bioinformaticsdotca/BiCG_2017/blob/master/IntegrativeAssignment/Images/Galaxy31.JPG?raw=true" alt="Running Cuffmerge" width="750" />

## Differential expression analysis using Cuffdiff

Finally we're going to perform the differential expression analysis between our two groups using the outputs from Hisat and cuffmerge. Find Cuffdiff in the search bar and select it, and make the following changes:

* _Transcripts_ to Cuffmerge on data...
* _1: Condition Name_ to Carcinoma
* Select the Carcinoma samples: datasets 14, 15, 16
* _2: Condition Name_ to Normal
* Select the Normal samples: datasets 17, 18, 19

Leave everything else on default, and execute the command.

<img src="https://github.com/bioinformaticsdotca/BiCG_2017/blob/master/IntegrativeAssignment/Images/Galaxy32.JPG?raw=true" alt="Running Cuffdiff" width="750" />
<img src="https://github.com/bioinformaticsdotca/BiCG_2017/blob/master/IntegrativeAssignment/Images/Galaxy32_2.JPG?raw=true" alt="Running Cuffdiff" width="750" />

Cuffdiff will generate differential expression results based on genes, transcripts, TSS, promoters, CDS, and splicing. We're going to look into the gene based differential expression, but feel free to peer into the other files.

Click on the eye of the _Cuffdiff on data 20, data 19, and others: gene differential expression testing_ to view the contents of the file. As we can see from the file, it contains the gene id, gene name, locus, the annotation for the samples, whether a test for significant differential expression was/could be performed, the normalized gene counts, log2 fold change, significance, false positive value, and finally whether the gene is significantly differentially expressed.

<img src="https://github.com/bioinformaticsdotca/BiCG_2017/blob/master/IntegrativeAssignment/Images/Galaxy33.JPG?raw=true" alt="Viewing output Cuffdiff" width="750" />

Alternatively, the file can be downloaded and opened in Excel for reordering by, for example, status in the significant column:

<img src="https://github.com/bioinformaticsdotca/BiCG_2017/blob/master/IntegrativeAssignment/Images/Galaxy34.JPG?raw=true" alt="Downloading output" width="750" />
<img src="https://github.com/bioinformaticsdotca/BiCG_2017/blob/master/IntegrativeAssignment/Images/Galaxy35.JPG?raw=true" alt="Opening output in excel" width="750" />
<img src="https://github.com/bioinformaticsdotca/BiCG_2017/blob/master/IntegrativeAssignment/Images/Galaxy36.jpg?raw=true" alt="Excel reordering 1" width="750" />
<img src="https://github.com/bioinformaticsdotca/BiCG_2017/blob/master/IntegrativeAssignment/Images/Galaxy37.JPG?raw=true" alt="Excel reordering 2" width="750" />
<img src="https://github.com/bioinformaticsdotca/BiCG_2017/blob/master/IntegrativeAssignment/Images/Galaxy38.JPG?raw=true" alt="Excel reordering 2" width="750" />

Finally, we're going to extract our workflow to be able to save and rerun it at a later time. This also helps to visually see the steps that were taken and the connections between the programs. 

<img src="https://github.com/bioinformaticsdotca/BiCG_2017/blob/master/IntegrativeAssignment/Images/Galaxy39_exporting_workflow.jpg?raw=true" alt="Extract workflow from history" width="750" />
<img src="https://github.com/bioinformaticsdotca/BiCG_2017/blob/master/IntegrativeAssignment/Images/Galaxy40_exporting_workflow.jpg?raw=true" alt="Accept all selected programs" width="750" />
<img src="https://github.com/bioinformaticsdotca/BiCG_2017/blob/master/IntegrativeAssignment/Images/Galaxy41_exporting_workflow.jpg?raw=true" alt="Click on workflow after exporting it" width="750" />
<img src="https://github.com/bioinformaticsdotca/BiCG_2017/blob/master/IntegrativeAssignment/Images/Galaxy42_exporting_workflow.jpg?raw=true" alt="Path to viewing our workflow" width="750" />
<img src="https://github.com/bioinformaticsdotca/BiCG_2017/blob/master/IntegrativeAssignment/Images/Galaxy43_exporting_workflow.jpg?raw=true" alt="Looking at workflow" width="750" />

This concludes the Galaxy tutorial. But this is still only an introduction - there's plenty of other analysis you can perform using the Galaxy server so it is encouraged to test different workflows!
