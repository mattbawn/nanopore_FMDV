# Nanopore
## Introduction

Analysis of nanopoe viral amplicon sequence

## some tests of software

### First Nextflow

Nexflow instructions [here](https://www.nextflow.io/docs/latest/getstarted.html#installation).

`wget -qO- https://get.nextflow.io | bash`

then `chmod +x nextflow`

using [viralrecon](https://nf-co.re/viralrecon)

ran test `../../nextflow run nf-core/viralrecon -profile test,conda --outdir first_test`

got error: 

```

No PSK available. Unable to resume.

 -- Check script '/home/home02/fbsmbaw/.nextflow/assets/nf-core/viralrecon/./workflows/illumina.nf' at line: 143 or see '.nextflow.log' file for more details
No PSK available. Unable to resume.

 -- Check script '/home/home02/fbsmbaw/.nextflow/assets/nf-core/viralrecon/./workflows/illumina.nf' at line: 137 or see '.nextflow.log' file for more details
No PSK available. Unable to resume.

 -- Check script '/home/home02/fbsmbaw/.nextflow/assets/nf-core/viralrecon/./workflows/illumina.nf' at line: 130 or see '.nextflow.log' file for more details
-[nf-core/viralrecon] Pipeline completed with errors-

```


