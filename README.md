[![Docker Cloud Automated build](https://img.shields.io/docker/cloud/automated/pinellolab/crispresso2.svg)](https://hub.docker.com/r/pinellolab/crispresso2)

# Customized-CRISPResso2-Code
CRISPResso2 NGS data analysis with customized docker script 
Referring to the ‘Source on Github’ (https://github.com/pinellolab/CRISPResso2), the Docker containerization system was installed and run using the following customized code templates based on the available script provided by [CRISPResso2](https://crispresso.pinellolab.partners.org/submission). Three biological replicates prepared for [Amplicon-EZ](https://web.genewiz.com/amplicon-ez-faq) were named ‘Rep1’ (as shown in the following codes), ‘Rep2’, ‘Rep3’, respectively. Multiple powershells (Windows) can be opened to run different scripts simultaneously. The ‘NNNNNNNNNNNNNNNNNNNN’ part of the following script can be replaced by the sequence of interest for customized analysis. The sequence of ‘guide_seq’ should match the corresponding sequence in ‘amplicon_seq’. 

Navigate to the directory with FASTQ data files using command line: 
```
cd "path of the directory"
```

##Base editing: 
```
docker run -v ${PWD}:/DATA -w /DATA -i pinellolab/crispresso2 CRISPResso --fastq_r1 Rep1_R1_001.fastq --fastq_r2 Rep1_R2_001.fastq --amplicon_seq NNNNNNNNNNNNNNNNNNNN --guide_seq NNNNNNNNNNNNNNNNNNNN --quantification_window_size 10 --quantification_window_center -10 --base_editor_output
```

NHEJ (non-homologous end joining):
```
docker run -v ${PWD}:/DATA -w /DATA -i pinellolab/crispresso2 CRISPResso --fastq_r1 Rep1_R1_001.fastq --fastq_r2 Rep1_R2_001.fastq --amplicon_seq NNNNNNNNNNNNNNNNNNNN --guide_seq NNNNNNNNNNNNNNNNNNNN -n nhej
```

Prime editing (insertion or deletion): 
```
docker run -v ${PWD}:/DATA -w /DATA -i pinellolab/crispresso2 CRISPResso --fastq_r1 Rep1_R1_001.fastq --fastq_r2 Rep1_R2_001.fastq --amplicon_seq NNNNNNNNNNNNNNNNNNNN --expected_hdr_amplicon_seq NNNNNNNNNNNNNNNNNNNN --guide_seq NNNNNNNNNNNNNNNNNNNN  --discard_indel_reads 
```

Prime editing (substitution): 
```
docker run -v ${PWD}:/DATA -w /DATA -i pinellolab/crispresso2 CRISPResso --fastq_r1 Rep1_R1_001.fastq --fastq_r2 Rep1_R2_001.fastq --amplicon_seq  NNNNNNNNNNNNNNNNNNNN --prime_editing_pegRNA_spacer_seq NNNNNNNNNNNNNNNNNNNN --prime_editing_pegRNA_extension_seq NNNNNNNNNNNNNNNNNNNN --prime_editing_nicking_guide_seq NNNNNNNNNNNNNNNNNNNN --prime_editing_pegRNA_scaffold_seq NNNNNNNNNNNNNNNNNNNN
```
