# pair-end fastq file name like this 
# sample1_1.fastq, sample1_2.fastq
# sample2_1.fastq, sample2_2.fastq
# ....

######################################
# define reference
ref=ref.fa
bwa index ref.fa

# define samples
samplelist=(
sample1
sample2
sample3
)

#####################################
for i in ${samplelist[@]}
do
	echo "---------------"
	echo $i
	echo "---------------"
	
	echo "***Begain bwa mapping"
	# sequenced fastq file
	fastq1=$i"_1.fastq"
	fastq2=$i"_2.fastq"
	echo $fastq1
	echo $fastq2
	
	# define output basename
	myoutput=$i".fastq"
	
	# bwa mapping main program
  bwa mem $ref $fastq1 $fastq2 > $myoutput.bwa.sam

	echo "***Sam=>Bam=>Sorted=>Index"
	samtools view -bS $myoutput.bwa.sam > $myoutput.bwa.bam
	samtools sort $myoutput.bwa.bam $myoutput.bwa.sorted
	samtools index $myoutput.bwa.sorted.bam
	rm $myoutput.bwa.sam
	rm $myoutput.bwa.bam

	echo "***Samtools rmdup"
	samtools rmdup $myoutput.bwa.sorted.bam $myoutput.bwa_rmdup.sorted.bam 2>$myoutput.bwa.rmdup
	samtools index $myoutput.bwa_rmdup.sorted.bam

done
