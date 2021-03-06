#Quasi-Clustering

## Description: 

This is an Viral Quasispecies Reconstruction Software to solve the Quasispecies Reconstruction problem. This project contains the software implementation of a novel algorithm based on semidefinite relaxation based correlation clustering approach for the Quasispecies problem. Specifically, our software has the following function 

    - 1) Reconstruct Full Length Haplotypes from Reference genome and Aligned Reads
    - 2) Estimate the abundances of individual species in the mixture 
    - 3) Choose the optimal number of quasispecies variants  present in the mixture


## Files:
### Source Files:
    Python Scripts 
   
        - SDHAP_vcf_to_snp.py
        - SDHAP_create_frag.py
        - SDHAP_K_iter.py
        - SDHAP_F.py
        - SDHAP_F_class.py
        - SDHAP_class.py
        - SDHAP_func.py
   
    Bash Scripts 
     
        - SDHAP_master.sh
        
    C files
    
        - quasi_clus.c
        - quasi_clus (executable)

### Sample Data File:
    - Ecoli.fasta
    - Ecoli.sam 
    - Ecoli.vcf 


## Software Requirements: 
* Python 2.7 or above (installation location should be included in $PATH)
* Python Packages : pysam
* ATLAS and LAPACK for gcc compilation
* Samtools

## OS Requirements: 

This software has been tested on Unix Debian 7 and RHEL 6 distribution. It has not been tested on Windows or Mac Platforms. 

## Input Data Required: 

* Reference genome in '*.fasta' format
* 'Sam' file containing reads aligned to the above reference genome
* 'vcf' file generated based on the aligned reads and reference as above. 


## Steps: 
    1) Unzip the Source files in to local directory. We will refer to the full path to this directory as SOURCE. 
    2) Transfer the input data files to another local directory.  We will refer to the full path of this directory as DATA.  
    3) Denote the full path to the directory where Samtools is installed as SAMTOOLS
    4) [Optional] Edit the file SDHAP_master.sh to change the default values of the following parameters 
    	Snp quality threshold (Lower threshold of Snp quality in VCF format)
    	sample Probability (for random sub sampling of reads) and 
    	read length thresholds (lower cutoff threshold for read lengths)
    	Also, if ATLAS in installed in non-standard location, then change the variables $ATLAS_LIB and $ATLAS_INCL accordingly in this file. 
    5) Navigate to SOURCE directory and change the Permission of the file SDHAP_master.sh as follows : 
        'chmod 755 SDHAP_master.sh'
    6) Navigate to DATA directory and type the following command to start the quasispecies reconstruction : 
    	'SOURCE/SDHAP_master.sh K1 K2 SOURCE DATA NAME REG1 REG2 SAMTOOLS'
	    where, the arguments are explained as follows -
	    'K1,K2' - start and end value of number of quasispecies variants for model selection (K1 > 1)
	    'NAME' - ascii string denoting name of the experiment (user chooses)
	    'REG1, REG2' - start and end of the genomic region along the reference over which quasispecies reconstruction is performed 

    'NOTE: Rename the input files *.fasta,*.sam and *.vcf to NAME.fasta, NAME.sam and NAME.vcf before running the program'
	

## Sample Run: 
    Download Sample data to a directory  DATA and source file to a directory SOURCE
    
    Type the following commands in a Bash shell - 
    *'chmod 755 SOURCE/SDHAP_master.sh;' 
    *'cd DATA/sample_data;' 
    *'SOURCE/SDHAP_master.sh 2 10 SOURCE DATA Ecoli 1 10000 SAMTOOLS'
	

## Output Files: 
    Main file 
        - NAME_K_recon.fasta - Full length Reconstructed Quasispecies Fasta file with 'K' haplotypes and their frequencies
        (e.g. Ecoli_2_recon.fasta)
    Secondary output files
        - NAME.frags (read-snp format)
        - NAME.snp (snp locations)
        - NAME_K_output.txt (snp-variant format) 
        - NAME.Fstats (Pseudo F statistics)
        - tmp_output.txt (Contains MEC, error rate  information)
    Temporary Files 
        - tmp_coverage_*.txt 
        - tmp_objective_*.txt
        - run_SDHAP.sh
        - read_snp_info.txt

### Contact Information : 

    Somsubhra Barik
    Electrical and Computer Engineering Department
    The University of Texas at Austin
    Austin
    Texas 78712
    USA
    email: sbarik@utexas.edu






