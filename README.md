# Andrew's 2021 Advanced Bioinformatics Course Notebook

## Day 02 22-Jan-2021

4. execute a pwd command and start a log of your commands with a header for today's date in your README.md github logfile in your workspace
```
[apear012@turing1 exercises]$ pwd
/cm/shared/courses/dbarshis/21AdvGenomics/sandboxes/apearson/data/exercises
```
5. cp the Exercise2.fasta.gz and Exercise2.fastq.tar.gz files into your exercises directory
```
[apear012@turing1 exercises]$ cp /cm/shared/courses/dbarshis/21AdvGenomics/assignments_exercises/day02/Exercise* .
[apear012@turing1 exercises]$ ls
Exercise2.fasta.gz  Exercise2.fastq.tar.gz
```
6. unzip and untar the files
```
[apear012@turing1 exercises]$ gunzip Exercise2.fasta.gz
[apear012@turing1 exercises]$ ls
Exercise2.fasta  Exercise2.fastq.tar.gz
```

If you wanted to gunzip without losing the original file, you would use:
```
$ gunzip -c Exercise2.fasta.gz > Exercise2.fasta
```

```
[apear012@turing1 exercises]$ tar -xzvf Exercise2.fastq.tar.gz 
Exercise2.fastq
[apear012@turing1 exercises]$ ls
Exercise2.fasta  Exercise2.fastq  Exercise2.fastq.tar.gz
```

8. calculate how many sequences are in each file and add these results to your notebook file
```
[apear012@turing1 exercises]$ grep -c '>' Exercise2.fasta
138
```

```
[apear012@turing1 exercises]$ wc -l Exercise2.fastq
245216 Exercise2.fastq
[apear012@turing1 exercises]$ echo 245216/4 | bc 
61304
```
9. cp the avg_cov_len_fasta_advbioinf.py from the /cm/shared/courses/dbarshis/21AdvGenomics/scripts directory into your class scripts directory
```
[apear012@turing1 scripts]$ cp /cm/shared/courses/dbarshis/21AdvGenomics/scripts/avg_cov_len_fasta_advbioinf.py .
[apear012@turing1 scripts]$ ls
avg_cov_len_fasta_advbioinf.py
```
10. start an interactive compute session and re-navigate to your exercises directory
```
wahab-01:~> salloc
salloc: Pending job allocation 133736
salloc: job 133736 queued and waiting for resources
salloc: job 133736 has been allocated resources
salloc: Granted job allocation 133736
This session will be terminated in 7 days. If your application requires
a longer excution time, please use command "salloc -t N-0" where N is the
number of days that you need.
```
11. run the avg_cov_len_fasta_DJB.py script on your Exercise2.fasta file by typing the path to the script followed by the Exercise2.fasta file name
```
 e2-w6420b-01:/cm/shared/courses/dbarshis/21AdvGenomics/sandboxes/apearson/data/exercises> ../../scripts//avg_cov_len_fasta_advbioinf.py Exercise2.fasta
The total number of sequences is 138
The average sequence length is 126640
The total number of bases is 17476447
The minimum sequence length is 1122
The maximum sequence length is 562680
The N50 is 187037
Median Length = 92612
contigs < 150bp = 0
contigs >= 500bp = 138
contigs >= 1000bp = 138
contigs >= 2000bp = 135
```

## Day 03 27-Jan-2021
Below is technically the day02 homework.

1. Write an sbatch script to cp the files /cm/shared/courses/dbarshis/21AdvGenomics/classdata/Astrangia_poculata/originalfastqs/ into your own data directory, Andrew-HADB01
```
[apear012@coreV2-25-072 data]$ pwd
/cm/shared/courses/dbarshis/21AdvGenomics/sandboxes/apearson/data
[apear012@coreV2-25-072 data]$ nano APCopyLane01.sh
[apear012@coreV2-25-072 data]$ ls
APCopyLane01.sh  exercises
[apear012@coreV2-25-072 data]$ cat APCopyLane01.sh 
#!/bin/bash -l

#SBATCH -o APCopyLane01.txt
#SBATCH -n 1
#SBATCH --mail-user=pearsoac@evms.edu
#SBATCH --mail-type=END
#SBATCH --job-name=APCopyLane01

cp /cm/shared/courses/dbarshis/21AdvGenomics/classdata/Astrangia_poculata/originalfastqs/HADB01* /cm/shared/courses/dbarshis/21AdvGenomics/sandboxes/apearson/data
```
2. Add the content of your sbatch script to your logfile
Did this above.

3. submit the slurm script (sbatch scripname.sh) and verify that it's working (by squeue -u yourusername multiple times and checking the destination directory to make sure the files are being created)
```
[apear012@coreV2-25-072 data]$ sbatch APCopyLane01.sh
Submitted batch job 9270452
[apear012@coreV2-25-072 data]$ squeue -u apear012
             JOBID PARTITION     NAME     USER ST       TIME  NODES NODELIST(REASON) 
           9270428      main       sh apear012  R      39:36      1 coreV2-25-072 
           9270452      main APCopyLa apear012  R       0:29      1 coreV2-25-072 
```

4. Make sure this is all documented on your github notebook
See above.

5. Write a sbatch script to gunzip all the fastq.gz files in your data directory

```
[apear012@turing1 data]$ pwd
/cm/shared/courses/dbarshis/21AdvGenomics/sandboxes/apearson/data
[apear012@turing1 data]$ cat APGunzipLane01Files.sh 
#!/bin/bash -l

#SBATCH -o APGunzipLane01Files.txt
#SBATCH -n 1
#SBATCH --mail-user=pearsoac@evms.edu
#SBATCH --mail-type=END
#SBATCH --job-name=APGunzipLane01Files

gunzip *.fastq.gz
[apear012@turing1 data]$ sbatch APGunzipLane01Files.sh 
Submitted batch job 9270467
```
**This is the day03 homework:**
1. cp the /cm/shared/courses/dbarshis/21AdvGenomics/assignments_exercises/day03 directory (and files) to your sandbox.

```
[apear012@turing1 apearson]$ pwd
/cm/shared/courses/dbarshis/21AdvGenomics/sandboxes/apearson
[apear012@turing1 apearson]$ cp -r /cm/shared/courses/dbarshis/21AdvGenomics/assignments_exercises/day03 .
[apear012@turing1 apearson]$ ls
AP_exercise1.txt  data  day03  groundrules.txt  scripts
```
2. mkdir a fastq directory in your data directory and mv all the .fastq files into this directory
```
[apear012@turing1 data]$ mkdir fastq
[apear012@turing1 data]$ mv ./*.fastq fastq
[apear012@turing1 data]$ cd fastq
[apear012@turing1 fastq]$ ls
HADB01-A_S17_L002_R1_001.fastq  HADB01-G_S23_L002_R1_001.fastq  HADB01-M_S29_L002_R1_001.fastq
HADB01-B_S18_L002_R1_001.fastq  HADB01-H_S24_L002_R1_001.fastq  HADB01-N_S30_L002_R1_001.fastq
HADB01-C_S19_L002_R1_001.fastq  HADB01-I_S25_L002_R1_001.fastq  HADB01-O_S31_L002_R1_001.fastq
HADB01-D_S20_L002_R1_001.fastq  HADB01-J_S26_L002_R1_001.fastq  HADB01-P_S32_L002_R1_001.fastq
HADB01-E_S21_L002_R1_001.fastq  HADB01-K_S27_L002_R1_001.fastq
HADB01-F_S22_L002_R1_001.fastq  HADB01-L_S28_L002_R1_001.fastq
```
3. cp the renamingtable_complete.txt from the day03 directory into your fastq directory and the /cm/shared/courses/dbarshis/21AdvGenomics/scripts/renamer_advbioinf.py script into your sandbox scripts folder and less the new script and check out the usage statement

```
[apear012@turing1 fastq]$ pwd
/cm/shared/courses/dbarshis/21AdvGenomics/sandboxes/apearson/data/fastq
[apear012@turing1 fastq]$ cp /cm/shared/courses/dbarshis/21AdvGenomics/assignments_exercises/day03/renamingtable_complete.txt .
[apear012@turing1 fastq]$ ls
HADB01-A_S17_L002_R1_001.fastq  HADB01-G_S23_L002_R1_001.fastq  HADB01-M_S29_L002_R1_001.fastq
HADB01-B_S18_L002_R1_001.fastq  HADB01-H_S24_L002_R1_001.fastq  HADB01-N_S30_L002_R1_001.fastq
HADB01-C_S19_L002_R1_001.fastq  HADB01-I_S25_L002_R1_001.fastq  HADB01-O_S31_L002_R1_001.fastq
HADB01-D_S20_L002_R1_001.fastq  HADB01-J_S26_L002_R1_001.fastq  HADB01-P_S32_L002_R1_001.fastq
HADB01-E_S21_L002_R1_001.fastq  HADB01-K_S27_L002_R1_001.fastq  renamingtable_complete.txt
HADB01-F_S22_L002_R1_001.fastq  HADB01-L_S28_L002_R1_001.fastq
```
```
[apear012@turing1 scripts]$ pwd
/cm/shared/courses/dbarshis/21AdvGenomics/sandboxes/apearson/scripts
[apear012@turing1 scripts]$ cp /cm/shared/courses/dbarshis/21AdvGenomics/scripts/renamer_advbioinf.py .
[apear012@turing1 scripts]$ ls
avg_cov_len_fasta_advbioinf.py  renamer_advbioinf.py
[apear012@turing1 scripts]$ less renamer_advbioinf.py 
```
renamer_advbioinf.py :
```
#!/usr/bin/env python
####usage renamer.py renamingtable
#### this script take the entries in the first column of table and renames (mv's) them to files with the names in the second column
import sys
import os

fin=open(sys.argv[1],'r')
linecount=0
for line in fin:
	linecount+=1
	if linecount>=2:
		cols=line.rstrip().split('\t')
		print 'mv %s %s' %(cols[0], cols[1])
#		os.popen('mv %s %s' %(cols[0], cols[1]))
```
4. run the renamer_advbioinf.py script in your fastq folder using the renamingtable_complete.txt as practice and verify the output to the screen by hand

