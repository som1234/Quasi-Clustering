# Quasi-Clustering
Description : 
This is an Viral Quasispecies Reconstruction Software to solve the Quasispecies Reconstruction problem. This project contains the software implementation of a novel algorithm based on semidefinite relaxation based correlation clustering approach for the Quasispecies problem. Specifically, our software has the following function - 
    1) Reconstruct Full Length Haplotypes from Reference genome and Aligned Reads
    2) Estimate the abundances of individual species in the mixture 
    3) Choose the optimal number of quasispecies variants  present in the mixture

Progam Files:
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
        - quasi_clus

Data File:
    - Ecoli.fasta
    - Ecoli.sam 
    - Ecoli.vcf 


Software Requirements: 
    1) Python 2.7 or above 
    	- Packages : pysam, pyvcf
    2) ATLAS and LAPACK for gcc compilation
    3) Samtools


Input Data: 
    1) Reference genome in *.fasta format
    2) Sam file containing reads aligned to the above reference genome
    3) vcf file generated based on the aligned reads and reference as above. 


Steps: 
    1) Unzip the Source files in to local directory. We will refer to the full path to this directory as SOURCE. 
    2) Transfer the input data files to another local directory.  We will refer to the full path of this directory as DATA.  
    3) Denote the full path to the directory where Samtools is installed as SAMTOOLS
    4) Navigate to SOURCE directory and change the Permission of the file SDHAP_master.sh as follows : 
	    chmod 755 SDHAP_master.sh
    5) Navigate to DATA directory and type the following command to start the quasispecies reconstruction : 
    	SOURCE/SDHAP_master.sh K1 K2 SOURCE DATA NAME REG1 REG2 SAMTOOLS
	    where, the arguments are explained as follows -
	    K1,K2 - start and end value of number of quasispecies variants for model selection
	    NAME - ascii string denoting name of the experiment (user chooses)
	    REG1, REG2 - start and end of the genomic region along the reference over which quasispecies reconstruction is performed 
    NOTE: Rename the input files *.fasta,*.sam and *.vcf to NAME.fasta, NAME.sam and NAME.vcf before running the program
	

Sample Run: 
    Let's assume the source files are located in /home/unga/sbarik and data files are located in /home/unga/sbarik/sample_data
    chmod 755 /home/unga/sbarik/SDHAP_master.sh; 
    cd /home/unga/sbarik/sample_data; 
    /home/unga/sbarik/SDHAP_master.sh 2 10 /home/unga/sbarik /home/unga/sbarik/sample_data Ecoli 1 10000 /home/unga/sbarik/samtools/bin
	

Output Files: 
    Main file 
        - NAME_K_recon.fasta - Full length Reconstructed Quasispecies Fasta file with 'K' haplotypes and their frequencies (e.g. Ecoli_2_recon.fasta)
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
        -read_snp_info.txt


