# Notes-about-genome-assembly-and-quality-control
This repository includes notes about genome assemblies and assessing the quality of genome assemblies (i.e., what all of the different metrics mean)

# What is a genome assembly?
A genome assembly is the process of piecing together the complete DNA sequence of an organism's genome from shorter DNA fragments. It is an essential step in genomics and involves several key stages. 

There are several different methods for sequencing. The data I have for my genome assemblies are **long-read PromethION Nanopore data** and **short-read Illumina data**. 

### **PromethION Nanopore** ###
PromethION is a high-thoroughput sequencer developed by Oxford Nanopore Technologies (ONT). It is designed for generating long-read DNA sequencing data. Unlike traditional sequencing methods, which rely on detecting fluroscent signals or chemical reactions, nanopore sequencing uses a different approach to read DNA sequences. 

Nanopore sequencing involves passing a DNA molecule through a tiny protein nanopore embedded in a membrane. As the DNA strand translocated through the nanopore, changes in electrical current are measured. Each DNA base (i.e., A, T, G, C) causes a characteristic disruption in the current, allowing the sequence of bases to be inferred. 

### **Illumina sequencing** ###
Illumina sequencing, also known as sequencing by synthesis (SBS), is a method that generates large volumes of DNA sequence data with high accuracy. It is commonly used for whole genome sequencing, targeted sequencing, RNA sequencing, and other applications. 

# 1. SEQUENCING:
The first step to creating a genome assembly is to sequence the DNA from an organism. The following notes describe, in detail, the SEQUENCING PROCESS:

# 1a. Library preparation

**DNA extraction:** In both Nanopore and Illumina sequencing, high molecular weight DNA is extracted from the sample (we used DNEasy blood and tissue kit)

### **Nanopore Library construction:** ###
The DNA is prepared for sequencing by attaching adapters to the ends of the DNA fragments. These adapters are necessary for the DNA to interact with the nanopores and be recognised by the sequencer.

### **Illumina Library construction:** ###

**Fragmentation**: The extracted DNA is fragmented into smaller pieces

**Adapter ligation**: Short DNA sequences called adapters are ligated to both ends of each fragment. These adapters are crucial for the sequencing process as they allow the fragments to bind to the flow cell and serve as primers during sequencing. 

**Amplification**: The library is often amplified (increased in quantity) through a process called PCR (polymerase chain reaction). This ensures there is enough material for sequencing. 

#### ***What is an adapter??????*** 
*In the context of DNA sequencing, an adapter is a short, synthetic, DNA sequence that is attached to the ends of DNA fragments during library preperation. Adapters serve several important functions in the sequencing process. For example:*

*- They **bind to the sequencer** (e.g., the flow cell or nanopores) allowing the DNA fragments to be captured and processed by the sequencer*

*- In sequencing methods that involve amplification (i.e., PCR), adaptaers provide the necessary sequences for the DNA fragments to be **amplified**, increasing the amount of DNA available for sequencing*

*- They contain unique **index sequences** (or barcodes) that enable the simultaneous sequencing of multiple samples in a single run. These index sequences are used to differentiate between samples and sort the data accordingly*

*During library preparation, adapters (which can either be **universal**; standard adapters designed to interact with the common features of the sequencer, or **custom**; adapters specific for certain sequencing platforms and may include additional features such as unique index sequences for multiplexing or specific sequences needed for certain technologies) are ligated (chemically joined) to the ends of the DNA fragments. This process is crucial for enabling the fragments to be recognised and processed by the sequencing technology. Once the DNA fragments are attached to the adapters, they are loaded onto the sequencer. These adapters facilitate the binding of these fragments to the sequencing platform, and endable the sequencing reactions to occur. After sequencing, the data generated includes the sequences of DNA fragments along with the adapter sequences. During data analysis, the adapters are usually trimmed off to focus on the actual genomic sequences* 

#### ***What is a primer?????*** 

*A primer is a short, single stranded nucleic acid sequence used to initiate the synthesis of a complementary strand of DNA or RNA. Primers are crucial for various applications, including polymerase chain reaction (PCR) sequencing, and other nucleic acid amplification methods.*

*They are typically 15-30 nucleotides long. Their sequence is designed to be complementary to a specific region of the target DNA or RNA. This complementary binding ensures that the primer can anneal to the correct location on the template strand. They are also designed with a specific orientation to match the direction in which DNA polymerase will synthesise the new strand.*

*Their primary function is to initiate DNA synthesis:*

*-In PCR, primers are used to amplify specific regions of DNA. Two primers are used: a forward primer and a reverse primer. The forward primer binds to the 3' end of the target sequence on one strand, while the reverse primer binds to the complementary strand in the opposite direction. This setup allows DNA polymerase (an enzyme that plays a crucial role in DNA replication and repair; it catalyses the synthesis of new DNA strands by adding nucleotides to a growing DNA chain based on the template strand) to extend the new strand from both primers, amplifying the region between them.*

