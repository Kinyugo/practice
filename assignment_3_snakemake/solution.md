# snakemake

snakemake is a tool for managing data analysis workflows that enables **reproducibility** and **scalability**. Snakemake workflow can support seamless migration to high performance computing systems, e.g clusters and grid, without having to modify the workflow too much. 

## Setup 
snakemake can be installed in a conda/mamba environment by following the steps below:
 1. Install mamba package manager
    ```
    conda install -n <channel name> -c conda-forge mamba
    ```
 2. Install snakemake in your desired environment
    ```
    conda activate base
    mamba create -c conda-forge -c bioconda -n snakemake snakemake
    ```
 ## Steps for working with snakemake
 1. Create an empty workflow in the current directory
    ```
    touch Snakefile
    snakemake -n
    ```
 2. Create a rule following the snakemake syntax e.g: to map sequences to the reference genome create a rule file that looks like this.
    ```
    rule map_reads:
      input:
          "data/genome.fa",
          "data/samples/A.fastq"
      output:
          "results/mapped/A.bam"
      conda:
          "envs/mapping.yaml"
      shell:
          "bwa mem {input} | samtools view -b - > {output}"
    ```
 3. Run your workflow 
    ```
    snakemake --use-conda results/mapped/A.bam --cores 1
    ```
## Key takeaways
1. snakemake is a workflow management system.
2. snakemake workflow defines the input, outputs and the command that maps the inputs to outputs in rules, within the _Snakefile_. 
 