```
[apear012@turing1 fastq]$ pwd
/cm/shared/courses/dbarshis/21AdvGenomics/sandboxes/apearson/data/fastq
[apear012@turing1 fastq]$ python ../../scripts/renamer_advbioinf.py renamingtable_complete.txt
mv HADB01-A_S17_L002_R1_001.fastq VA_W_01_14.fastq
mv HADB01-B_S18_L002_R1_001.fastq VA_B_01_14.fastq
mv HADB01-C_S19_L002_R1_001.fastq RI_W_01_14.fastq
mv HADB01-D_S20_L002_R1_001.fastq RI_B_01_14.fastq
mv HADB01-E_S21_L002_R1_001.fastq VA_W_01_22.fastq
mv HADB01-F_S22_L002_R1_001.fastq VA_B_01_22.fastq
mv HADB01-G_S23_L002_R1_001.fastq RI_W_01_22.fastq
mv HADB01-H_S24_L002_R1_001.fastq RI_B_01_22.fastq
mv HADB01-I_S25_L002_R1_001.fastq VA_W_01_18.fastq
mv HADB01-J_S26_L002_R1_001.fastq VA_B_01_18.fastq
mv HADB01-K_S27_L002_R1_001.fastq RI_W_01_18.fastq
mv HADB01-L_S28_L002_R1_001.fastq RI_B_01_18.fastq
mv HADB01-M_S29_L002_R1_001.fastq VA_W_08_SNP.fastq
mv HADB01-N_S30_L002_R1_001.fastq VA_B_09_SNP.fastq
mv HADB01-O_S31_L002_R1_001.fastq RI_W_08_SNP.fastq
mv HADB01-P_S32_L002_R1_001.fastq RI_B_08_SNP.fastq
mv HADB02-A_S33_L003_R1_001.fastq VA_W_02_14.fastq
mv HADB02-B_S34_L003_R1_001.fastq VA_B_02_14.fastq
mv HADB02-C_S35_L003_R1_001.fastq RI_W_02_14.fastq
mv HADB02-D_S36_L003_R1_001.fastq RI_B_02_14.fastq
mv HADB02-E_S37_L003_R1_001.fastq VA_W_02_22.fastq
mv HADB02-F_S38_L003_R1_001.fastq VA_B_02_22.fastq
mv HADB02-G_S39_L003_R1_001.fastq RI_W_02_22.fastq
mv HADB02-H_S40_L003_R1_001.fastq RI_B_02_22.fastq
mv HADB02-I_S41_L003_R1_001.fastq VA_W_02_18.fastq
mv HADB02-J_S42_L003_R1_001.fastq VA_B_02_18.fastq
mv HADB02-K_S43_L003_R1_001.fastq RI_W_02_18.fastq
mv HADB02-L_S44_L003_R1_001.fastq RI_B_02_18.fastq
mv HADB02-M_S45_L003_R1_001.fastq VA_W_09_SNP.fastq
mv HADB02-N_S46_L003_R1_001.fastq VA_B_08_SNP.fastq
mv HADB02-O_S47_L003_R1_001.fastq RI_W_09_SNP.fastq
mv HADB02-P_S48_L003_R1_001.fastq RI_B_09_SNP.fastq
mv HADB03-A_S49_L004_R1_001.fastq VA_W_03_14.fastq
mv HADB03-B_S50_L004_R1_001.fastq VA_B_03_14.fastq
mv HADB03-C_S51_L004_R1_001.fastq RI_W_03_14.fastq
mv HADB03-D_S52_L004_R1_001.fastq RI_B_03_14.fastq
mv HADB03-E_S53_L004_R1_001.fastq VA_W_03_22.fastq
mv HADB03-F_S54_L004_R1_001.fastq VA_B_03_22.fastq
mv HADB03-G_S55_L004_R1_001.fastq RI_W_03_22.fastq
mv HADB03-H_S56_L004_R1_001.fastq RI_B_03_22.fastq
mv HADB03-I_S57_L004_R1_001.fastq VA_W_03_18.fastq
mv HADB03-J_S58_L004_R1_001.fastq VA_B_03_18.fastq
mv HADB03-K_S59_L004_R1_001.fastq RI_W_03_18.fastq
mv HADB03-L_S60_L004_R1_001.fastq RI_B_03_18.fastq
mv HADB03-M_S61_L004_R1_001.fastq VA_W_10_SNP.fastq
mv HADB03-N_S62_L004_R1_001.fastq VA_B_10_SNP.fastq
mv HADB03-O_S63_L004_R1_001.fastq RI_W_10_SNP.fastq
mv HADB03-P_S64_L004_R1_001.fastq RI_B_10_SNP.fastq
mv HADB04-A_S65_L005_R1_001.fastq VA_W_04_14.fastq
mv HADB04-B_S66_L005_R1_001.fastq VA_B_04_14.fastq
mv HADB04-C_S67_L005_R1_001.fastq RI_W_04_14.fastq
mv HADB04-D_S68_L005_R1_001.fastq RI_B_04_14.fastq
mv HADB04-E_S69_L005_R1_001.fastq VA_W_04_22.fastq
mv HADB04-F_S70_L005_R1_001.fastq VA_B_04_22.fastq
mv HADB04-G_S71_L005_R1_001.fastq RI_W_04_22.fastq
mv HADB04-H_S72_L005_R1_001.fastq RI_B_04_22.fastq
mv HADB04-I_S73_L005_R1_001.fastq VA_W_04_18.fastq
mv HADB04-J_S74_L005_R1_001.fastq VA_B_04_18.fastq
mv HADB04-K_S75_L005_R1_001.fastq RI_W_04_18.fastq
mv HADB04-L_S76_L005_R1_001.fastq RI_B_04_18.fastq
mv HADB04-M_S77_L005_R1_001.fastq VA_W_05_14.fastq
mv HADB04-N_S78_L005_R1_001.fastq VA_B_05_14.fastq
mv HADB04-O_S79_L005_R1_001.fastq RI_W_05_14.fastq
mv HADB04-P_S80_L005_R1_001.fastq RI_B_05_14.fastq
mv HADB05-A_S81_L006_R1_001.fastq VA_W_05_22.fastq
mv HADB05-B_S82_L006_R1_001.fastq VA_B_05_22.fastq
mv HADB05-C_S83_L006_R1_001.fastq RI_W_05_22.fastq
mv HADB05-D_S84_L006_R1_001.fastq RI_B_05_22.fastq
mv HADB05-E_S85_L006_R1_001.fastq VA_W_05_18.fastq
mv HADB05-F_S86_L006_R1_001.fastq VA_B_05_18.fastq
mv HADB05-G_S87_L006_R1_001.fastq RI_W_05_18.fastq
mv HADB05-H_S88_L006_R1_001.fastq RI_B_05_18.fastq
mv HADB05-I_S89_L006_R1_001.fastq VA_W_06_14.fastq
mv HADB05-J_S90_L006_R1_001.fastq VA_B_06_14.fastq
mv HADB05-K_S91_L006_R1_001.fastq RI_W_06_14.fastq
mv HADB05-L_S92_L006_R1_001.fastq RI_B_06_14.fastq
mv HADB05-M_S93_L006_R1_001.fastq VA_W_06_22.fastq
mv HADB05-N_S94_L006_R1_001.fastq VA_B_06_22.fastq
mv HADB05-O_S95_L006_R1_001.fastq RI_W_06_22.fastq
mv HADB05-P_S96_L006_R1_001.fastq RI_B_06_22.fastq
mv HADB06-A_S97_L007_R1_001.fastq VA_W_06_18.fastq
mv HADB06-B_S98_L007_R1_001.fastq VA_B_06_18.fastq
mv HADB06-C_S99_L007_R1_001.fastq RI_W_06_18.fastq
mv HADB06-D_S100_L007_R1_001.fastq RI_B_06_18.fastq
mv HADB06-E_S101_L007_R1_001.fastq VA_W_07_14.fastq
mv HADB06-F_S102_L007_R1_001.fastq VA_B_07_14.fastq
mv HADB06-G_S103_L007_R1_001.fastq RI_W_07_14.fastq
mv HADB06-H_S104_L007_R1_001.fastq RI_B_07_14.fastq
mv HADB06-I_S105_L007_R1_001.fastq VA_W_07_22.fastq
mv HADB06-J_S106_L007_R1_001.fastq VA_B_07_22.fastq
mv HADB06-K_S107_L007_R1_001.fastq RI_W_07_22.fastq
mv HADB06-L_S108_L007_R1_001.fastq RI_B_07_22.fastq
mv HADB06-M_S109_L007_R1_001.fastq VA_W_07_18.fastq
mv HADB06-N_S110_L007_R1_001.fastq VA_B_07_18.fastq
mv HADB06-O_S111_L007_R1_001.fastq RI_W_07_18.fastq
mv HADB06-P_S112_L007_R1_001.fastq RI_B_07_18.fastq
```
5. Uncomment the last line of the renaming script in your scripts folder that starts with os.popen and comment out the next to last line that starts with print.
```
[apear012@turing1 scripts]$ pwd
/cm/shared/courses/dbarshis/21AdvGenomics/sandboxes/apearson/scripts
[apear012@turing1 scripts]$ cat renamer_advbioinf.py 
#!/usr/bin/env python
####usage renamer.py renamingtable
#### this script take the entries in the first column of table and renames (mv's) them to files with the names in the second column
import sys
import os

fin=open(sys.argv[1],'r')
linecount=0
for line in fin:
	linecount+=1
	if linecount>=2:
		cols=line.rstrip().split('\t')
		print 'mv %s %s' %(cols[0], cols[1])
#		os.popen('mv %s %s' %(cols[0], cols[1]))
[apear012@turing1 scripts]$ nano renamer_advbioinf.py 
[apear012@turing1 scripts]$ cat renamer_advbioinf.py
#!/usr/bin/env python
####usage renamer.py renamingtable
#### this script take the entries in the first column of table and renames (mv's) them to files with the names in the second column
import sys
import os

fin=open(sys.argv[1],'r')
linecount=0
for line in fin:
	linecount+=1
	if linecount>=2:
		cols=line.rstrip().split('\t')
#		print 'mv %s %s' %(cols[0], cols[1])
		os.popen('mv %s %s' %(cols[0], cols[1]))
```

6. write a sbatch script and submit it to rename all the .fastq files according to the renaming table using your renamer_advbioinf.py script

```
[apear012@turing1 fastq]$ pwd
/cm/shared/courses/dbarshis/21AdvGenomics/sandboxes/apearson/data/fastq
[apear012@turing1 fastq]$ nano APRenameLane01Files.sh
```
APRenameLane01Files.sh:
```
#!/bin/bash -l

#SBATCH -o APRenameLane01Files.txt
#SBATCH -n 1
#SBATCH --mail-user=pearsoac@evms.edu
#SBATCH --mail-type=END
#SBATCH --job-name=APRenameLane01Files

../../scripts/renamer_advbioinf.py renamingtable_complete.txt ./*.fastq*
```
```
[apear012@turing1 fastq]$ sbatch APRenameLane01Files.sh 
Submitted batch job 9270537
[apear012@turing1 fastq]$ ls
APRenameLane01Files.sh      RI_B_01_18.fastq   RI_W_01_18.fastq   VA_B_01_18.fastq   VA_W_01_18.fastq
APRenameLane01Files.txt     RI_B_01_22.fastq   RI_W_01_22.fastq   VA_B_01_22.fastq   VA_W_01_22.fastq
renamingtable_complete.txt  RI_B_08_SNP.fastq  RI_W_08_SNP.fastq  VA_B_09_SNP.fastq  VA_W_08_SNP.fastq
RI_B_01_14.fastq            RI_W_01_14.fastq   VA_B_01_14.fastq   VA_W_01_14.fastq
```
7. Make sure this is all documented on your github page
see above

8. The naming convention for the files is as follows:
  * SOURCEPOPULATION_SYMBIOTICSTATE_GENOTYPE_TEMPERATURE.fastq
  * There are 2 sources: Virginia and Rhode Island
  * There are 2 symbiotic states: Brown and White
  
9. Next, you're going to start the process of adapter clipping and quality trimming all the renamed .fastq files in batches, by lane.

10. cp the script /cm/shared/courses/dbarshis/21AdvGenomics/scripts/Trimclipfilterstatsbatch_advbioinf.py into your scripts directory.
```
[apear012@turing1 scripts]$ pwd
/cm/shared/courses/dbarshis/21AdvGenomics/sandboxes/apearson/scripts

[apear012@turing1 scripts]$ cp /cm/shared/courses/dbarshis/21AdvGenomics/scripts/Trimclipfilterstatsbatch_advbioinf.py .
[apear012@turing1 scripts]$ ls
avg_cov_len_fasta_advbioinf.py  renamer_advbioinf.py  Trimclipfilterstatsbatch_advbioinf.py
```

11. Less/head the new script and check out the usage statement

```
[apear012@turing1 scripts]$ pwd
/cm/shared/courses/dbarshis/21AdvGenomics/sandboxes/apearson/scripts
[apear012@turing1 scripts]$ head Trimclipfilterstatsbatch_advbioinf.py 
#!/usr/bin/env python
# Written by Dan Barshis

import sys, os

########### Usage #############
# Trimclipfilterstatsbatch.py barcodefile.txt anynumberoffastqfiles
# This should be run from within the folder with all of your original .fastqstrim
# Will quality trim multiple SINGLE-END fastq files
# Things to customize for your particular platform:
```

12. cp the /cm/shared/courses/dbarshis/21AdvGenomics/assignments_exercises/day03/adapterlist_advbioinf.txt into the working directory with your fastq files.

```
[apear012@turing1 fastq]$ pwd
/cm/shared/courses/dbarshis/21AdvGenomics/sandboxes/apearson/data/fastq
[apear012@turing1 fastq]$ cp /cm/shared/courses/dbarshis/21AdvGenomics/assignments_exercises/day03/adapterlist_advbioinf.txt .
[apear012@turing1 fastq]$ ls
adapterlist_advbioinf.txt   RI_B_01_14.fastq   RI_W_01_14.fastq   VA_B_01_14.fastq   VA_W_01_14.fastq
APRenameLane01Files.sh      RI_B_01_18.fastq   RI_W_01_18.fastq   VA_B_01_18.fastq   VA_W_01_18.fastq
APRenameLane01Files.txt     RI_B_01_22.fastq   RI_W_01_22.fastq   VA_B_01_22.fastq   VA_W_01_22.fastq
renamingtable_complete.txt  RI_B_08_SNP.fastq  RI_W_08_SNP.fastq  VA_B_09_SNP.fastq  VA_W_08_SNP.fastq
```
13. Make a sbatch script for the Trimclipfilter... script and run it on your fastq files

```
[apear012@turing1 fastq]$ nano APTrimLane01Files.sh
[apear012@turing1 fastq]$ cat APTrimLane01Files.sh 
#!/bin/bash -l

#SBATCH -o APTrimLane01Files.txt
#SBATCH -n 1
#SBATCH --mail-user=pearsoac@evms.edu
#SBATCH --mail-type=END
#SBATCH --job-name=APTrimLane01Files

../../scripts/Trimclipfilterstatsbatch_advbioinf.py adapterlist_advbioinf.txt ./*.fastq*
[apear012@turing1 fastq]$ sbatch APTrimLane01Files.sh 
Submitted batch job 9270540
```
Email received immediately saying my job had failed.

```
[apear012@turing1 fastq]$ pwd
/cm/shared/courses/dbarshis/21AdvGenomics/sandboxes/apearson/data/fastq
[apear012@turing1 fastq]$ nano APTrimLane01Files.sh 
[apear012@turing1 fastq]$ cat APTrimLane01Files.sh
#!/bin/bash -l

#SBATCH -o APTrimLane01Files.txt
#SBATCH -n 1
#SBATCH --mail-user=pearsoac@evms.edu
#SBATCH --mail-type=END
#SBATCH --job-name=APTrimLane01Files

../../scripts/Trimclipfilterstatsbatch_advbioinf.py adapterlist_advbioinf.txt *.fastq
```

```
[apear012@turing1 fastq]$ sbatch APTrimLane01Files.sh
Submitted batch job 9270839
[apear012@turing1 fastq]$ squeue -u apear012
             JOBID PARTITION     NAME     USER ST       TIME  NODES NODELIST(REASON) 
           9270839      main APTrimLa apear012  R       0:00      1 coreV1-22-016 
```

14. This will take a while (like days)
15. Now might be a good time to update everything on your github

## Day 04 29-Jan-2021

1. Add your trimclipstats.txt output to the full class datafile /cm/shared/courses/dbarshis/21AdvGenomics/classdata/Astrangia_poculata/Fulltrimclipstatstable.txt using the following steps
	
