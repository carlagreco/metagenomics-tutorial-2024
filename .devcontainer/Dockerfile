# Use the official micromamba base image
FROM continuumio/miniconda3

# Set up a working directory
WORKDIR /workspace

# Install fastp, kraken2, and biopython using conda
RUN conda install -c bioconda make fastp kraken2 biopython krona -y

# Update PATH (conda automatically updates this, but just in case)
ENV PATH="/opt/conda/bin:${PATH}"

RUN /opt/conda/opt/krona/updateTaxonomy.sh

# Create the directory /project/workspace/data
RUN mkdir -p /data

# Download a sample data file into /project/workspace/data using wget
RUN wget ftp://ftp.sra.ebi.ac.uk/vol1/fastq/SRR876/007/SRR8761407/SRR8761407_2.fastq.gz -O /data/SampleA_R2.fastq.gz
RUN wget ftp://ftp.sra.ebi.ac.uk/vol1/fastq/SRR876/007/SRR8761407/SRR8761407_1.fastq.gz -O /data/SampleA_R1.fastq.gz

RUN mkdir -p /db/k2

RUN wget https://genome-idx.s3.amazonaws.com/kraken/k2_viral_20240112.tar.gz -O /db/k2.tar.gz && tar xvf /db/k2.tar.gz -C /db/k2
RUN rm /db/k2.tar.gz
