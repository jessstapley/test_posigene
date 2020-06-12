# Using Posigene
https://github.com/gengit/PosiGene

# Created cds fasta files
# step 1. 
Map whole genome sequence reads (Illumina) to a reference genome using bwa. Call variants and pull out an individual-sample-reference fasta for each sample using GATK. The individual-sample-reference fasta will differ to the reference genome at variable sites. At sites with inadequate coverage to call a variant, the individual-sample-reference genome is identical to the reference genome (not missing)

```
java -Xmx4g -jar /cluster/apps/gatk/3.7/x86_64/GenomeAnalysisTK.jar \
     -T FastaAlternateReferenceMaker \
     -IUPAC ${name} \
     -R /cluster/work/gdc/shared/p427/GenAccFiles/EfFl1_v0.2.fna \
     -o ${path_out}/${name}.fasta \
     -V ${path_out}/${name}.recode.vcf 
```
# step 2
Using the gff for the reference genome I extracted the cds from each individual-sample-reference genome using bedtools.

```
bedtools getfasta -fi indv_ref_genome_unfiltered/"$p".fasta -bed /file.gff3 > Efcds_"$p".fasta
```
# step 3
Ran posigene as follows

```
perl PosiGene.pl -o=Dg_target -as=Taxa1 -tn=10 -ts=Taxa2 -bn=Dg -rs=Taxa3:Efcds_SRR8238189.1.fasta -nhsbr=Taxa2:Efcds_12H_1702_18.fasta,Taxa4:Efcds_11H_1725_18.fasta,Taxa5:Efcds_5A_1715_16.fasta,Taxa1:Efcds_SRR5420176.1.fasta
'''

# Error
Step 4/7, 9/10 threads returned
Step 4/7, 10/10 threads returned
Step 4/7, creating concatenated alignment...
An error has occured during execution...
Try to run the program again and use the parameter "-continue" to start again from the last valid point of execution...

