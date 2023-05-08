## Minimap2

[github page](https://github.com/lh3/minimap2)

`git clone https://github.com/lh3/minimap2`
`cd minimap2 && make`

Try nanopore mapping:

`/home/home02/fbsmbaw/minimap2/minimap2 -ax map-ont FMDV/FMDV_noribo.fa FMDV/raw_fastq_pass/FAQ53111_pass_76d688ef_17.fastq`

output
```
[M::mm_idx_gen::0.003*2.21] collected minimizers
[M::mm_idx_gen::0.006*2.54] sorted minimizers
[M::main::0.007*2.41] loaded/built the index for 1 target sequence(s)
[M::mm_mapopt_update::0.007*2.36] mid_occ = 52
[M::mm_idx_stat] kmer size: 15; skip: 10; is_hpc: 0; #seq: 1
[M::mm_idx_stat::0.007*2.33] distinct minimizers: 1310 (99.77% are singletons); average occurrences: 1.066; average spacing: 5.008; total length: 6996
[M::worker_pipeline::137.503*2.93] mapped 218214 sequences
[M::worker_pipeline::354.939*2.99] mapped 230097 sequences
[M::worker_pipeline::446.985*2.78] mapped 248765 sequences
[M::worker_pipeline::463.536*2.69] mapped 99929 sequences
[M::main] Version: 2.24-r1155-dirty
[M::main] CMD: /home/home02/fbsmbaw/minimap2/minimap2 -ax map-ont FMDV/FMDV_noribo.fa FMDV/raw_fastq_pass/all_FMDV.fastq
[M::main] Real time: 463.539 sec; CPU: 1245.418 sec; Peak RSS: 2.745 GB

```
Based on an answer [here](https://www.biostars.org/p/367626/#367648) You could call variants (using whatever variant calling software you like, GATK, freebayes etc.) from your .bam file and then use vcf-consensus (http://vcftools.sourceforge.net/perl_module.html#vcf-consensus) to build your consensus sequence. The code below should work:

`cat ref.fa | vcf-consensus file.vcf.gz > out.fa`



### sort sam file

From an [example here](http://quinlanlab.org/tutorials/samtools/samtools.html#samtools-sort)

`samtools sort aln_all.sam -o aln_all_sorted.sam`

get some mapping stats:

`samtools flagstat aln_all_sorted.sam > flagstat_sorted.txt`


Variant Call from sam file based on [this method](https://wikis.utexas.edu/display/bioiteam/Variant+calling+using+SAMtools).


