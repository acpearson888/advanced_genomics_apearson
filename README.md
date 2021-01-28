# Andrew's 2021 Advanced Bioinformatics Course Notebook

## Day 02 22-Jan-2021

4- execute a pwd command and start a log of your commands with a header for today's date in your README.md github logfile in your workspace
```
[apear012@turing1 exercises]$ pwd
/cm/shared/courses/dbarshis/21AdvGenomics/sandboxes/apearson/data/exercises
```
5- cp the Exercise2.fasta.gz and Exercise2.fastq.tar.gz files into your exercises directory
```
[apear012@turing1 exercises]$ cp /cm/shared/courses/dbarshis/21AdvGenomics/assignments_exercises/day02/Exercise* .
[apear012@turing1 exercises]$ ls
Exercise2.fasta.gz  Exercise2.fastq.tar.gz
```
6- unzip and untar the files
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

8- calculate how many sequences are in each file and add these results to your notebook file
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
9- cp the avg_cov_len_fasta_advbioinf.py from the /cm/shared/courses/dbarshis/21AdvGenomics/scripts directory into your class scripts directory
```
[apear012@turing1 scripts]$ cp /cm/shared/courses/dbarshis/21AdvGenomics/scripts/avg_cov_len_fasta_advbioinf.py .
[apear012@turing1 scripts]$ ls
avg_cov_len_fasta_advbioinf.py
```
10- start an interactive compute session and re-navigate to your exercises directory
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
11- run the avg_cov_len_fasta_DJB.py script on your Exercise2.fasta file by typing the path to the script followed by the Exercise2.fasta file name
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

1- Write an sbatch script to cp the files /cm/shared/courses/dbarshis/21AdvGenomics/classdata/Astrangia_poculata/originalfastqs/ into your own data directory, Andrew-HADB01
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
2- Add the content of your sbatch script to your logfile
Did this above.

3- submit the slurm script (sbatch scripname.sh) and verify that it's working (by squeue -u yourusername multiple times and checking the destination directory to make sure the files are being created)
```
[apear012@coreV2-25-072 data]$ sbatch APCopyLane01.sh
Submitted batch job 9270452
[apear012@coreV2-25-072 data]$ squeue -u apear012
             JOBID PARTITION     NAME     USER ST       TIME  NODES NODELIST(REASON) 
           9270428      main       sh apear012  R      39:36      1 coreV2-25-072 
           9270452      main APCopyLa apear012  R       0:29      1 coreV2-25-072 
```

4- Make sure this is all documented on your github notebook
See above.

5- Write a sbatch script to gunzip all the fastq.gz files in your data directory

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
This is the day03 homework:
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
