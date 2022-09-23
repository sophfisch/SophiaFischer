# file types
FASTA (stores a variable number of sequence records, and for each record it stores the sequence itself, and a sequence ID) \
FASTQ (header, sequence, comment, quality) \
SAM/BAM (Alignments, mapping. SAM is human readable and BAM is binary) \
BED (Genomic ranges) \
GFF/GTF (Gene annotation) \
BEDgraphs (Genomic ranges) \
Wiggle les, BEDgraphs and BigWigs (Genomic scores) \
Indexed BEDgraphs/Wiggles \
VCFs (variants) \

# FASTQ
## phred
how certain something is, different encoding depending on when it was sequenced
important when using grep because the "at" is also a phred!!
awk 'NR % 4 == 1' SP1.fq | head  # get header line
awk 'NR % 4 == 2' SP1.fq | head  # get sequence line
awk 'NR % 4 == 3' SP1.fq | head  # get comment line
awk 'NR % 4 == 0' SP1.fq | head  # get quality line

## make fastq to fasta

awk 'NR % 4 == 1 {print ">"$1}; 
     NR % 4 == 2 {print}' SP1.fq \
     | head  
     
     
# BED files format
>https://genome.ucsc.edu/FAQ/FAQformat.html#format1

## BED3 and BED6
BED3 and name, score, strand \
chr22 1000 5000 cloneA 960 + \
chr22 2000 6000 cloneB 900 - \

## to go to the a.bed file directory
cd ~/course/soft/bedtools2/test/intersect/

awk -v OFS='\t' '{print $1,$2,$3,".",0,"."}' \
  recordsOutOfOrder.bed

cd - ## to go back to the previous directory

## bedtools 
>https://github.com/compbiozurich/UZH-BIO392/blob/imallona/ 

course-material/2022/imallona/exercises.md
By far, the most common question asked of two sets of genomic features is whether or not any of the features in the two sets “overlap” with one another. This is known as feature intersection. bedtools intersect allows one to screen for overlaps between two sets of genomic features. Moreover, it allows one to have fine control as to how the intersections are reported. bedtools intersect works with both BED/GFF/VCF and BAM files as input.
paper on bedtools:

>https://www.ncbi.nlm.nih.gov/pmc/articles/PMC2832824/

### intersect
bedtools intersect \
  -a  ~/course/soft/bedtools2/test/intersect/a.bed \
  -b  ~/course/soft/bedtools2/test/intersect/b.bed
### intersect only on same strand
bedtools intersect \
  -s \
  -a  ~/course/soft/bedtools2/test/intersect/a.bed \
  -b  ~/course/soft/bedtools2/test/intersect/b.bed
### no overlap at all
-v
### not sure what this does
bedtools intersect \
  -wao \
  -a  ~/course/soft/bedtools2/test/intersect/a.bed \
  -b  ~/course/soft/bedtools2/test/intersect/b.bed


# useful
cat - printing files onto the screen \
mv - moving and renaming files \
rm - removing files and directories \
chmod - changing access permissions \
grep - searching for strings in files \
wc - counting words \
sed - stream editing files \
awk - a full language to process texts 

Ctrl+A or Home: Go to the beginning of the line. \
Ctrl+E or End: Go to the end of the line.

## editing the standard ouput using pipes
echo "hello there"
echo "hello there" | sed "s/hello/hi/"
echo "hello there" | sed "s/hello/hi/" | sed "s/there/world/"
## redirecting the standard output to a file
echo hello > newfile.txt
ls -l newfile.txt
cat newfile.txt

## piping commands and redirecting to a file
echo hello | sed 's/hello/hElLo/' > newfile2.txt
ls -l newfile2.txt
cat newfile2.txt

