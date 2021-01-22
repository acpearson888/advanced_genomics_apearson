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
Exercise2.fasta  Exercise2.fastq.tar.gz```

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
#9- cp the avg_cov_len_fasta_advbioinf.py from the /cm/shared/courses/dbarshis/21AdvGenomics/scripts directory into your class scripts directory
```
[apear012@turing1 scripts]$ cp /cm/shared/courses/dbarshis/21AdvGenomics/scripts/avg_cov_len_fasta_advbioinf.py .
[apear012@turing1 scripts]$ ls
avg_cov_len_fasta_advbioinf.py
```
#10- start an interactive compute session and re-navigate to your exercises directory
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
#11- run the avg_cov_len_fasta_DJB.py script on your Exercise2.fasta file by typing the path to the script followed by the Exercise2.fasta file name
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

