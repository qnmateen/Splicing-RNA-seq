# Splicing-RNA-seq
RNA seq data splicing using DEXSeq


## Steps Involve

### 1. Take fastq file
       Trim it
       Align it to genome to get sam/bam file
       
### 2. Download your gtf file

### 3. Using R, install DEXSeq package

### 4. Locate dexseq_prepare_annotation.py
       Now use this file to make the annotation file that will be in gff format
       
       
   ### Please install HTSeq using conda
       
### 5. Make gff file 
       using this command
       
       python /DATA/anshul/covid_lung_analysis/DEXseq_counts/dexseq_prepare_annotation.py /nfs_master/noorul/Gencode_mouse/gencode.vM27.primary_assembly.annotation.gtf gencode.vM27.primary_assembly.annotation.DEXSeq.chr.gff
       
### 6. DEXSeq code  
      
     make a .sh file
       #!/bin/bash


       mkdir DEXseq

       cwd=$(pwd)
       outpt=$cwd/DEXseq

       inpt=$cwd/star_result
       N=15
       while read i
       do
           ((j=j%N)); ((j++==0)) && wait
           python /DATA/anshul/covid_lung_analysis/DEXseq_counts/dexseq_count.py -p no -f bam -s no             /nfs_master/noorul/noorul2/mouse_data_nafld/gencode.vM27.primary_assembly.annotation.DEXSeq.chr.gff   "$inpt/${i}"Aligned.sortedByCoord.out.bam    "$outpt/${i}"DEXseqCounts.txt &
       done < "sample_list1"


In this code - we need to probide the dexseq python script that we get from the package installed, the flattened gff file which we made from gtf file and aligned bam files that we take from STAR result.


### 7. Run .sh file

The output will be .txt file for each sample


### Now the further analysis will be performed on R

So first use R in cluster using -X mode on mac and install XQuartz

module load codes/R-4.1.1

### Codes for R

       if (!require("BiocManager", quietly = TRUE))
       install.packages("BiocManager")

       BiocManager::install("DEXSeq")
       
       library("DEXSeq")
       
       