*-In DNA sequencing, primers are used to initiate the sequencing reactions. The primer binds to the template DNA and provides a starting point for DNA polymerase to synthasise the new strand while incoroporating fluorescently labeled nucleotides to determine the sequence.*

# 1b. Loading the flow cell
The prepared library (including adapters/barcodes)is loaded onto a flow cell which is specialised depending on the sequencer.

#### ***What is a flow cell????*** 

*A flow cell is the environment where the actual sequencing reactions take place. The flow cell usually consists of a series of channels or wells where DNA molecules are held and processed. These channels are designed to facilitate the flow of fluids and reagents needed for sequencing.*

*The interior surfaces of the flow cell are often coated with materials that help capture and immobolise the DNA fragments or other molecules of interest. For example, in Illumina sequencing, the surface is coated with oligonucleotides that bind the DNA fragments. Many flow cells incorperate optical elements, such as glass or plastic that allows light to pass through. This is crucial for capturing the flurescent signals emitted during sequencing, which are used to determine the DNA sequence.*

*The flow cell main functions:*

*- Capture and immobilisation: During the sequencing process, DNA fragments or molecules are loaded onto the flow cell where they are captured and immobilised on the surface. This allows for a controlled environment where sequencing reactions can occur.*

*- Sequencing reactions: The flow cell supports the sequencing chemistry, whether its based on detecting fluroscent signals (i.e., Illumina sequencing) or measuring electrical changes (i.e., ONT sequencing)*

***- Illumina flow cell**: These have a surface coated with oligonucleotides (short sequence of nucleotides, few to several dozen bases long) that bind DNA fragments. During sequencing, fluorescently labeled nucleotides are incorporated into the DNA, and the flow cell captures the resulting fluorescent signals to determine the sequence.*

***- Oxford Nanopore flow cell**: In nanopore sequencing, the flow cell contains nanopores embedded in a membrane. DNA molecules pass through these pores, and changes in electrical current are measured to determine the DNA sequence.*

# *Illumina only* 3. Cluser generation

**Bridge amplification**: In the flow cell, each DNA fragment with its adapters is locally amplified. This process creates millions of clusers of identical DNA fragments. Each cluster originates from a single DNA fragment and contains many copies of it. 

# 1c. Sequencing

### *Nanopore* ###
**DNA translocation**: The DNA is driven through the nanopores. As they pass through, the electrical current changes in a manner that is specific to each DNA base. This current change is continuously recorded. 

**Signal detection**: The electrical signals are converted into digital data, which is then used to determine the sequence of DNA bases.

### *Illumina* ###
**Sequencing by synthesis**

**Sequencing reactions**: During sequencing, fluroscently labeled nucleotides (A, T, C, G) are added to the flow cell. Each nucleotide incorporates into the growing DNA strand, and this incorporation is detected by a camera. 

**Fluorescent detection***: Each time a nucleotide is added, it emits a specific fluroscent signal. The system captures these signals to determine which base (A, T, C, G) was added at each position in the DNA fragment

**Read generation**: The sequencing machine records these fluorescent signals and generates a sequence read, which is the raw sequence data of the DNA fragment

# Key features of PromethION:
**Long Reads:** One of the main advantages of ONT is its ability to generate very long reads, often spanning thousands to hundreds of thousands of bases. This is useful for resolving complex genomic regions, repetitive sequences, and structural variants. 

**High throughput**: The PromethION is capable of producing large amounts of sequencing data, making it suitable for large-scale projects and comprehensive genome analysis

**Real time sequencing**: Nanopore sequencing can provide data in real time as the DNA molecules pass through the nanopores. This allows for immediate analysis and potentially faster results 

# Key features of Illumina data:
**High throughput**: Illumina sequencing generates millions of reads in a single run, providing comprehensive coverage of the genome or transcriptome

**Short reads**: Illumina technology typically produces relatively short reads, often ranging from 75-300 bases in length. These reads are highly accurate, but may need to be assembled to cover longer genomic regions 

**High accuracy**: Illumina sequencing is known for its high accuracy and reliability, making it a popular choice for various genomic studies 

**Obtaining high quality sequencing reads is important. In my methods, I used ONT PromethION long reads to assemble my genome (as it can resolve repetitive regions and generally more informative), and then used Illumina short-reads to polish my assembly (as Illumina is more accurate).**

# GENOME ASSEMBLY FROM THE RAW SEQUENCE DATA

# 1. Base Calling: 

