<div align="center">
    <img src="http://146.56.237.198:3838/findGSEX/findGSEX_logo1205.png" width="50%" height=auto>
</div>

# findGSEX

Accurate estimating genome size is a crucial task in sequencing projects. Current methods often struggle with polyploidy or become inefficient when dealing with species that exceed a ploidy level of six. To address these challenges, we introduce findGSEX, an enhanced version of findGSE. findGSEX utilizes a segmented fitting approach to fit a normal distribution to polyploid species within a segmented framework. This ap-proach simplifies the process of single fitting while significantly expanding the range of ploidy levels it can handle

# News 🌟

We have released our backend-server findGSEX and provide a CPU-based version of [findGSEX](http://146.56.237.198:3838/findGSEX/) online platform. Please check it out!!!


## Installation & Usage

## Instructions for running Jellyfish:

1. Download and install jellyfish from: [http://www.genome.umd.edu/jellyfish.html#Release](http://www.genome.umd.edu/jellyfish.html#Release)
2. Count kmers using jellyfish:

```bash
jellyfish count -C -m 21 -t 1 -s 5G *.fastq -o reads.mer
```

*Note: Adjust the memory (-s) and threads (-t) parameters according to your server. This example uses 1 threads and 5GB of RAM. The kmer length (-m) may need to be scaled if you have low coverage or a high error rate. Always use 'canonical kmers' (-C).*

3. Export the kmer count histogram:

```bash
jellyfish histo -h 30000000 -t 10 -o reads.histo reads.mer
```

*Note: The thread count (-t) should be scaled according to your server.*

4. Upload `reads.histo` to findGSEX.

## Instructions for installing findGSEX package

1. Install `devtools`:

```bash
install.packages("devtools")
```

2. Install directly from GitHub:


```bash
devtools::install_github("sperfu/findGSEX")
```

### Usage:
```R
# Set options (optional):

options(warn = -1)

# Define input parameters:

path <- "histo_files"
samples <- "your_file.histo"
sizek <- 21
exp_hom <- 200
ploidy <- 4
output_dir <- "outfiles"
xlimit <- -1
ylimit <- -1
range_left <- exp_hom * 0.2
range_right <- exp_hom * 0.2

#Call the findGSEX function with specified parameters:

findGSEX(path, samples, sizek, exp_hom, ploidy, range_left, range_right, xlimit, ylimit, output_dir)

# For any questions, usage inquiries, or reporting potential bugs, please contact the author.
```

After running, You will find 'your_file.histo_hap_genome_size_est.pdf' in your output_dir folder, please give it a try!!!


## Note:

If you enconter problem when installing devtools, especially for those packages below, please consider install them using conda install command:

```bash
conda install -c conda-forge r-gert
conda install -c conda-forge r-textshaping
conda install -c conda-forge r-ragg
conda install -c conda-forge r-pkgdown
```

If you enconter issues like:

1. could not find function "brewer.pal"
   
2.  could not find function "alpha"

Solutions:

```R
library(RColorBrewer)
library(ggplot2)
```