1a. Run /cm/shared/courses/dbarshis/21AdvGenomics/scripts/Schafran_trimstatstable_advbioinf_clippedtrimmed.py -h to examine usage
```
[apear012@coreV2-25-072 filteringstats]$ pwd
/cm/shared/courses/dbarshis/21AdvGenomics/sandboxes/apearson/data/fastq/filteringstats
[apear012@turing1 filteringstats]$ python /cm/shared/courses/dbarshis/21AdvGenomics/scripts/Schafran_trimstatstable_advbioinf_clippedtrimmed.py -h
Written by Peter Schafran pscha005@odu.edu 5-Oct-2015

This script takes a stats output file from fastx_clipper and converts it into a table.

Usage: Schafran_trimstatstable.py [-c, -v, -h] inputfile.txt outputfile.txt

Options (-c and -v must be listed separately to run together):
-h	Display this help message
-c	Use comma delimiter instead of tabs
-v	Verbose mode (print steps to stdout)
```
1b. Run the script on your data with the outputfilename YOURNAME_trimclipstatsout.txt

```
[apear012@coreV2-25-072 filteringstats]$ python /cm/shared/courses/dbarshis/21AdvGenomics/scripts/Schafran_trimstatstable_advbioinf_clippedtrimmed.py trimclipstats.txt ANDREW_trimclipstatsout.txt
```

1c. Add YOURNAME_trimclipstatsout.txt to the class file by running tail -n +2 YOURNAME_trimclipstatsout.txt >> /cm/shared/courses/dbarshis/21AdvGenomics/classdata/Astrangia_poculata/Fulltrimclipstatstable.txt

```
[apear012@turing1 filteringstats]$ tail -n +2 ANDREW_trimclipstatsout.txt >> /cm/shared/courses/dbarshis/21AdvGenomics/classdata/Astrangia_poculata/Fulltrimclipstatstable.txt
```


2. Now we're going to map our reads back to our assembly using the bowtie2 alignment algorithm (starting to follow this pipeline https://github.com/bethsheets/SNPcalling_tutorial)

3. write a sbatch script to do the following commands in sequence on your _clippedtrimmedfilterd.fastq datafiles from your lane of data

```
module load bowtie2/2.2.4
for i in *_clippedtrimmed.fastq; do bowtie2 --rg-id ${i%_clippedtrimmed.fastq} \
--rg SM:${i%_clippedtrimmed.fastq} \
--very-sensitive -x /cm/shared/courses/dbarshis/21AdvGenomics/classdata/Astrangia_poculata/refassembly/Apoc_hostsym -U $i \
> ${i%_clippedtrimmedfilterd.fastq}.sam --no-unal -k 5; done
```
```
apear012@turing1:/cm/shared/courses/dbarshis/21AdvGenomics/sandboxes/apearson/data/fastq/QCFastqs$ pwd
/cm/shared/courses/dbarshis/21AdvGenomics/sandboxes/apearson/data/fastq/QCFastqs
apear012@turing1:/cm/shared/courses/dbarshis/21AdvGenomics/sandboxes/apearson/data/fastq/QCFastqs$ nano APbowtie.sh
```
APbowtie.sh:
```
#!/bin/bash -l

#SBATCH -o APbowtie.txt
#SBATCH -n 1
#SBATCH --mail-user=pearsoac@evms.edu
#SBATCH --mail-type=END
#SBATCH --job-name=APbowtie

module load bowtie2/2.2.4
for i in *_clippedtrimmed.fastq; do bowtie2 --rg-id ${i%_clippedtrimmed.fastq} \
--rg SM:${i%_clippedtrimmed.fastq} \
--very-sensitive -x /cm/shared/courses/dbarshis/21AdvGenomics/classdata/Astrangia_poculata/refassembly/Apoc_hostsym -U $i \
> ${i%_clippedtrimmedfilterd.fastq}.sam --no-unal -k 5; done
```

```
apear012@turing1:/cm/shared/courses/dbarshis/21AdvGenomics/sandboxes/apearson/data/fastq/QCFastqs$ sbatch APbowtie.sh 
Submitted batch job 9271109
apear012@turing1:/cm/shared/courses/dbarshis/21AdvGenomics/sandboxes/apearson/data/fastq/QCFastqs$ squeue -u apear012
             JOBID PARTITION     NAME     USER ST       TIME  NODES NODELIST(REASON) 
           9271094      main       sh apear012  R      54:07      1 coreV2-25-072 
           9271109      main APbowtie apear012  R       0:07      1 coreV2-25-007 
```

4. Submit and add everything to your logfile.

See above.

## Day 05 03-Feb-2021

1. Team up with a partner for this one and work only on a combined set of data for your two lanes of sequences

Partner: Areej 
Lanes: 01, 06, and 07

2. Run the Trinity denovo assembler on your clippedtrimmed.fastq files for your two lanes together

3. Modify the below sbatch script (note the differences in the header compared to the previous one)

original script:
```
#!/bin/bash -l

#SBATCH -o OUTFILE.txt
#SBATCH -n 32
#SBATCH -p himem
#SBATCH --mail-user=YOUREMAIL@odu.edu
#SBATCH --mail-type=END
#SBATCH --job-name=YOURJOBNAME

enable_lmod
module load container_env trinity

crun Trinity --seqType fq --max_memory 768G --normalize_reads --single ALLSINGLEENDREADSSEPARATEDBYCOMMAS --CPU 32
```
Edited script (renamed APAMAssemble.sh in /cm/shared/courses/dbarshis/21AdvGenomics/sandboxes/apearson/data/fastq/QCFastqs/apam/)
```
#!/bin/bash -l

#SBATCH -o APAMAssemble.txt
#SBATCH -n 32
#SBATCH -p himem
#SBATCH --mail-user=pearsoac@evms.edu
#SBATCH --mail-type=END
#SBATCH --job-name=APAMAssemble

enable_lmod
module load container_env trinity

crun Trinity --seqType fq --max_memory 768G --normalize_reads --single RI_B_01_14_clippedtrimmed.fastq,RI_W_06_18_clippedtrimmed.fastq,VA_B_07_22_clippedtrimmed.fastq,RI_B_01_18_clippedtrimmed.fastq,RI_W_07_14_clippedtrimmed.fastq,VA_B_09_SNP_clippedtrimmed.fastq,RI_B_01_22_clippedtrimmed.fastq,RI_W_07_18_clippedtrimmed.fastq,VA_W_01_14_clippedtrimmed.fastq,RI_B_06_18_clippedtrimmed.fastq,RI_W_07_22_clippedtrimmed.fastq,VA_W_01_18_clippedtrimmed.fastq,RI_B_07_14_clippedtrimmed.fastq,RI_W_08_SNP_clippedtrimmed.fastq,VA_W_01_22_clippedtrimmed.fastq,RI_B_07_18_clippedtrimmed.fastq,VA_B_01_14_clippedtrimmed.fastq,VA_W_06_18_clippedtrimmed.fastq,RI_B_07_22_clippedtrimmed.fastq,VA_B_01_18_clippedtrimmed.fastq,VA_W_07_14_clippedtrimmed.fastq,RI_B_08_SNP_clippedtrimmed.fastq,VA_B_01_22_clippedtrimmed.fastq,VA_W_07_18_clippedtrimmed.fastq,RI_W_01_14_clippedtrimmed.fastq,VA_B_06_18_clippedtrimmed.fastq,VA_W_07_22_clippedtrimmed.fastq,RI_W_01_18_clippedtrimmed.fastq,VA_B_07_14_clippedtrimmed.fastq,VA_W_08_SNP_clippedtrimmed.fastq,RI_W_01_22_clippedtrimmed.fastq,VA_B_07_18_clippedtrimmed.fastq --CPU 32
```

4. Check https://trinityrnaseq.github.io/ for usage info

5. Submit your trinity script

```
[apear012@turing1 apam]$ pwd
/cm/shared/courses/dbarshis/21AdvGenomics/sandboxes/apearson/data/fastq/QCFastqs/apam
[apear012@coreV2-22-007 apam]$ sbatch APAMAssemble.sh 
Submitted batch job 9272358
[apear012@coreV2-22-007 apam]$ squeue -u apear012
             JOBID PARTITION     NAME     USER ST       TIME  NODES NODELIST(REASON) 
           9272358     himem APAMAsse apear012 PD       0:00      1 (Resources) 
           9272334      main       sh apear012  R    1:19:02      1 coreV2-25-002 
           9272357      main       sh apear012  R       6:01      1 coreV2-22-007 
```
Job failed after ~15min.

edited APAMAssemble.sh (removed --normalize_reads):
```
#!/bin/bash -l

#SBATCH -o APAMAssemble.txt
#SBATCH -n 32
#SBATCH -p himem
#SBATCH --mail-user=pearsoac@evms.edu
#SBATCH --mail-type=END
#SBATCH --job-name=APAMAssemble

enable_lmod
module load container_env trinity

crun Trinity --seqType fq --max_memory 768G --single RI_B_01_14_clippedtrimmed.fastq,RI_W_06_18_clippedtrimmed.fastq,VA_B_07_22_clippedtrimmed.fastq,RI_B_01_18_clippedtrimmed.fastq,RI_W_07_14_clippedtrimmed.fastq,VA_B_09_SNP_clippedtrimmed.fastq,RI_B_01_22_clippedtrimmed.fastq,RI_W_07_18_clippedtrimmed.fastq,VA_W_01_14_clippedtrimmed.fastq,RI_B_06_18_clippedtrimmed.fastq,RI_W_07_22_clippedtrimmed.fastq,VA_W_01_18_clippedtrimmed.fastq,RI_B_07_14_clippedtrimmed.fastq,RI_W_08_SNP_clippedtrimmed.fastq,VA_W_01_22_clippedtrimmed.fastq,RI_B_07_18_clippedtrimmed.fastq,VA_B_01_14_clippedtrimmed.fastq,VA_W_06_18_clippedtrimmed.fastq,RI_B_07_22_clippedtrimmed.fastq,VA_B_01_18_clippedtrimmed.fastq,VA_W_07_14_clippedtrimmed.fastq,RI_B_08_SNP_clippedtrimmed.fastq,VA_B_01_22_clippedtrimmed.fastq,VA_W_07_18_clippedtrimmed.fastq,RI_W_01_14_clippedtrimmed.fastq,VA_B_06_18_clippedtrimmed.fastq,VA_W_07_22_clippedtrimmed.fastq,RI_W_01_18_clippedtrimmed.fastq,VA_B_07_14_clippedtrimmed.fastq,VA_W_08_SNP_clippedtrimmed.fastq,RI_W_01_22_clippedtrimmed.fastq,VA_B_07_18_clippedtrimmed.fastq --CPU 32
```
```
[apear012@turing1 apam]$ sbatch APAMAssemble.sh
Submitted batch job 9272385
[apear012@turing1 apam]$ squeue -u apear012
             JOBID PARTITION     NAME     USER ST       TIME  NODES NODELIST(REASON) 
           9272357      main       sh apear012  R    1:15:39      1 coreV2-22-007 
           9272385     himem APAMAsse apear012  R       0:14      1 coreV4-21-himem-003 
```

## Day 06 05-Feb-2021

1. start an interactive session via salloc and run the /cm/shared/apps/trinity/2.0.6/util/TrinityStats.pl script on your Trinity.fasta output from your assembly

```
[apear012@turing1 apam]$ salloc
salloc: Pending job allocation 9272856
salloc: job 9272856 queued and waiting for resources
salloc: job 9272856 has been allocated resources
salloc: Granted job allocation 9272856
```

```
[apear012@coreV2-22-028 djbtestassembly]$ pwd
/cm/shared/courses/dbarshis/21AdvGenomics/sandboxes/apearson/data/fastq/QCFastqs/apam/djbtestassembly
[apear012@coreV2-22-028 djbtestassembly]$ /cm/shared/apps/trinity/2.0.6/util/TrinityStats.pl Trinity.fasta 


################################
## Counts of transcripts, etc.
################################
Total trinity 'genes':	20980
Total trinity transcripts:	21992
Percent GC: 46.21

########################################
Stats based on ALL transcript contigs:
########################################

	Contig N10: 1178
	Contig N20: 694
	Contig N30: 514
	Contig N40: 414
	Contig N50: 347

	Median contig length: 273
	Average contig: 356.95
	Total assembled bases: 7850006


#####################################################
## Stats based on ONLY LONGEST ISOFORM per 'GENE':
#####################################################

	Contig N10: 1027
	Contig N20: 643
	Contig N30: 486
	Contig N40: 397
	Contig N50: 336

	Median contig length: 271
	Average contig: 347.72
	Total assembled bases: 7295061

```
2. compare this with the output from avg_cov_len_fasta_advbioinf.py on our class reference assembly (/cm/shared/courses/dbarshis/21AdvGenomics/classdata/Astrangia_poculata/refassembly/15079_Apoc_hostsym.fasta) and add both to your logfile
```
[apear012@coreV2-22-028 scripts]$ pwd
/cm/shared/courses/dbarshis/21AdvGenomics/sandboxes/apearson/scripts
[apear012@coreV2-22-028 scripts]$ python avg_cov_len_fasta_advbioinf.py /cm/shared/courses/dbarshis/21AdvGenomics/classdata/Astrangia_poculata/refassembly/15079_Apoc_hostsym.fasta
The total number of sequences is 15079
The average sequence length is 876
The total number of bases is 13210470
The minimum sequence length is 500
The maximum sequence length is 10795
The N50 is 881
Median Length = 578
contigs < 150bp = 0
contigs >= 500bp = 15079
contigs >= 1000bp = 3660
contigs >= 2000bp = 536
[apear012@coreV2-22-028 scripts]$ pwd
/cm/shared/courses/dbarshis/21AdvGenomics/sandboxes/apearson/scripts
```
```
[apear012@coreV2-22-028 scripts]$ python avg_cov_len_fasta_advbioinf.py /cm/shared/courses/dbarshis/21AdvGenomics/sandboxes/apearson/data/fastq/QCFastqs/apam/djbtestassembly/Trinity.fasta 
The total number of sequences is 21992
The average sequence length is 356
The total number of bases is 7850006
The minimum sequence length is 192
The maximum sequence length is 10795
The N50 is 347
Median Length = 355
contigs < 150bp = 0
contigs >= 500bp = 2862
contigs >= 1000bp = 607
contigs >= 2000bp = 91
```
3. less or head your bowtie2 job output file to look at your alignment statistics and calculate the following from the information:
	a-the mean percent "overall alignment rate"
