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

## Second try some individual tools

The viralrecon pipelines consists of the following:

### Nanopore

1. Sequencing QC ([`pycoQC`](https://github.com/a-slide/pycoQC))
2. Aggregate pre-demultiplexed reads from MinKNOW/Guppy ([`artic guppyplex`](https://artic.readthedocs.io/en/latest/commands/))
3. Read QC ([`NanoPlot`](https://github.com/wdecoster/NanoPlot))
4. Align reads, call variants and generate consensus sequence ([`artic minion`](https://artic.readthedocs.io/en/latest/commands/))
5. Remove unmapped reads and obtain alignment metrics ([`SAMtools`](https://sourceforge.net/projects/samtools/files/samtools/))
6. Genome-wide and amplicon coverage QC plots ([`mosdepth`](https://github.com/brentp/mosdepth/))
7. Downstream variant analysis:
   - Count metrics ([`BCFTools`](http://samtools.github.io/bcftools/bcftools.html))
   - Variant annotation ([`SnpEff`](http://snpeff.sourceforge.net/SnpEff.html), [`SnpSift`](http://snpeff.sourceforge.net/SnpSift.html))
   - Consensus assessment report ([`QUAST`](http://quast.sourceforge.net/quast))
   - Lineage analysis ([`Pangolin`](https://github.com/cov-lineages/pangolin))
   - Clade assignment, mutation calling and sequence quality checks ([`Nextclade`](https://github.com/nextstrain/nextclade))
   - Individual variant screenshots with annotation tracks ([`ASCIIGenome`](https://asciigenome.readthedocs.io/en/latest/))
   - Create variants long format table collating per-sample information for individual variants ([`BCFTools`](http://samtools.github.io/bcftools/bcftools.html)), functional effect prediction ([`SnpSift`](http://snpeff.sourceforge.net/SnpSift.html)) and lineage analysis ([`Pangolin`](https://github.com/cov-lineages/pangolin))
8. Present QC, visualisation and custom reporting for sequencing, raw reads, alignment and variant calling results ([`MultiQC`](http://multiqc.info/))

I'll therefore, try some of these things by themselves.

### Nanoplot

#### Install

[Nanoplot](https://github.com/wdecoster/NanoPlot) Github.

`pip install NanoPlot`

then `pip install NanoPlot --upgrade`

command `NanoPlot -t 2 --fastq ../raw_fastq_pass/FAQ53111_pass_76d688ef_18.fastq --maxlength 40000 --plots dot --legacy hex` produces some plots but gives error
`AttributeError: 'list' object has no attribute 'lower'`

**Here are the plots:**

<p float="left">
  <img src="https://github.com/mattbawn/nanopore_FMDV/blob/main/pics/LengthvsQualityScatterPlot_dot.png" width="300" />
  <img src="https://github.com/mattbawn/nanopore_FMDV/blob/main/pics/Non_weightedHistogramReadlength.png" width="300" /> 
  <img src="https://github.com/mattbawn/nanopore_FMDV/blob/main/pics/Non_weightedLogTransformed_HistogramReadlength.png" width="300" />
</p>

<p float="left">
  <img src="https://github.com/mattbawn/nanopore_FMDV/blob/main/pics/WeightedHistogramReadlength.png" width="300" />
  <img src="https://github.com/mattbawn/nanopore_FMDV/blob/main/pics/WeightedLogTransformed_HistogramReadlength.png" width="300" /> 
  <img src="https://github.com/mattbawn/nanopore_FMDV/blob/main/pics/WeightedLogTransformed_HistogramReadlength.png" width="300" />
</p>

<p float="left">
  <img src="https://github.com/mattbawn/nanopore_FMDV/blob/main/pics/Yield_By_Length.png" width="300" />
</p>

### Arctic

#### Install

`conda install -c bioconda artic`

errors:

```

Retrieving notices: ...working... done
Collecting package metadata (current_repodata.json): done
Solving environment: failed with initial frozen solve. Retrying with flexible solve.
Solving environment: failed with repodata from current_repodata.json, will retry with next repodata source.
Collecting package metadata (repodata.json): done
Solving environment: failed with initial frozen solve. Retrying with flexible solve.
Solving environment: /
Found conflicts! Looking for incompatible packages.                                                iled

UnsatisfiableError: The following specifications were found to be incompatible with each other:

Output in format: Requested package -> Available versionsThe following specifications were found to incompatible with your system:

  - feature:/linux-64::__glibc==2.17=0
  - feature:|@/linux-64::__glibc==2.17=0

Your installed version is: 2.17

```


`git clone https://github.com/artic-network/fieldbioinformatics`

`cd fieldbioinformatics
python setup.py install`

```

led to error:

```
error: Setup script exited with error in PyVCF setup command: use_2to3 is invalid.
```

Info [here](https://stackoverflow.com/questions/69100275/error-while-downloading-the-requirements-using-pip-install-setup-command-use-2), suggested:

`pip install setuptools==58`

which led to:


```
Using /home/home02/fbsmbaw/miniconda3/lib/python3.9/site-packages
Finished processing dependencies for artic==1.2.3
```



