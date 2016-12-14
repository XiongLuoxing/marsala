# marsala
Welcome to marsala. <br />
The main site was http://xielab.github.io/marsala

## What is Marsala?
Marsala is a program that comprehensively detects variants (SNV and CNV) in PGS with linkage analysis. Marsala runs on Linux.

## What types of input can I use with Marsala?

Marsala is designed to work with reads from whole genome sequencing, although users have been successful in using Marsala with reads from specific region of genome.

In general, Marsala uses sequencing information from five parts:

1. Disease-Grandparent or Disease-child (A)

2. Disease-parent (F01) and Normal parent (F02)

3. Embryo (E)

4. Sperm (S)

5. polar body 1 and polar body 2

We here support 3 modes: 
  mode1. A+F01+E
  mode2. A+F01+F02+E
  mode3. F01+F02+E
  mode4. F01+F02+E+S
Polar body Could be added to any of the 4 modes. Once polar body 1 has been given, polar body 2 has to be present, too.

## How does Marsala detect variants?

1. SNV <br />
In all of four modes, the basic clue is to find the allele passed from F01 to E, and compare it with the diseases allele. The allele passed from F01 to E is decided by the genotypes called at nearby sites. <br />
If A is given(mode1 and mode2), the diseased allele is the allele passed from A to F01, which could be phased out by comparing the genotype of A and F01. <br />
If A is absent, the 2 alleles could be phased out by grouping and intergrating all the alleles passed from F01 to E, which comprise the 2 alleles in F01. And the diseased allele has mutation at the causal site. <br />


2. CNV <br />
Marsala estimate the DNA copy number of E and report whether E was normal.

This protocol has been validated in following research: <br />

Liying Yan,  Lei Huang,  Liya Xu,  Jin Huang,  Fei Ma,  Xiaohui Zhu,  Yaqiong Tang,  Mingshan Liu, Ying Lian,  Ping Liu,  Rong Li,  Sijia Lu,  Fuchou Tang,  Jie Qiao,   X. Sunney Xie.  Live births after simultaneous avoidance of monogenic diseases and chromosome abnormality by next-generation sequencing with linkage analyses.PNAS 2015 112 (52) 15964-15969

## Prerequisites

To use marsala, you will need the following programs in your PATH(The version we use is appended at the end):

bwa [0.7.15-r1140]<br />
http://bio-bwa.sourceforge.net/

samtools [1.3.1 (using htslib 1.3.1)] <br />
http://samtools.sourceforge.net/

bcftools [1.3.1 (using htslib 1.3.1)]<br />
https://samtools.github.io/bcftools/

GATK [3.3-0-g37228af]<br />
https://www.broadinstitute.org/gatk/

control-freec [v7.2]<br />
http://bioinfo-out.curie.fr/projects/freec/

bedtools [v2.25.0] <br />
http://bedtools.readthedocs.io/en/latest/

picard [1.119] <br />
http://broadinstitute.github.io/picard/

If necessary, you are recommended to change the commands in file marsala, to fit in the version of pragram with the parameters we use now. 

The reference genome version we use is hg19. 

## Obtaining and intalling Marsala

You can download the latest source release on github.

To install marsala, unpack the tarball and change directory to the package directory as follows:

`tar zxvf marsala-0.0.1.tar.gz`

`cd marsala-0.0.1`

Configure the package, specifying the install path of required tools as needed

`./configure`

Go to the folder data/, Download dbsnp frequency file, download to the this folder from GTAK Resource bundle as suggested:
https://software.broadinstitute.org/gatk/guide/article?id=1213
Extract the columns using commands:
bcftools query -f '%CHROM\t%POS\t%REF\t%ALT\t%CAF\t\n' [The downloaded dbSNP file.] > dbsnp_138.freq
Example of file dbSNP_138.freq:
chrM    64      C       T       [0.9373,0.06268]
chrM    72      T       C       [0.9878,0.01123]
chrM    93      A       G       [0.9663,0.03368]
chrM    97      G       A       [0.9972,0.002806]


## Using Marsala

Please just type marsala for detail help.
There is a example of how should you build a config file in -l parameter. We highly recommend you use tab separated config file instead of -da, -de parameters to input sequence file.