```
[apear012@turing1 QCFastqs]$ pwd
/cm/shared/courses/dbarshis/21AdvGenomics/sandboxes/apearson/data/fastq/QCFastqs
[apear012@turing1 QCFastqs]$ grep 'overall alignment rate' APbowtie.txt | cut -d '%' -f 1
3.22
1.74
1.41
1.65
2.01
1.86
1.34
1.49
2.68
7.09
1.84
1.83
1.75
1.70
52.97
1.47
```
	b-the mean percent reads "aligned exactly 1 time"
```
[apear012@turing1 QCFastqs]$ grep 'aligned exactly 1 time' APbowtie.txt | cut -d '%' -f 1 | cut -d '(' -f 2
1.63
1.18
1.00
1.18
0.67
1.21
0.88
0.94
1.71
5.19
1.29
1.23
1.09
1.18
0.55
1.03
```
	c-the mean number of reads "aligned exactly 1 time"
```
[apear012@turing1 QCFastqs]$ grep 'aligned exactly 1 time' APbowtie.txt | cut -d '%' -f 1 | cut -d ' ' -f 5
117712
281939
240500
256601
40180
298308
182262
381640
354945
1169727
374006
332280
168092
330623
397
276577
```
	d-the mean percent reads "aligned >1 times"
```
[apear012@turing1 QCFastqs]$ grep 'aligned >1 time' APbowtie.txt | cut -d '%' -f 1 | cut -d '(' -f 2
1.59
0.56
0.41
0.47
1.34
0.65
0.45
0.55
0.97
1.91
0.55
0.60
0.66
0.51
52.42
0.44
```
	
	hint use grep and paste into excel
	
Copied each of these outputs into excel and averaged. This was used for the next step to make the alignstatsAP.txt


4. add your statistics as single rows to the shared table /cm/shared/courses/dbarshis/21AdvGenomics/classdata/Astrangia_poculata/alignmentstatstable.txt as tab-delimited text in the following order:
LaneX_yourinitials	b-the mean percent "overall alignment rate"	c-the mean percent reads "aligned exactly 1 time"	d-the mean number of reads "aligned exactly 1 time"	e-the mean percent reads "aligned >1 times"
```
[apear012@turing1 QCFastqs]$ pwd
/cm/shared/courses/dbarshis/21AdvGenomics/sandboxes/apearson/data/fastq/QCFastqs
[apear012@turing1 QCFastqs]$ nano alignstatsAP.txt
[apear012@turing1 QCFastqs]$ cat alignstatsAP.txt 
Lane1AP	5.378125	1.3725	300361.8125	4.005
[apear012@turing1 QCFastqs]$ cat alignstatsAP.txt >> /cm/shared/courses/dbarshis/21AdvGenomics/classdata/Astrangia_poculata/alignmentstatstable.txt
[apear012@turing1 QCFastqs]$ tail /cm/shared/courses/dbarshis/21AdvGenomics/classdata/Astrangia_poculata/alignmentstatstable.txt
LaneX	overallalignmentrate	percsinglyaligned	numsinglyaligned	percmultiplyaligned
LaneX_djb	2.495714286	1.251428571	247656.7143	1.247142857
LaneX_djb	2.495714286	1.251428571	247656.7143	1.247142857
Lane1AP	5.378125	1.3725	300361.8125	4.005
```

5. Data cleanup and archiving:

a. mv your Trinity.fasta file from your trinity_out_dir to a folder called testassembly in your data directory
```
[apear012@turing1 trinity_out_dir]$ pwd
/cm/shared/courses/dbarshis/21AdvGenomics/sandboxes/apearson/data/fastq/QCFastqs/apam/trinity_out_dir
[apear012@turing1 trinity_out_dir]$ mkdir ../../../../testassembly
[apear012@turing1 trinity_out_dir]$ mv Trinity.fasta ../../../../testassembly/
```
b. set up a sbatch script to:
		rm -r YOURtrinity_out_dir
		rm -r YOURoriginalfastqs
		rm -r YOURfilteringstats # as long as you've already appended your filteringstats output to the class table as part of homework_day04.txt

```
[apear012@turing1 fastq]$ pwd
/cm/shared/courses/dbarshis/21AdvGenomics/sandboxes/apearson/data/fastq
[apear012@turing1 fastq]$ nano AP_Cleanup.sh
```

AP_Cleanup.sh:
```
#!/bin/bash -l

#SBATCH -o AP_Cleanup.txt
#SBATCH -n 1
#SBATCH --mail-user=acpearson@evms.edu
#SBATCH --mail-type=END
#SBATCH --job-name=AP_Cleanup

rm -r ./QCFastqs/apam/trinity_out_dir
rm -r filteringstats
rm -r originalfastqs
```
```
[apear012@turing1 fastq]$ sbatch AP_Cleanup.sh 
Submitted batch job 9273047
[apear012@turing1 fastq]$ squeue -u apear012
             JOBID PARTITION     NAME     USER ST       TIME  NODES NODELIST(REASON) 
           9273047      main AP_Clean apear012  R       0:01      1 coreV1-22-003 
```
6. submit a blast against sprot from your testassembly folder using the following command
#!/bin/bash -l

#SBATCH -o OUTFILENAME.txt
#SBATCH -n 6         
#SBATCH --mail-user=EMAIL
#SBATCH --mail-type=END
#SBATCH --job-name=JOBNAME

enable_lmod
module load container_env blast
blastx -query Trinity.fasta -db /cm/shared/apps/blast/databases/uniprot_sprot_Sep2018 -out blastx.outfmt6 \
        -evalue 1e-20 -num_threads 6 -max_target_seqs 1 -outfmt 6
###Exploring our SAM files, check out http://bowtie-bio.sourceforge.net/bowtie2/manual.shtml#sam-output for bowtie2 specific output and http://bio-bwa.sourceforge.net/bwa.shtml#4 for general SAM output
```
[apear012@turing1 testassembly]$ pwd
/cm/shared/courses/dbarshis/21AdvGenomics/sandboxes/apearson/data/testassembly
[apear012@turing1 testassembly]$ nano AP_Blast.sh
```
AP_Blast.sh:
```
#!/bin/bash -l

#SBATCH -o AP_Blast.txt
#SBATCH -n 1
#SBATCH --mail-user=acpearson@evms.edu
#SBATCH --mail-type=END
#SBATCH --job-name=AP_Blast

enable_lmod
module load container_env blast
blastx -query Trinity.fasta -db /cm/shared/apps/blast/databases/uniprot_sprot_Sep2018 -out blastx.outfmt6 \
        -evalue 1e-20 -num_threads 6 -max_target_seqs 1 -outfmt 6
```
```
[apear012@turing1 testassembly]$ ls
AP_Blast.sh  Trinity.fasta
[apear012@turing1 testassembly]$ sbatch AP_Blast.sh 
Submitted batch job 9273048
[apear012@turing1 testassembly]$ squeue -u apear012
             JOBID PARTITION     NAME     USER ST       TIME  NODES NODELIST(REASON) 
           9273048      main AP_Blast apear012  R       0:02      1 coreV1-22-016 
```
7. head one of your .sam files to look at the header
```
[apear012@turing1 QCFastqs]$ pwd
/cm/shared/courses/dbarshis/21AdvGenomics/sandboxes/apearson/data/fastq/QCFastqs
[apear012@turing1 QCFastqs]$ head RI_B_01_14_clippedtrimmed.fastq.sam 
@HD	VN:1.0	SO:unsorted
@SQ	SN:TR78|c0_g1_i1_coral	LN:1109
@SQ	SN:TR78|c0_g2_i1_coral	LN:1109
@SQ	SN:TR79|c0_g1_i1_coral	LN:610
@SQ	SN:TR79|c0_g2_i1_coral	LN:1549
@SQ	SN:TR87|c0_g1_i1_coral	LN:732
@SQ	SN:TR93|c0_g1_i1_coral	LN:550
@SQ	SN:TR101|c0_g1_i1_coral	LN:673
@SQ	SN:TR104|c0_g1_i1_coral	LN:607
@SQ	SN:TR105|c0_g1_i1_coral	LN:587
```
8. grep -v '@' your.sam | head to look at the sequence read lines, why does this work to exclude the header lines?
```
[apear012@turing1 QCFastqs]$ grep -v '@' RI_B_01_14_clippedtrimmed.fastq.sam | head
K00188:59:HMTFHBBXX:2:1101:25814:1701	16	TR14006|c0_g2_i1_coral	317	255	51M	*	0	CAGCTGGAAATTCACGTGGTGGCAGTGGAAGTGGCTTTTGACAGAAATCTG	AJJJJJJJJJJJJFJJJJJJJJJJJJJJJJJJJJJJJJJJJJJJJFFFFAA	AS:i:0	XN:i:0	XM:i:0	XO:i:0	XG:i:0	NM:i:0	MD:Z:51	YT:Z:UU	RG:Z:RI_B_01_14
K00188:59:HMTFHBBXX:2:1101:19827:1912	0	TR6438|c0_g1_i3_coral	30	1	51M	*	0	TGAACATAGGCCGCTAACATCAAGGCATAAAAGTTTTGTGGCCGTTTTCGA	AAFFFJJJJJJJJJJJJJJJFJJJFJJJJJJJJJJJJJJJJJJJJFJJJJJ	AS:i:0	XS:i:0	XN:i:0	XM:i:0	XO:i:0	XG:i:0	NM:i:0	MD:Z:51	YT:Z:UU	RG:Z:RI_B_01_14
K00188:59:HMTFHBBXX:2:1101:19827:1912	256	TR6438|c0_g1_i1_coral	30	255	51M	*	0	TGAACATAGGCCGCTAACATCAAGGCATAAAAGTTTTGTGGCCGTTTTCGA	AAFFFJJJJJJJJJJJJJJJFJJJFJJJJJJJJJJJJJJJJJJJJFJJJJJ	AS:i:0	XS:i:0	XN:i:0	XM:i:0	XO:i:0	XG:i:0	NM:i:0	MD:Z:51	YT:Z:UU	RG:Z:RI_B_01_14
K00188:59:HMTFHBBXX:2:1101:19827:1912	256	TR6438|c0_g1_i4_coral	30	255	51M	*	0	TGAACATAGGCCGCTAACATCAAGGCATAAAAGTTTTGTGGCCGTTTTCGA	AAFFFJJJJJJJJJJJJJJJFJJJFJJJJJJJJJJJJJJJJJJJJFJJJJJ	AS:i:0	XS:i:0	XN:i:0	XM:i:0	XO:i:0	XG:i:0	NM:i:0	MD:Z:51	YT:Z:UU	RG:Z:RI_B_01_14
K00188:59:HMTFHBBXX:2:1101:23622:1912	16	TR43756|c0_g1_i1_coral	7449	1	51M	*	0	GGGGCCGAAGCCCCTGCAATTAAAATTGTTGACCACCTACATACCAAAGAC	JJJJJJJJJJJJFJJJJJJJJJJJFJFJJJJJJJJJJJJJJFJJJJFAAAA	AS:i:0	XS:i:0	XN:i:0	XM:i:0	XO:i:0	XG:i:0	NM:i:0	MD:Z:51	YT:Z:UU	RG:Z:RI_B_01_14
K00188:59:HMTFHBBXX:2:1101:23622:1912	272	TR43756|c0_g1_i1_coral	2063	255	51M	*	0	GGGGCCGAAGCCCCTGCAATTAAAATTGTTGACCACCTACATACCAAAGAC	JJJJJJJJJJJJFJJJJJJJJJJJFJFJJJJJJJJJJJJJJFJJJJFAAAA	AS:i:0	XS:i:0	XN:i:0	XM:i:0	XO:i:0	XG:i:0	NM:i:0	MD:Z:51	YT:Z:UU	RG:Z:RI_B_01_14
K00188:59:HMTFHBBXX:2:1101:23622:1912	272	TR43756|c0_g2_i1_coral	2077	255	51M	*	0	GGGGCCGAAGCCCCTGCAATTAAAATTGTTGACCACCTACATACCAAAGAC	JJJJJJJJJJJJFJJJJJJJJJJJFJFJJJJJJJJJJJJJJFJJJJFAAAA	AS:i:0	XS:i:0	XN:i:0	XM:i:0	XO:i:0	XG:i:0	NM:i:0	MD:Z:51	YT:Z:UU	RG:Z:RI_B_01_14
K00188:59:HMTFHBBXX:2:1101:20212:1947	0	TR11796|c0_g1_i1_sym	24	1	51M	*	0	TCCACCTTCCTGCGCATACCATCCATCCTACGCTTGCTGCTGAAAACGTTG	-AAFAFFFJA--FJJJ<FJ77AFJ7-<JAJFF7-F<A7<F-FJA<FFJJFF	AS:i:0	XS:i:0	XN:i:0	XM:i:0	XO:i:0	XG:i:0	NM:i:0	MD:Z:51	YT:Z:UU	RG:Z:RI_B_01_14
K00188:59:HMTFHBBXX:2:1101:20212:1947	256	TR11796|c0_g2_i1_sym	552	255	51M	*	0	TCCACCTTCCTGCGCATACCATCCATCCTACGCTTGCTGCTGAAAACGTTG	-AAFAFFFJA--FJJJ<FJ77AFJ7-<JAJFF7-F<A7<F-FJA<FFJJFF	AS:i:0	XS:i:0	XN:i:0	XM:i:0	XO:i:0	XG:i:0	NM:i:0	MD:Z:51	YT:Z:UU	RG:Z:RI_B_01_14
K00188:59:HMTFHBBXX:2:1101:23723:1947	0	TR43756|c0_g2_i1_coral	1579	1	51M	*	0	AACCATAACGAGCATCATCTTGATTAAGCTCATTAGGGTTAGCCTCGGTAC	AAFFFJJJJJJJJJJJJJJJJJJJJJJJJ7<FFJJJJJJJJFJJJJJJJJJ	AS:i:0	XS:i:0	XN:i:0	XM:i:0	XO:i:0	XG:i:0	NM:i:0	MD:Z:51	YT:Z:UU	RG:Z:RI_B_01_14
```
This works because the -v flag for grep means find all lines that DO NOT include '@'. Since all the header lines include @, they are excluded.

