# Nextflow-pipeline
Helicobacter pylori Whole Genome pipeline analysis implemented in Nextflow.


1.bbduk tool has been implimented so far in nextflow for adapter trimming and quality-trimming

The parameters include
	
  bbduk.sh -Xmx1g in1=${reads[0]} in2=${reads[1]} out1=clean1.fastq out2=clean2.fastq \
  minlen=30 qtrim=rl trimq=10 ktrim=r k=30 mink=11 ref=${genome_file} hdist=1 stats=stats.txt tbo tpe

Explanation
.......ref" means "reference sequence" (in this case, adapters); "qtrim=rl" means quality-trim the right and left sides; "trimq=30"   means trim regions with average quality below Q30; "ktrim=r" means "look for adapter kmers, and when found, trim to the right"; "k=30" means "try to match 30-mers between the read and reference"; "mink=11" means "use kmers as short as 11 at the end of the read"; "tbo" and "tpe" allow better adapter trimming of reads that are paired.flags "tbo", which specifies to also trim adapters based on pair overlap detection (which does not require known adapter sequences), and "tpe", which specifies to trim both reads to the same length (in the event that an adapter kmer was only detected in one of them)."stats" will produce a report of which contaminant sequences were seen, and how many reads had them.

N.B It's best to do adapter-trimming first, then quality-trimming, because if you do quality-trimming first, sometimes adapters will be partially trimmed and become too short to be recognized as adapter sequence. When you run BBDuk with both quality-trimming and adapter-trimming in the same run, it will do adapter-trimming first, then quality-trimming.



