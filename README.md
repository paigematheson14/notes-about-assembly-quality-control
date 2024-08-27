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

# Sequencing process:

# 1. Library preparation

**DNA extraction:** In both Nanopore and Illumina sequencing, high molecular weight DNA is extracted from the sample (we used DNEasy blood and tissue kit)

**Nanopore Library construction:** The DNA is prepared for sequencing by attaching adapters to the ends of the DNA fragments. These adapters are necessary for the DNA to interact with the nanopores and be recognised by the sequencer.

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

*Their primary function is to initiate DNA synthesis: 

-In PCR, primers are used to amplify specific regions of DNA. Two primers are used: a forward primer and a reverse primer. The forward primer binds to the 3' end of the target sequence on one strand, while the reverse primer binds to the complementary strand in the opposite direction. This setup allows DNA polymerase (an enzyme that plays a crucial role in DNA replication and repair; it catalyses the synthesis of new DNA strands by adding nucleotides to a growing DNA chain based on the template strand) to extend the new strand from both primers, amplifying the region between them. 

-In DNA sequencing, primers are used to initiate the sequencing reactions. The primer binds to the template DNA and provides a starting point for DNA polymerase to synthasise the new strand while incoroporating fluorescently labeled nucleotides to determine the sequence.*

# 2. Loading the flow cell
Flow cell: The prepared library (including adapters/barcodes)is loaded onto a flow cell which is specialised depending on the sequencer.

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

# 3. Sequencing**

### *Nanopore* ###
**DNA translocation**: The DNA is driven through the nanopores. As they pass through, the electrical current changes in a manner that is specific to each DNA base. This current change is continuously recorded. 

**Signal detection**: The electrical signals are converted into digital data, which is then used to determine the sequence of DNA bases.

### *Illumina* ###
**Sequencing by synthesis**

**Sequencing reactions**: During sequencing, fluroscently labeled nucleotides (A, T, C, G) are added to the flow cell. Each nucleotide incorporates into the growing DNA strand, and this incorporation is detected by a camera. 

**Fluorescent detection***: Each time a nucleotide is added, it emits a specific fluroscent signal. The system captures these signals to determine which base (A, T, C, G) was added at each position in the DNA fragment

**Read generation**: The sequencing machine records these fluorescent signals and generates a sequence read, which is the raw sequence data of the DNA fragment

# 4. Data Analysis
**- Base Calling**: The raw signal data from the electrical current changes (ONT) or fluorescent signals (Illumina) are processed using basecalling algorithms to determine the sequence of bases in the DNA.

**- Data processing**: The basecalled sequences are then assembled and analysed to provide insights into the genetic information. 

# Key features of PromethION:
**Long Reads:** One of the main advantages of ONT is its ability to generate very long reads, often spanning thousands to hundreds of thousands of bases. This is useful for resolving complex genomic regions, repetitive sequences, and structural variants. 

**High throughput**: The PromethION is capable of producing large amounts of sequencing data, making it suitable for large-scale projects and comprehensive genome analysis

**Real time sequencing**: Nanopore sequencing can provide data in real time as the DNA molecules pass through the nanopores. This allows for immediate analysis and potentially faster results 

# Key features of Illumina data:
**High throughput**: Illumina sequencing generates millions of reads in a single run, providing comprehensive coverage of the genome or transcriptome

**Short reads**: Illumina technology typically produces relatively short reads, often ranging from 75-300 bases in length. These reads are highly accurate, but may need to be assembled to cover longer genomic regions 

**High accuracy**: Illumina sequencing is known for its high accuracy and reliability, making it a popular choice for various genomic studies 