9. in an interactive session run /cm/shared/courses/dbarshis/21AdvGenomics/scripts/get_explain_sam_flags_advbioinf.py on 2-3 of your .sam files using * to select 2-3 at the same time.
```
[apear012@turing1 QCFastqs]$ salloc
salloc: Pending job allocation 9273049
salloc: job 9273049 queued and waiting for resources
salloc: job 9273049 has been allocated resources
salloc: Granted job allocation 9273049
[apear012@coreV1-22-016 QCFastqs]$ pwd
/cm/shared/courses/dbarshis/21AdvGenomics/sandboxes/apearson/data/fastq/QCFastqs
[apear012@coreV1-22-016 QCFastqs]$ python /cm/shared/courses/dbarshis/21AdvGenomics/scripts/get_explain_sam_flags_advbioinf.py *14_clippedtrimmed.fastq.sam
RI_B_01_14_clippedtrimmed.fastq.sam
['0', '272', '256', '16']
0 :
272 :
	read reverse strand
	not primary alignment
256 :
	not primary alignment
16 :
	read reverse strand
RI_W_01_14_clippedtrimmed.fastq.sam
['0', '272', '256', '16']
0 :
272 :
	read reverse strand
	not primary alignment
256 :
	not primary alignment
16 :
	read reverse strand
VA_B_01_14_clippedtrimmed.fastq.sam
['0', '272', '256', '16']
0 :
272 :
	read reverse strand
	not primary alignment
256 :
	not primary alignment
16 :
	read reverse strand
VA_W_01_14_clippedtrimmed.fastq.sam
['0', '272', '256', '16']
0 :
272 :
	read reverse strand
	not primary alignment
256 :
	not primary alignment
16 :
	read reverse strand
[apear012@coreV1-22-016 QCFastqs]$ python /cm/shared/courses/dbarshis/21AdvGenomics/scripts/get_explain_sam_flags_advbioinf.py *18_clippedtrimmed.fastq.sam
RI_B_01_18_clippedtrimmed.fastq.sam
['0', '272', '256', '16']
0 :
272 :
	read reverse strand
	not primary alignment
256 :
	not primary alignment
16 :
	read reverse strand
RI_W_01_18_clippedtrimmed.fastq.sam
['0', '272', '256', '16']
0 :
272 :
	read reverse strand
	not primary alignment
256 :
	not primary alignment
16 :
	read reverse strand
VA_B_01_18_clippedtrimmed.fastq.sam
['0', '272', '256', '16']
0 :
272 :
	read reverse strand
	not primary alignment
256 :
	not primary alignment
16 :
	read reverse strand
VA_W_01_18_clippedtrimmed.fastq.sam
['0', '272', '256', '16']
0 :
272 :
	read reverse strand
	not primary alignment
256 :
	not primary alignment
16 :
	read reverse strand
[apear012@coreV1-22-016 QCFastqs]$ python /cm/shared/courses/dbarshis/21AdvGenomics/scripts/get_explain_sam_flags_advbioinf.py *22_clippedtrimmed.fastq.sam
RI_B_01_22_clippedtrimmed.fastq.sam
['0', '272', '256', '16']
0 :
272 :
	read reverse strand
	not primary alignment
256 :
	not primary alignment
16 :
	read reverse strand
RI_W_01_22_clippedtrimmed.fastq.sam
['0', '272', '256', '16']
0 :
272 :
	read reverse strand
	not primary alignment
256 :
	not primary alignment
16 :
	read reverse strand
VA_B_01_22_clippedtrimmed.fastq.sam
['0', '272', '256', '16']
0 :
272 :
	read reverse strand
	not primary alignment
256 :
	not primary alignment
16 :
	read reverse strand
VA_W_01_22_clippedtrimmed.fastq.sam
['0', '272', '256', '16']
0 :
272 :
	read reverse strand
	not primary alignment
256 :
	not primary alignment
16 :
	read reverse strand
[apear012@coreV1-22-016 QCFastqs]$ python /cm/shared/courses/dbarshis/21AdvGenomics/scripts/get_explain_sam_flags_advbioinf.py *SNP_clippedtrimmed.fastq.sam
RI_B_08_SNP_clippedtrimmed.fastq.sam
['0', '272', '256', '16']
0 :
272 :
	read reverse strand
	not primary alignment
256 :
	not primary alignment
16 :
	read reverse strand
RI_W_08_SNP_clippedtrimmed.fastq.sam
['0', '272', '256', '16']
0 :
272 :
	read reverse strand
	not primary alignment
256 :
	not primary alignment
16 :
	read reverse strand
VA_B_09_SNP_clippedtrimmed.fastq.sam
['0', '272', '256', '16']
0 :
272 :
	read reverse strand
	not primary alignment
256 :
	not primary alignment
16 :
	read reverse strand
VA_W_08_SNP_clippedtrimmed.fastq.sam
['0', '272', '256', '16']
0 :
272 :
	read reverse strand
	not primary alignment
256 :
	not primary alignment
16 :
	read reverse strand
```

10. we need to run the read sorting step required for SNP calling, so if you have time, set up and run the following script on your .sam files to finish before Wednesday:
```
#!/bin/bash -l

#SBATCH -o OUTFILENAME.txt
#SBATCH -n 1         
#SBATCH --mail-user=EMAIL
#SBATCH --mail-type=END
#SBATCH --job-name=JOBNAME

enable_lmod
module load samtools/1
for i in *.sam; do `samtools view -bS $i > ${i%.sam}_UNSORTED.bam`; done

for i in *UNSORTED.bam; do samtools sort $i > ${i%_UNSORTED.bam}.bam
samtools index ${i%_UNSORTED.bam}.bam
done
```

```
[apear012@coreV1-22-016 QCFastqs]$ nano AP_Sort.sh
```
AP_Sort.sh:
```
#!/bin/bash -l

#SBATCH -o AP_Sort.txt
#SBATCH -n 1
#SBATCH --mail-user=pearsoac@evms.edu
#SBATCH --mail-type=END
#SBATCH --job-name=AP_Sort

enable_lmod
module load samtools/1
for i in *.sam; do `samtools view -bS $i > ${i%.sam}_UNSORTED.bam`; done

for i in *UNSORTED.bam; do samtools sort $i > ${i%_UNSORTED.bam}.bam
samtools index ${i%_UNSORTED.bam}.bam
done
```
```
[apear012@coreV1-22-016 QCFastqs]$ sbatch AP_Sort.sh 
Submitted batch job 9273050
[apear012@coreV1-22-016 QCFastqs]$ squeue -u apear012
             JOBID PARTITION     NAME     USER ST       TIME  NODES NODELIST(REASON) 
           9273050      main  AP_Sort apear012  R       0:11      1 coreV1-22-016 
           9273049      main       sh apear012  R      14:11      1 coreV1-22-016 
           9273048      main AP_Blast apear012  R      21:11      1 coreV1-22-016 
```

## Day 07 10-Feb-2021