The raw signal data from the electrical current changes (ONT) or fluorescent signals (Illumina) are processed using basecalling algorithms to determine the sequence of bases in the DNA. Essentially it's the process of converting the raw data produced during sequencing into readable nucleotide sequences. The output of basecalling is a sequence file (e.g., in formats like FASTQ). 

**Even though I was provided with FASTQ files (i.e., already basecalled) from ONT, we decided to do basecalling of the raw SLOW5 files ourselves. This is because ONT still uses GUPPY to basecall and we wanted to use Dorado which is more accurate**

#### What is Dorado? 

Dorado is a basecaller designed for Oxford Nanopore Technologies sequencing data. It is known for its ability to process long-read sequencing data with a focus on **high accuracy**. Dorado uses machine learning techniques to improve basecalling performance and reduce error rates compared to some earlier methods. 

Dorado (developed by Nabsys) is a good basecaller due to its improved accuracy and ability to handle the complexities of long-read sequencing. Compared to Guppy (which was developed by ONT, and is still robust with extensive support and consistently good across various datasets), Dorado potentially offers improved basecalling accuracy, especially for long reads and better performance in specific scenarios (e.g., complex or noisy data). Apparently, ONT will begin using Dorado as their main basecaller in the future! 

# 2. Demultiplexing
Demultiplexing is a process used to separate and sort sequences generated from multiple samples that were pooled together during the sequencing run. This is essential when a single sequencing run is used to analyse several samples simultaneously, which is a common practice to increase efficiency and reduce costs. 

Heres how it works: 

#### Sample pooling: 
during library prep, each sample is tagged with a unique barcode or index sequence. These barcodes are short DNA sequences that are added to each sample to distinguish it from others. 

#### Sequencing: 
All the samples, each with their unique barcode, are combined and sequenced together in a single run. This means the raw sequencing data contains sequences from all samples mixed together

#### Data processing: 
After sequencing, the raw data includes the sequences of the barcodes along with the actual DNA sequences. ***Demultiplexing involves using these barcode sequences to sort the mixed data back into separate files each corresponding to the original sample.*** 

#### Output: 
The demultiplexed data consists of separate sequence files for each sample, which can then be analysed individually. This separation is crucial for accurate analysis and interpretation of the data. 

**My data had four samples which each corresponded to the four Calliphora species. I used the demux function implemented in Dorado to demultiplex my samples. The output file from Dorado was .bam. I converted the BAM files into FastQ files using samtools. Samtools is the best and fasted for insect genomes**

# Quality control of FastQ files 
I used NanoPlot to look into the quality of my fastq files. 

Nanoplot is a tool designed for visualising and assessing the quality of long-read sequencing data generated by Nanopore sequencing technologies. It provides graphical summaries and metrics that help researchers evaluate the quality of their sequencing runs and datasets. 

# Key Features

# Quality visualisation 

### Read Length Distribution

Displays histograms or cumulative plots of read lengths to provide an overview of the size distribution of the reads in your dataset. 

***What is read length?***

*This refers to the length of each individual sequence read. For example, if a sequencing run generates reads that are 1000 bases long on average, the read length distribution will reflect this average length along with the variability in read lengths.*

***Key metrics of read length***

*- Mean read length - the average length of all reads in the dataset*

*- Median read length - the middle value of the read lengths when they are sorted in ascending order, which can be more informative than the mean in the presence of outliers*

*- Read length range - the range from the shortest to the longest read, indicating the spread of read lengths.*

#### Data quality assessment of read length
**Consistency**

A narrow distribution with relatively uniform read lengths often indicates a **high-quality** sequencing run, whereas a wide distribution might suggest issues like sequencing errors or problems with library preparation

**Error rates**

Longer reads are generally more challenging to generate with high accuracy. A distribution with a high proportion of long reads might indicate potential issues with read accuracy or error rates. 

**Downstream applications**

For long read sequencing technologies, **longer reads are advantageous** for assembing complex genomes and resolving repetitive regions. A distribution with a high proportion of long reads is beneficial for assembly quality. 


### Read Quality Scores

Shows distributions of quality scores, helping to assess the accuracy of the sequencing data. Read quality scores measure the *confidence in each base call made during sequencing*. In other words, they quantify the likelihood that a particular base (C, T, G, A) is **correct**. They are typically represented as Phred scores in sequencing data 

**Phred scores**

Each score is derived from the probability of an incorrect base call. For instance, a Phred score of Q20 indicates a 1% error rate (or a 99% probability of correctness). Phred scores are usually integers ranging from 0-40 or higher. Higher scores indicate greater confidence or accuracy in the base call. Reads with low-quality scores are often FILTERED OUT OR TRIMMED to improve the overall quality of the dataset before analysis. 

