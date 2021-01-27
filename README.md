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