1. Run the following command on your sprot output file to process into the contig length/match format that trinity examines
```
#!/bin/bash -l

#SBATCH -o OUTFILE.TXT
#SBATCH -n 1
#SBATCH --mail-user=YOUREMAIL.odu.edu
#SBATCH --mail-type=END
#SBATCH --job-name=JOBNAME

/cm/shared/apps/trinity/2.0.6/util/analyze_blastPlus_topHit_coverage.pl blastx.outfmt6 Trinity.fasta /cm/shared/apps/blast/databases/uniprot_sprot_Sep2018.fasta
```
```
[apear012@turing1 testassembly]$ pwd
/cm/shared/courses/dbarshis/21AdvGenomics/sandboxes/apearson/data/testassembly
[apear012@turing1 testassembly]$ nano AP_BlastxToSprot.sh
```
AP_BlastxToSprot.sh:
```
#!/bin/bash -l

#SBATCH -o AP_BlastxToSprot.txt
#SBATCH -n 1
#SBATCH --mail-user=pearsoac@evms.edu
#SBATCH --mail-type=END
#SBATCH --job-name=AP_BlastxToSprot

/cm/shared/apps/trinity/2.0.6/util/analyze_blastPlus_topHit_coverage.pl blastx.outfmt6 Trinity.fasta /cm/shared/apps/blast/databases/uniprot_sprot_Sep2018.fasta
```
```
[apear012@turing1 testassembly]$ sbatch AP_BlastxToSprot.sh 
Submitted batch job 9276483
[apear012@turing1 testassembly]$ squeue -u apear012
             JOBID PARTITION     NAME     USER ST       TIME  NODES NODELIST(REASON) 
           9276483      main AP_Blast apear012 PD       0:00      1 (Priority) 
[apear012@turing1 testassembly]$ ls
AP_Blast.sh   AP_BlastxToSprot.sh   blastx.outfmt6       blastx.outfmt6.hist.list         Trinity.fasta
AP_Blast.txt  AP_BlastxToSprot.txt  blastx.outfmt6.hist  blastx.outfmt6.w_pct_hit_length
[apear012@turing1 testassembly]$ cat *.hist
#hit_pct_cov_bin	count_in_bin	>bin_below
100	198	198
90	87	285
80	88	373
70	110	483
60	146	629
50	210	839
40	339	1178
30	650	1828
20	1178	3006
10	909	3915
[apear012@turing1 testassembly]$ grep -c '>' Trinity.fasta 
30194
```
2. Rm UNSORTED.bam
```
[apear012@coreV3-23-046 QCFastqs]$ pwd
/cm/shared/courses/dbarshis/21AdvGenomics/sandboxes/apearson/data/fastq/QCFastqs
[apear012@turing1 QCFastqs]$ ls
alignstatsAP.txt                               RI_W_08_SNP_clippedtrimmed.fastq_UNSORTED.bam
apam                                           *stats.txt.bam
APbowtie.sh                                    *stats.txt.sam
APbowtie.txt                                   *stats.txt_UNSORTED.bam
AP_Sort.sh                                     VA_B_01_14_clippedtrimmed.fastq
AP_Sort.txt                                    VA_B_01_14_clippedtrimmed.fastq.bam
RI_B_01_14_clippedtrimmed.fastq                VA_B_01_14_clippedtrimmed.fastq.bam.bai
RI_B_01_14_clippedtrimmed.fastq.bam            VA_B_01_14_clippedtrimmed.fastq.sam
RI_B_01_14_clippedtrimmed.fastq.bam.bai        VA_B_01_14_clippedtrimmed.fastq_UNSORTED.bam
RI_B_01_14_clippedtrimmed.fastq.sam            VA_B_01_18_clippedtrimmed.fastq
RI_B_01_14_clippedtrimmed.fastq_UNSORTED.bam   VA_B_01_18_clippedtrimmed.fastq.bam
RI_B_01_18_clippedtrimmed.fastq                VA_B_01_18_clippedtrimmed.fastq.bam.bai
RI_B_01_18_clippedtrimmed.fastq.bam            VA_B_01_18_clippedtrimmed.fastq.sam
RI_B_01_18_clippedtrimmed.fastq.bam.bai        VA_B_01_18_clippedtrimmed.fastq_UNSORTED.bam
RI_B_01_18_clippedtrimmed.fastq.sam            VA_B_01_22_clippedtrimmed.fastq
RI_B_01_18_clippedtrimmed.fastq_UNSORTED.bam   VA_B_01_22_clippedtrimmed.fastq.bam
RI_B_01_22_clippedtrimmed.fastq                VA_B_01_22_clippedtrimmed.fastq.bam.bai
RI_B_01_22_clippedtrimmed.fastq.bam            VA_B_01_22_clippedtrimmed.fastq.sam
RI_B_01_22_clippedtrimmed.fastq.bam.bai        VA_B_01_22_clippedtrimmed.fastq_UNSORTED.bam
RI_B_01_22_clippedtrimmed.fastq.sam            VA_B_09_SNP_clippedtrimmed.fastq
RI_B_01_22_clippedtrimmed.fastq_UNSORTED.bam   VA_B_09_SNP_clippedtrimmed.fastq.bam
RI_B_08_SNP_clippedtrimmed.fastq               VA_B_09_SNP_clippedtrimmed.fastq.bam.bai
RI_B_08_SNP_clippedtrimmed.fastq.bam           VA_B_09_SNP_clippedtrimmed.fastq.sam
RI_B_08_SNP_clippedtrimmed.fastq.bam.bai       VA_B_09_SNP_clippedtrimmed.fastq_UNSORTED.bam
RI_B_08_SNP_clippedtrimmed.fastq.sam           VA_W_01_14_clippedtrimmed.fastq
RI_B_08_SNP_clippedtrimmed.fastq_UNSORTED.bam  VA_W_01_14_clippedtrimmed.fastq.bam
RI_W_01_14_clippedtrimmed.fastq                VA_W_01_14_clippedtrimmed.fastq.bam.bai
RI_W_01_14_clippedtrimmed.fastq.bam            VA_W_01_14_clippedtrimmed.fastq.sam
RI_W_01_14_clippedtrimmed.fastq.bam.bai        VA_W_01_14_clippedtrimmed.fastq_UNSORTED.bam
RI_W_01_14_clippedtrimmed.fastq.sam            VA_W_01_18_clippedtrimmed.fastq
RI_W_01_14_clippedtrimmed.fastq_UNSORTED.bam   VA_W_01_18_clippedtrimmed.fastq.bam
RI_W_01_18_clippedtrimmed.fastq                VA_W_01_18_clippedtrimmed.fastq.bam.bai
RI_W_01_18_clippedtrimmed.fastq.bam            VA_W_01_18_clippedtrimmed.fastq.sam
RI_W_01_18_clippedtrimmed.fastq.bam.bai        VA_W_01_18_clippedtrimmed.fastq_UNSORTED.bam
RI_W_01_18_clippedtrimmed.fastq.sam            VA_W_01_22_clippedtrimmed.fastq
RI_W_01_18_clippedtrimmed.fastq_UNSORTED.bam   VA_W_01_22_clippedtrimmed.fastq.bam
RI_W_01_22_clippedtrimmed.fastq                VA_W_01_22_clippedtrimmed.fastq.bam.bai
RI_W_01_22_clippedtrimmed.fastq.bam            VA_W_01_22_clippedtrimmed.fastq.sam
RI_W_01_22_clippedtrimmed.fastq.bam.bai        VA_W_01_22_clippedtrimmed.fastq_UNSORTED.bam
RI_W_01_22_clippedtrimmed.fastq.sam            VA_W_08_SNP_clippedtrimmed.fastq
RI_W_01_22_clippedtrimmed.fastq_UNSORTED.bam   VA_W_08_SNP_clippedtrimmed.fastq.bam
RI_W_08_SNP_clippedtrimmed.fastq               VA_W_08_SNP_clippedtrimmed.fastq.bam.bai
RI_W_08_SNP_clippedtrimmed.fastq.bam           VA_W_08_SNP_clippedtrimmed.fastq.sam
RI_W_08_SNP_clippedtrimmed.fastq.bam.bai       VA_W_08_SNP_clippedtrimmed.fastq_UNSORTED.bam
RI_W_08_SNP_clippedtrimmed.fastq.sam
[apear012@turing1 QCFastqs]$ salloc
salloc: Pending job allocation 9276491
salloc: job 9276491 queued and waiting for resources
salloc: job 9276491 has been allocated resources
salloc: Granted job allocation 9276491
[apear012@coreV3-23-046 QCFastqs]$ rm *UNSORTED.bam
[apear012@coreV3-23-046 QCFastqs]$ ls
alignstatsAP.txt                          RI_W_08_SNP_clippedtrimmed.fastq.bam.bai
apam                                      RI_W_08_SNP_clippedtrimmed.fastq.sam
APbowtie.sh                               *stats.txt.bam
APbowtie.txt                              *stats.txt.sam
AP_Sort.sh                                VA_B_01_14_clippedtrimmed.fastq
AP_Sort.txt                               VA_B_01_14_clippedtrimmed.fastq.bam
RI_B_01_14_clippedtrimmed.fastq           VA_B_01_14_clippedtrimmed.fastq.bam.bai
RI_B_01_14_clippedtrimmed.fastq.bam       VA_B_01_14_clippedtrimmed.fastq.sam
RI_B_01_14_clippedtrimmed.fastq.bam.bai   VA_B_01_18_clippedtrimmed.fastq
RI_B_01_14_clippedtrimmed.fastq.sam       VA_B_01_18_clippedtrimmed.fastq.bam
RI_B_01_18_clippedtrimmed.fastq           VA_B_01_18_clippedtrimmed.fastq.bam.bai
RI_B_01_18_clippedtrimmed.fastq.bam       VA_B_01_18_clippedtrimmed.fastq.sam
RI_B_01_18_clippedtrimmed.fastq.bam.bai   VA_B_01_22_clippedtrimmed.fastq
RI_B_01_18_clippedtrimmed.fastq.sam       VA_B_01_22_clippedtrimmed.fastq.bam
RI_B_01_22_clippedtrimmed.fastq           VA_B_01_22_clippedtrimmed.fastq.bam.bai
RI_B_01_22_clippedtrimmed.fastq.bam       VA_B_01_22_clippedtrimmed.fastq.sam
RI_B_01_22_clippedtrimmed.fastq.bam.bai   VA_B_09_SNP_clippedtrimmed.fastq
RI_B_01_22_clippedtrimmed.fastq.sam       VA_B_09_SNP_clippedtrimmed.fastq.bam
RI_B_08_SNP_clippedtrimmed.fastq          VA_B_09_SNP_clippedtrimmed.fastq.bam.bai
RI_B_08_SNP_clippedtrimmed.fastq.bam      VA_B_09_SNP_clippedtrimmed.fastq.sam
RI_B_08_SNP_clippedtrimmed.fastq.bam.bai  VA_W_01_14_clippedtrimmed.fastq
RI_B_08_SNP_clippedtrimmed.fastq.sam      VA_W_01_14_clippedtrimmed.fastq.bam
RI_W_01_14_clippedtrimmed.fastq           VA_W_01_14_clippedtrimmed.fastq.bam.bai
RI_W_01_14_clippedtrimmed.fastq.bam       VA_W_01_14_clippedtrimmed.fastq.sam
RI_W_01_14_clippedtrimmed.fastq.bam.bai   VA_W_01_18_clippedtrimmed.fastq
RI_W_01_14_clippedtrimmed.fastq.sam       VA_W_01_18_clippedtrimmed.fastq.bam
RI_W_01_18_clippedtrimmed.fastq           VA_W_01_18_clippedtrimmed.fastq.bam.bai
RI_W_01_18_clippedtrimmed.fastq.bam       VA_W_01_18_clippedtrimmed.fastq.sam
RI_W_01_18_clippedtrimmed.fastq.bam.bai   VA_W_01_22_clippedtrimmed.fastq
RI_W_01_18_clippedtrimmed.fastq.sam       VA_W_01_22_clippedtrimmed.fastq.bam
RI_W_01_22_clippedtrimmed.fastq           VA_W_01_22_clippedtrimmed.fastq.bam.bai
RI_W_01_22_clippedtrimmed.fastq.bam       VA_W_01_22_clippedtrimmed.fastq.sam
RI_W_01_22_clippedtrimmed.fastq.bam.bai   VA_W_08_SNP_clippedtrimmed.fastq
RI_W_01_22_clippedtrimmed.fastq.sam       VA_W_08_SNP_clippedtrimmed.fastq.bam
RI_W_08_SNP_clippedtrimmed.fastq          VA_W_08_SNP_clippedtrimmed.fastq.bam.bai
RI_W_08_SNP_clippedtrimmed.fastq.bam      VA_W_08_SNP_clippedtrimmed.fastq.sam
```
```
[apear012@coreV3-23-046 QCFastqs]$ enable lmod
enable: Command not found.
[apear012@coreV3-23-046 QCFastqs]$ enable_lmod
[apear012@coreV3-23-046 QCFastqs]$ module load samtools
[apear012@coreV3-23-046 QCFastqs]$ samtools tview RI_B_01_14_clippedtrimmed.fastq.bam /cm/shared/courses/dbarshis/21AdvGenomics/classdata/Astrangia_poculata/refassembly/15079_Apoc_hostsym.fasta
1         11        21        31        41        51        61        71        
TCAGGACCAAGTCCACTCATGATCGGAAGAGAAAACTTCTTTTTGGGATCGAATGGCCGGGCTCCAGACTTAGATATTAT
                                                        ........................
                                                        ,,,,,,,,,,,,,,,,,,,,,,,,
                                                        ,,,,,,,,,,,,,,,,,,,,,,,,
                                                        ,,,,,,,,,,,,,,,,,,,,,,,,
                                                        ,,,,,,,,,,,,,,,,,,,,,,,,
```
3. Run the following to start genotyping your SNPs for filtering next class
```
#!/bin/bash -l

#SBATCH -o OUTFILENAME.txt
#SBATCH -n 1         
#SBATCH --mail-user=EMAIL
#SBATCH --mail-type=END
#SBATCH --job-name=JOBNAME

enable_lmod
module load dDocent
freebayes --genotype-qualities -f /cm/shared/courses/dbarshis/21AdvGenomics/classdata/Astrangia_poculata/refassembly/15079_Apoc_hostsym.fasta *.bam > YOURNAMEmergedfastqs.vcf
```
```
[apear012@turing1 QCFastqs]$ pwd
/cm/shared/courses/dbarshis/21AdvGenomics/sandboxes/apearson/data/fastq/QCFastqs
[apear012@turing1 QCFastqs]$ nano AP_Freebayes.sh
```
AP_Freebayes.sh:
```
#!/bin/bash -l

#SBATCH -o AP_Freebayes.txt
#SBATCH -n 1
#SBATCH --mail-user=pearsoac@evms.edu
#SBATCH --mail-type=END
#SBATCH --job-name=AP_Freebayes

enable_lmod
module load dDocent
freebayes --genotype-qualities -f /cm/shared/courses/dbarshis/21AdvGenomics/classdata/Astrangia_poculata/refassembly/15079_Apoc_hostsym.fasta *.bam > APmergedfastqs.vcf
```
```
[apear012@turing1 QCFastqs]$ pwd
/cm/shared/courses/dbarshis/21AdvGenomics/sandboxes/apearson/data/fastq/QCFastqs
[apear012@turing1 QCFastqs]$ sbatch AP_Freebayes.sh 
Submitted batch job 9276576
[apear012@turing1 QCFastqs]$ squeue -u apear012
             JOBID PARTITION     NAME     USER ST       TIME  NODES NODELIST(REASON) 
           9276576      main AP_Freeb apear012  R       0:02      1 coreV3-23-026 
           9276491      main       sh apear012  R    1:11:32      1 coreV3-23-046 
```

## Day 08 12-Feb-2021

1. Clean up your data directory by:

	-Making a SAMS folder and mv all your .sam files into that directory

```
[apear012@turing1 data]$ pwd
/cm/shared/courses/dbarshis/21AdvGenomics/sandboxes/apearson/data
[apear012@turing1 data]$ mkdir SAMS
[apear012@turing1 data]$ mv ./fastq/QCFastqs/*.sam SAMS
```

	-Make a BAMS folder and mv all your .bam files and .bam.bai files into that directory

```
[apear012@turing1 data]$ mkdir BAMS
[apear012@turing1 data]$ mv ./fastq/QCFastqs/*.bam BAMS
[apear012@coreV3-23-040 data]$ mv ./fastq/QCFastqs/*.bai BAMS
[apear012@coreV3-23-040 data]$ ls BAMS
RI_B_01_14_clippedtrimmed.fastq.bam       VA_B_01_14_clippedtrimmed.fastq.bam
RI_B_01_14_clippedtrimmed.fastq.bam.bai   VA_B_01_14_clippedtrimmed.fastq.bam.bai
RI_B_01_18_clippedtrimmed.fastq.bam       VA_B_01_18_clippedtrimmed.fastq.bam
RI_B_01_18_clippedtrimmed.fastq.bam.bai   VA_B_01_18_clippedtrimmed.fastq.bam.bai
RI_B_01_22_clippedtrimmed.fastq.bam       VA_B_01_22_clippedtrimmed.fastq.bam
RI_B_01_22_clippedtrimmed.fastq.bam.bai   VA_B_01_22_clippedtrimmed.fastq.bam.bai
RI_B_08_SNP_clippedtrimmed.fastq.bam      VA_B_09_SNP_clippedtrimmed.fastq.bam
RI_B_08_SNP_clippedtrimmed.fastq.bam.bai  VA_B_09_SNP_clippedtrimmed.fastq.bam.bai
RI_W_01_14_clippedtrimmed.fastq.bam       VA_W_01_14_clippedtrimmed.fastq.bam
RI_W_01_14_clippedtrimmed.fastq.bam.bai   VA_W_01_14_clippedtrimmed.fastq.bam.bai
RI_W_01_18_clippedtrimmed.fastq.bam       VA_W_01_18_clippedtrimmed.fastq.bam
RI_W_01_18_clippedtrimmed.fastq.bam.bai   VA_W_01_18_clippedtrimmed.fastq.bam.bai
RI_W_01_22_clippedtrimmed.fastq.bam       VA_W_01_22_clippedtrimmed.fastq.bam
RI_W_01_22_clippedtrimmed.fastq.bam.bai   VA_W_01_22_clippedtrimmed.fastq.bam.bai
RI_W_08_SNP_clippedtrimmed.fastq.bam      VA_W_08_SNP_clippedtrimmed.fastq.bam
RI_W_08_SNP_clippedtrimmed.fastq.bam.bai  VA_W_08_SNP_clippedtrimmed.fastq.bam.bai
*stats.txt.bam
```

	-rm your _unfiltered.vcf files if you have any