Quality score distributions are often visualised using histograms, showing the frequency of different score ranges across the dataset. Plotting quality scores across each base position in the reads can **reveal patterns**, such as decreasing quality towards the end of reads, which is common in some sequencing technologies. 

Accurate quality scores are crucial for reliable variant calling, as low-quality basecalls can lead to false positives or missed variants. High quality reads are essential for constructing accurate genome assemblies, especially in regions of the genome that are complex or repetitive. 

### Base composition
Refers to the relative abundance of the four nucleotide bases. Analysing base composition can provide valuable insights including sequence characteristics, genomic features, and the quality of sequencing data. Nanoplot provides plots of the base composition (e.g., GC content) to understand the nucleotide distribution across the reads. 

**Quality control**

Anomolies in base composition, such as unexpected GC content or deviations from expected distributions can indicate sequencing errors or biases. For example, high GC content in a region might suggest a potential issue with the sequencing technology or library preparation. Base composition can also help investigate GC content and identify repeat regions (repetitive sequences or regions with unusual base composition, which may be relevant in studies of genome structure or function).

***What is GC content????***

*GC content is the proportion of G and C bases and is a key feature of many genomes. It can influence gene expression, DNA stability, and the formation of secondary structures. GC-rich regions are often associated with regulatory elements, while AT-rich regions might be more gene-poor.*

***Comparing base composition across different species can reveal evolutionary patterns, adaptations, and genomic differences. For example, some species might have a higher GC content compared to others, reflecting their adaptation to specific environments***


Base composition can also be used in genome annotation to identify potential **coding regions, regulatory elements, and other functional features.** Abnormal base composition can help refine annotations and improve genome assembly. 

# Read statistics 

### Basic metrics
Calculates and presents basic statistics such as the total number of reads, total base pairs, average read length, and median read length

### Read counts 
Summarises the number of reads within different length or quality score bins 

# Duplicate reads 
My genome assembly had a lot of duplicate reads. 

Duplicate reads in genome assemblies can arise from various sources and are often encountered during sequencing and data processing. Understanding why duplicates occur and how they can impact genome assemblies is important for improving the quality and accuracy of the resulting genomic data. 

### Causes of duplicate reads 

#### Sequencing artifacts 
**Library preparation:** particularly in protocols were PCR amplification is used, duplicates can arise if the same DNA fragment is amplified multiple times. This is common in high through-put sequencing where amplification steps are necessary to generate sufficient DNA for sequencing. 

**Sequencing process:** Multiple runs, e.g., if the same sample if sequenced across multiple runs or lanes, duplicates can appear if the sequencing platform generates overlapping reads from the same DNA fragments in different runs. Or overlapping regions - e.g., if the same genomic region is covered by multiple reads 

**Data handling and processing:** Merging reads or datasets can lead to the presence of duplicate reads 

### Impact of duplicate reads 

Duplicate reads can **skew the representation of certain regions of the genome, leading to overrepresentation** of those regions in the assembly. This can affect the assembly and representation of the genome. 

Duplicates can also complicate the assembly process, especially in regions with repetitive sequences, making it **harder to accurately resolve these regions**. 

Duplicates can also impact variant calling by **introducing false positives or reducing sensitivity to real variants**. Accurate variant detection requires careful balance between handling duplicates and maintaining sensitivity. 

Duplicates can also **introduce bias** in downstream analyses, such as gene expression studies, function annotation, and comparative genomes, leading to potential inaccuracies. 

Therefore it is imporant to do quality control checks and process the data post-assembly using tools to remove the duplicate reads. 
























**- Data processing**: The basecalled sequences are then assembled and analysed to provide insights into the genetic information. 



# 2. OVERLAPPING
Once the DNA fragments are sequenced, the next step is to find overlaps between these fragments. This is crucial because the DNA fragments generated from sequencing are usually too short to cover the entire genome, and identifying where they overlap helps in reconstructing the original sequence. 

**Overlap-Layout-Consensus**- this algorithmic approach involves identifying overlaps between fragments, creating a layout of these overlaps, and then generating a consensus sequence that best represents the original DNA. 

**De Bruijn graphs**: In this method, short sequences (k-mers) are used to build up a graph where these nodes represent these k-mers, and edges represent overlaps. The genome assembly is constructed by traversing the graph and connecting nodes to reconstruct the original sequences. 

# 3. ASSEMBLING 
The assembly process involves stitching together the overlapping fragments to form longer, continuous sequences called contigs, which can then make up the complete genome. This can be broadly categorised into two types: de novo (no reference genome) and reference based (aligning reads to a known reference genome of a closely related species and using that alignment to assemble the genome). My genome assembly is DE NOVO!!

In de novo assembly, the goal is to construct the complete genome sequence directly from the sequenced DNA fragments. 

### Key steps in De Novo Genome Assembly ###

#### Sequencing