I didn't have any.


	-rm your .fastq files
	
```
[apear012@coreV3-23-040 QCFastqs]$ pwd
/cm/shared/courses/dbarshis/21AdvGenomics/sandboxes/apearson/data/fastq/QCFastqs
[apear012@coreV3-23-040 QCFastqs]$ rm *.fastq
```
	-Make a VCF folder in your data directory and mv your YOURNAMEmergedfastqs.vcf into this directory (if your freebayes job didn't complete then skip this step)

```
[apear012@coreV3-23-040 data]$ pwd
/cm/shared/courses/dbarshis/21AdvGenomics/sandboxes/apearson/data
[apear012@coreV3-23-040 data]$ mkdir VCF
[apear012@coreV3-23-040 data]$ mv ./fastq/QCFastqs/*.vcf VCF
```
2. Start an interactive session via salloc

Did this during previous steps.

3. cp the /cm/shared/courses/dbarshis/21AdvGenomics/classdata/Astrangia_poculata/VCF/mergedfastq_HEAAstrangiaAssembly.vcf to your VCF folder

```
[apear012@coreV3-23-040 VCF]$ pwd
/cm/shared/courses/dbarshis/21AdvGenomics/sandboxes/apearson/data/VCF
[apear012@coreV3-23-040 VCF]$ cp /cm/shared/courses/dbarshis/21AdvGenomics/classdata/Astrangia_poculata/VCF/mergedfastq_HEAAstrangiaAssembly.vcf .
[apear012@coreV3-23-040 VCF]$ ls
APmergedfastqs.vcf  mergedfastq_HEAAstrangiaAssembly.vcf
```

4. Determine the number of individuals and variant sites in the class vcf file (and yours if it worked) using:
/cm/shared/apps/vcftools/0.1.12b/bin/vcftools --vcf mergedfastq_HEAAstrangiaAssembly.vcf

```
[apear012@coreV3-23-040 VCF]$ vcftools --vcf APmergedfastqs.vcf 

VCFtools - 0.1.14
(C) Adam Auton and Anthony Marcketta 2009

Parameters as interpreted:
	--vcf APmergedfastqs.vcf

After filtering, kept 16 out of 16 Individuals
After filtering, kept 148757 out of a possible 148757 Sites
Run Time = 1.00 seconds
```

5. cp the /cm/shared/courses/dbarshis/21AdvGenomics/classdata/Astrangia_poculata/VCF/GoodCoralGenelistForVCFSubsetter.txt into your directory with your .vcf files

```
[apear012@coreV3-23-040 VCF]$ cp /cm/shared/courses/dbarshis/21AdvGenomics/classdata/Astrangia_poculata/VCF/GoodCoralGenelistForVCFSubsetter.txt .
[apear012@coreV3-23-040 VCF]$ ls
APmergedfastqs.vcf  GoodCoralGenelistForVCFSubsetter.txt  mergedfastq_HEAAstrangiaAssembly.vcf  out.log
```

6. Run our host vcf extractor on your merged vcf file using the following syntax:
```
/cm/shared/courses/dbarshis/21AdvGenomics/scripts/21Sp_vcfsubsetter_advbioinf.py GoodCoralGenelistForVCFSubsetter.txt mergedfastq_HEAAstrangiaAssembly.vcf
```

```
[apear012@coreV3-23-026 VCF]$ /cm/shared/courses/dbarshis/21AdvGenomics/scripts/21Sp_vcfsubsetter_advbioinf.py GoodCoralGenelistForVCFSubsetter.txt mergedfastq_HEAAstrangiaAssembly.vcf
```

7. Compare the number of variant sites in your three files (YOURNAMEmergedfastqs.vcf,  mergedfastq_HEAAstrangiaAssembly.vcf, and  mergedfastq_HEAAstrangiaAssembly_subset.vcf) using:
/cm/shared/apps/vcftools/0.1.12b/bin/vcftools --vcf

```
[apear012@turing1 VCF]$ ls
APmergedfastqs.vcf                    mergedfastq_HEAAstrangiaAssembly_subset.vcf  out.log
GoodCoralGenelistForVCFSubsetter.txt  mergedfastq_HEAAstrangiaAssembly.vcf
[apear012@turing1 VCF]$ vcftools --vcf mer
mergedfastq_HEAAstrangiaAssembly_subset.vcf* mergedfastq_HEAAstrangiaAssembly.vcf*
[apear012@turing1 VCF]$ vcftools --vcf mergedfastq_HEAAstrangiaAssembly_subset.vcf 

VCFtools - 0.1.14
(C) Adam Auton and Anthony Marcketta 2009

Parameters as interpreted:
	--vcf mergedfastq_HEAAstrangiaAssembly_subset.vcf

After filtering, kept 40 out of 40 Individuals
After filtering, kept 432676 out of a possible 432676 Sites
Run Time = 6.00 seconds
[apear012@turing1 VCF]$ vcftools --vcf mergedfastq_HEAAstrangiaAssembly.vcf

VCFtools - 0.1.14
(C) Adam Auton and Anthony Marcketta 2009

Parameters as interpreted:
	--vcf mergedfastq_HEAAstrangiaAssembly.vcf

After filtering, kept 40 out of 40 Individuals
After filtering, kept 1214003 out of a possible 1214003 Sites
Run Time = 11.00 seconds
[apear012@turing1 VCF]$ vcftools --vcf APmergedfastqs.vcf 

VCFtools - 0.1.14
(C) Adam Auton and Anthony Marcketta 2009

Parameters as interpreted:
	--vcf APmergedfastqs.vcf

After filtering, kept 16 out of 16 Individuals
After filtering, kept 148757 out of a possible 148757 Sites
Run Time = 2.00 seconds
```

8. Work through the [VCF filtering tutorial](http://www.ddocent.com/filtering/) until the following step:

Now that we have a list of individuals to remove, we can feed that directly into VCFtools for filtering.

vcftools --vcf raw.g5mac3dp3.recode.vcf --remove lowDP.indv --recode --recode-INFO-all --out raw.g5mac3dplm

```
[apear012@turing1 VCF]$ vcftools --vcf mer --max-missing 0.5 --mac 3 --minQ 30 --recode --recode-INFO-all --out raw.g5mac3
mergedfastq_HEAAstrangiaAssembly_subset.vcf* mergedfastq_HEAAstrangiaAssembly.vcf*
[apear012@turing1 VCF]$ vcftools --vcf mergedfastq_HEAAstrangiaAssembly_subset.vcf --max-missing 0.5 --mac 3 --minQ 30 --recode --recode-INFO-all --out raw.g5mac3

VCFtools - 0.1.14
(C) Adam Auton and Anthony Marcketta 2009

Parameters as interpreted:
	--vcf mergedfastq_HEAAstrangiaAssembly_subset.vcf
	--recode-INFO-all
	--mac 3
	--minQ 30
	--max-missing 0.5
	--out raw.g5mac3
	--recode

After filtering, kept 40 out of 40 Individuals
Outputting VCF file...
After filtering, kept 99853 out of a possible 432676 Sites
Run Time = 33.00 seconds
[apear012@turing1 VCF]$ ls
APmergedfastqs.vcf                           out.log
GoodCoralGenelistForVCFSubsetter.txt         raw.g5mac3.log
mergedfastq_HEAAstrangiaAssembly_subset.vcf  raw.g5mac3.recode.vcf
mergedfastq_HEAAstrangiaAssembly.vcf
[apear012@turing1 VCF]$ vcftools --vcf raw.g5mac3.recode.vcf --minDP 3 --recode --recode-INFO-all --out raw.g5mac3dp3 

VCFtools - 0.1.14
(C) Adam Auton and Anthony Marcketta 2009

Parameters as interpreted:
	--vcf raw.g5mac3.recode.vcf
	--recode-INFO-all
	--minDP 3
	--out raw.g5mac3dp3
	--recode

After filtering, kept 40 out of 40 Individuals
Outputting VCF file...
After filtering, kept 99853 out of a possible 99853 Sites
Run Time = 30.00 seconds
[apear012@turing1 VCF]$ vcftools --vcf raw.g5mac3dp3.recode.vcf --missing-indv

VCFtools - 0.1.14
(C) Adam Auton and Anthony Marcketta 2009

Parameters as interpreted:
	--vcf raw.g5mac3dp3.recode.vcf
	--missing-indv

After filtering, kept 40 out of 40 Individuals
Outputting Individual Missingness
After filtering, kept 99853 out of a possible 99853 Sites
Run Time = 3.00 seconds
[apear012@turing1 VCF]$ bash
apear012@turing1:/cm/shared/courses/dbarshis/21AdvGenomics/sandboxes/apearson/data/VCF$ mawk '!/IN/' out.imiss | cut -f5 > totalmissing
apear012@turing1:/cm/shared/courses/dbarshis/21AdvGenomics/sandboxes/apearson/data/VCF$ gnuplot << \EOF 
> set terminal dumb size 120, 30
> set autoscale 
> unset label
> set title "Histogram of % missing data per individual"
> set ylabel "Number of Occurrences"
> set xlabel "% of missing data"
> #set yr [0:100000]
> binwidth=0.01
> bin(x,width)=width*floor(x/width) + binwidth/2.0
> plot 'totalmissing' using (bin($1,binwidth)):(1.0) smooth freq with boxes
> pause -1
> EOF

                                         Histogram of % missing data per individual
  Number of Occurrences
      3 ++----------+-----------+-----------+-----------+------------+---***-----+-----------+-----------+----------++
        +           +           +           +           +       'totalmissing' using (bin($1,binwidth)):(1.0) ****** +
        |                                                                * *                                         |
        |                                                                * *                                         |
        |                                                                * *                                         |
        |                                                                * *                                         |
    2.5 ++                                                               * *                                        ++
        |                                                                * *                                         |
        |                                                                * *                                         |
        |                                                                * *                                         |
        |                                                                * *                                         |
        |                                                                * *                                         |
      2 ++                                                       **      * * ***  ******    ** ****   ****          ++
        |                                                        **      * * * *  * *  *    ** ** *   *  *           |
        |                                                        **      * * * *  * *  *    ** ** *   *  *           |
        |                                                        **      * * * *  * *  *    ** ** *   *  *           |
        |                                                        **      * * * *  * *  *    ** ** *   *  *           |
        |                                                        **      * * * *  * *  *    ** ** *   *  *           |
    1.5 ++                                                       **      * * * *  * *  *    ** ** *   *  *          ++
        |                                                        **      * * * *  * *  *    ** ** *   *  *           |
        |                                                        **      * * * *  * *  *    ** ** *   *  *           |
        |                                                        **      * * * *  * *  *    ** ** *   *  *           |
        |                                                        **      * * * *  * *  *    ** ** *   *  *           |
        +           +           +           +           +        **  +   * * * * +* *  *    ** ** *   *  *           +
      1 *********************************************************************************************************---++
       0.1         0.2         0.3         0.4         0.5          0.6         0.7         0.8         0.9          1
                                                      % of missing data

apear012@turing1:/cm/shared/courses/dbarshis/21AdvGenomics/sandboxes/apearson/data/VCF$ exit
exit
```

## Day 09 17-Feb-2021

1. Run one of the following sets of prescribed filters on your mergedfastq_HEAAstrangiaAssembly_subset.vcf, note these are fairly conservative filters
##Half the class run the following (I was instructed to do this one)
/cm/shared/apps/vcftools/0.1.12b/bin/vcftools --vcf mergedfastq_HEAAstrangiaAssembly_subset.vcf --maf 0.015 --max-alleles 2 --max-missing 0.5 --minQ 30 --minGQ 20 --minDP 3 --remove-indels --hwe 0.01 --recode --recode-INFO-all --out 18718_mergedfastq_HEAAstrangiaAssembly_subset_ClassFilters
##the other half run the filters we used from the paper
/cm/shared/apps/vcftools/0.1.12b/bin/vcftools --vcf mergedfastq_HEAAstrangiaAssembly_subset.vcf --max-missing 0.5 --mac 3 --minQ 30 --minDP 10 --max-alleles 2 --maf 0.015 --remove-indels --recode --recode-INFO-all --out 1578_mergedfastq_HEAAstrangiaAssembly_subset_HEAFilters

```
[apear012@coreV3-23-015 VCF]$ pwd
/cm/shared/courses/dbarshis/21AdvGenomics/sandboxes/apearson/data/VCF
[apear012@coreV3-23-015 VCF]$ /cm/shared/apps/vcftools/0.1.12b/bin/vcftools --vcf mergedfastq_HEAAstrangiaAssembly_subset.vcf --maf 0.015 --max-alleles 2 --max-missing 0.5 --minQ 30 --minGQ 20 --minDP 3 --remove-indels --hwe 0.01 --recode --recode-INFO-all --out 18718_mergedfastq_HEAAstrangiaAssembly_subset_ClassFilters

VCFtools - v0.1.12b
(C) Adam Auton and Anthony Marcketta 2009

Parameters as interpreted:
	--vcf mergedfastq_HEAAstrangiaAssembly_subset.vcf
	--recode-INFO-all
	--maf 0.015
	--max-alleles 2
	--minDP 3
	--minGQ 20
	--hwe 0.01
	--minQ 30
	--max-missing 0.5
	--out 18718_mergedfastq_HEAAstrangiaAssembly_subset_ClassFilters
	--recode
	--remove-indels

After filtering, kept 40 out of 40 Individuals
Outputting VCF file...
After filtering, kept 18718 out of a possible 432676 Sites
Run Time = 10.00 seconds
```
2. Make a population file containing two columns with no header, tab delimited text the first column should be the individual name and the second column the population to which that individual belongs

```
[apear012@coreV3-23-015 VCF]$ grep '#CHROM' mergedfastq_HEAAstrangiaAssembly.vcf > samplenames.txt
[apear012@coreV3-23-015 VCF]$ cat samplenames.txt 
#CHROM	POS	ID	REF	ALT	QUAL	FILTER	INFO	FORMAT	RI_W_06_merged	RI_W_07_merged	VA_B_03_merged	RI_W_02_merged	RI_W_04_merged	VA_W_09_SNP_clipped	RI_B_08_SNP_clipped	VA_W_08_SNP_clipped	VA_B_08_SNP_clipped	VA_W_02_merged	VA_B_07_merged	RI_B_05_merged	VA_W_06_merged	VA_W_04_merged	VA_W_01_merged	VA_B_10_SNP_clipped	VA_B_06_merged	VA_W_05_merged	RI_B_09_SNP_clipped	VA_W_10_SNP_clipped	RI_W_08_SNP_clipped	RI_B_06_merged	RI_W_10_SNP_clipped	RI_B_04_merged	VA_W_03_merged	RI_B_07_mergedRI_W_05_merged	RI_W_09_SNP_clipped	VA_B_01_merged	VA_B_09_SNP_clipped	RI_B_10_SNP_clipped	RI_W_01_merged	RI_B_01_merged	VA_B_04_merged	RI_B_02_merged	RI_W_03_merged	VA_B_02_merged	VA_W_07_merged	VA_B_05_merged	RI_B_03_merged
```
Copied the contents of samplenames.txt into BBedit and used regular expressions in find and replace as such:

```
FIND: (\w\w_\w)(_.*)
REPLACE: \1\2\t\1
```
```
[apear012@coreV2-22-030 VCF]$ nano popfile.txt
```
popfile.txt:
```
RI_W_06_merged	RI_W
RI_W_07_merged	RI_W
VA_B_03_merged	VA_B
RI_W_02_merged	RI_W
RI_W_04_merged	RI_W
VA_W_09_SNP_clipped	VA_W
RI_B_08_SNP_clipped	RI_B
VA_W_08_SNP_clipped	VA_W
VA_B_08_SNP_clipped	VA_B
VA_W_02_merged	VA_W
VA_B_07_merged	VA_B
RI_B_05_merged	RI_B
VA_W_06_merged	VA_W
VA_W_04_merged	VA_W
VA_W_01_merged	VA_W
VA_B_10_SNP_clipped	VA_B
VA_B_06_merged	VA_B
VA_W_05_merged	VA_W
RI_B_09_SNP_clipped	RI_B
VA_W_10_SNP_clipped	VA_W
RI_W_08_SNP_clipped	RI_W
RI_B_06_merged	RI_B
RI_W_10_SNP_clipped	RI_W
RI_B_04_merged	RI_B
VA_W_03_merged	VA_W
RI_B_07_merged	RI_B
RI_W_05_merged	RI_W
RI_W_09_SNP_clipped	RI_W
VA_B_01_merged	VA_B
VA_B_09_SNP_clipped	VA_B
RI_B_10_SNP_clipped	RI_B
RI_W_01_merged	RI_W
RI_B_01_merged	RI_B
VA_B_04_merged	VA_B
RI_B_02_merged	RI_B
RI_W_03_merged	RI_W
VA_B_02_merged	VA_B
VA_W_07_merged	VA_W
VA_B_05_merged	VA_B
RI_B_03_merged	RI_B
```

3. Convert your filtered .vcf file to genepop format using the following command:

/cm/shared/courses/dbarshis/21AdvGenomics/scripts/vcftogenepop_advbioinf.py YOURFILTERED.vcf YOUR_PopFile.txt

```
[apear012@coreV2-22-030 VCF]$ /cm/shared/courses/dbarshis/21AdvGenomics/scripts/vcftogenepop_advbioinf.py 18718_mergedfastq_HEAAstrangiaAssembly_subset_ClassFilters.recode.vcf popfile.txt 
Indivs with genotypes in vcf file: RI_W_06_merged	RI_W_07_merged	VA_B_03_merged	RI_W_02_merged	RI_W_04_merged	VA_W_09_SNP_clipped	RI_B_08_SNP_clipped	VA_W_08_SNP_clipped	VA_B_08_SNP_clipped	VA_W_02_merged	VA_B_07_merged	RI_B_05_merged	VA_W_06_merged	VA_W_04_merged	VA_W_01_merged	VA_B_10_SNP_clipped	VA_B_06_merged	VA_W_05_merged	RI_B_09_SNP_clipped	VA_W_10_SNP_clipped	RI_W_08_SNP_clipped	RI_B_06_merged	RI_W_10_SNP_clipped	RI_B_04_merged	VA_W_03_merged	RI_B_07_merged	RI_W_05_merged	RI_W_09_SNP_clipped	VA_B_01_merged	VA_B_09_SNP_clipped	RI_B_10_SNP_clipped	RI_W_01_merged	RI_B_01_merged	VA_B_04_merged	RI_B_02_merged	RI_W_03_merged	VA_B_02_merged	VA_W_07_merged	VA_B_05_merged	RI_B_03_merged
44 18718 18718 18718 18718 40
```

4. SCP your YOURFILE_allfilters.recode_subset_genepop.gen file to your laptop

```
(base) Andrews-MacBook-Air:day09 AndrewsComputer$ pwd
/Users/AndrewsComputer/Documents/Bio_ODU_2021/21sp_advgenomics/assignments_exercises/day09
(base) Andrews-MacBook-Air:day09 AndrewsComputer$ scp apear012@turing.hpc.odu.edu:/cm/shared/courses/dbarshis/21AdvGenomics/sandboxes/apearson/data/VCF/18718_mergedfastq_HEAAstrangiaAssembly_subset_ClassFilters.recode_genepop.gen .
apear012@turing.hpc.odu.edu's password: 
18718_mergedfastq_HEAAstrangiaAssembly_subset_ClassFilters.recode_genepop.ge 100% 4062KB 180.0KB/s   00:22    
(base) Andrews-MacBook-Air:day09 AndrewsComputer$ ls
18718_mergedfastq_HEAAstrangiaAssembly_subset_ClassFilters.recode_genepop.gen
adegenet_PCAs.R
adegenet_PCAs_HEAOutliers.R
homework_day09.txt
```

5. Switch to the adegenet_PCAs.R script and follow through the steps to produce some of the figures.

I did this. I had to import a number of dependencies for the R package 'adegenet' manually to get this to work. Specifically, the R package 'sf', a dependancy of 'adegent', gave me trouble and I had to go to download it in Chrome and manually add the package from the file browser.

## Day 10 19-Feb-2021

1. Work through the adegenet_PCAs.R script and follow through the steps to produce some of the figures.

I did this.

2. cd into your SAMS folder containing your .sams and run the following as an sbatch script on your sam files to generate read mapping counts from each individual file:
/cm/shared/courses/dbarshis/21AdvGenomics/scripts/countxpression_SB_advbioinf.py *.sam

```
[apear012@turing1 SAMS]$ pwd
/cm/shared/courses/dbarshis/21AdvGenomics/sandboxes/apearson/data/SAMS
[apear012@coreV2-25-017 SAMS]$ /cm/shared/courses/dbarshis/21AdvGenomics/scripts/countxpression_SB_advbioinf.py *.sam
```

3. Once your job from step 1 is finished, start an salloc session and run the following on your outputted _counts.txt files:
/cm/shared/courses/dbarshis/21AdvGenomics/scripts/ParseExpression2BigTable_advbioinf.py /cm/shared/courses/dbarshis/21AdvGenomics/classdata/Astrangia_poculata/host_genelist.txt YOURNAMEFullCounts_summed.txt NoMatch *_counts.txt

(I also had to rename the match_counts.txt file to matchcounts.txt so this command would not include it.)

```
[apear012@turing1 SAMS]$ mv match_counts.txt matchcounts.txt
[apear012@turing1 SAMS]$ /cm/shared/courses/dbarshis/21AdvGenomics/scripts/ParseExpression2BigTable_advbioinf.py /cm/shared/courses/dbarshis/21AdvGenomics/classdata/Astrangia_poculata/host_genelist.txt APFullCounts_summed.txt NoMatch *_counts.txt
Hits not matchedRI_B_01_14_clippedtrimmed.fastq_counts.txt=1698	RI_B_01_18_clippedtrimmed.fastq_counts.txt=169RI_B_01_22_clippedtrimmed.fastq_counts.txt=1698	RI_B_08_SNP_clippedtrimmed.fastq_counts.txt=1698	RI_W_01_14_clippedtrimmed.fastq_counts.txt=1698	RI_W_01_18_clippedtrimmed.fastq_counts.txt=1698	RI_W_01_22_clippedtrimmed.fastq_counts.txt=1698	RI_W_08_SNP_clippedtrimmed.fastq_counts.txt=1698	VA_B_01_14_clippedtrimmed.fastq_counts.txt=1698	VA_B_01_18_clippedtrimmed.fastq_counts.txt=1698	VA_B_01_22_clippedtrimmed.fastq_counts.txt=1698	VA_B_09_SNP_clippedtrimmed.fastq_counts.txt=1698	VA_W_01_14_clippedtrimmed.fastq_counts.txt=1698	VA_W_01_18_clippedtrimmed.fastq_counts.txt=1698	VA_W_01_22_clippedtrimmed.fastq_counts.txt=1698	VA_W_08_SNP_clippedtrimmed.fastq_counts.txt=1698
[apear012@turing1 SAMS]$ ls
APFullCounts_summed.txt                      stats.txt
matchcounts.txt                              VA_B_01_14_clippedtrimmed.fastq_counts.txt
RI_B_01_14_clippedtrimmed.fastq_counts.txt   VA_B_01_14_clippedtrimmed.fastq.sam
RI_B_01_14_clippedtrimmed.fastq.sam          VA_B_01_18_clippedtrimmed.fastq_counts.txt
RI_B_01_18_clippedtrimmed.fastq_counts.txt   VA_B_01_18_clippedtrimmed.fastq.sam
RI_B_01_18_clippedtrimmed.fastq.sam          VA_B_01_22_clippedtrimmed.fastq_counts.txt
RI_B_01_22_clippedtrimmed.fastq_counts.txt   VA_B_01_22_clippedtrimmed.fastq.sam
RI_B_01_22_clippedtrimmed.fastq.sam          VA_B_09_SNP_clippedtrimmed.fastq_counts.txt
RI_B_08_SNP_clippedtrimmed.fastq_counts.txt  VA_B_09_SNP_clippedtrimmed.fastq.sam
RI_B_08_SNP_clippedtrimmed.fastq.sam         VA_W_01_14_clippedtrimmed.fastq_counts.txt
RI_W_01_14_clippedtrimmed.fastq_counts.txt   VA_W_01_14_clippedtrimmed.fastq.sam
RI_W_01_14_clippedtrimmed.fastq.sam          VA_W_01_18_clippedtrimmed.fastq_counts.txt
RI_W_01_18_clippedtrimmed.fastq_counts.txt   VA_W_01_18_clippedtrimmed.fastq.sam
RI_W_01_18_clippedtrimmed.fastq.sam          VA_W_01_22_clippedtrimmed.fastq_counts.txt
RI_W_01_22_clippedtrimmed.fastq_counts.txt   VA_W_01_22_clippedtrimmed.fastq.sam
RI_W_01_22_clippedtrimmed.fastq.sam          VA_W_08_SNP_clippedtrimmed.fastq_counts.txt
RI_W_08_SNP_clippedtrimmed.fastq_counts.txt  VA_W_08_SNP_clippedtrimmed.fastq.sam
RI_W_08_SNP_clippedtrimmed.fastq.sam
```

4. scp YOURNAMEFullCounts_summed.txt to your laptop

```
(base) Andrews-MacBook-Air:Day10 AndrewsComputer$ pwd
/Users/AndrewsComputer/Documents/Bio_ODU_2021/21sp_advgenomics/assignments_exercises/Day10
(base) Andrews-MacBook-Air:Day10 AndrewsComputer$ scp apear012@turing.hpc.odu.edu:/cm/shared/courses/dbarshis/21AdvGenomics/sandboxes/apearson/data/SAMS/APFullCounts_summed.txt .
apear012@turing.hpc.odu.edu's password: 
APFullCounts_summed.txt                                                      100%  762KB 182.5KB/s   00:04    
(base) Andrews-MacBook-Air:Day10 AndrewsComputer$ ls
APFullCounts_summed.txt
coral_279_cloneremoved_neutral.filtered1SNPper_genepop.gen
coral_66_cloneremoved_highoutliers.filtered1SNPper_genepop.gen
homework_day10.txt
```

5. edit the first line of YOURNAMEFullCounts_summed.txt to remove the _counts.txt_UniqueTotReads from each sample name to just retain the actual informative part of the sample name (e.g., RI_W_06_18)

I used the find a replace feature of BBedit (without GREP) to replace each instance of '_clippedtrimmed.fastq_counts.txt_UniqueTotReads' from the end of the file names