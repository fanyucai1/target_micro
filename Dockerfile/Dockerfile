FROM fanyucai1/base
RUN cd /software/ && git clone https://github.com/ndaniel/fastqtk.git && cd fastqtk && make -j20 && \
    cd /software/ && git clone https://github.com/lh3/seqtk.git && cd seqtk && make -j20 && \
    cd /software/ && git clone https://github.com/lh3/minimap2 && cd minimap2 && make -j20 &&  \
    cd /software/ && git clone https://github.com/ncbi/sra-human-scrubber.git && \
    cd /software/ && git clone https://github.com/lh3/bwa.git && cd bwa && make -j20 &&  \
    cd /usr/bin/ && wget http://opengene.org/fastp/fastp && chmod a+x ./fastp && \
    cd /software/ && git clone https://github.com/arq5x/bedtools2.git && cd bedtools2 && make -j20

RUN cd /software/ && \
    wget https://github.com/samtools/samtools/releases/download/1.20/samtools-1.20.tar.bz2 && tar xjvf samtools-1.20.tar.bz2 && \
    wget https://github.com/samtools/bcftools/releases/download/1.20/bcftools-1.20.tar.bz2 && tar xjvf bcftools-1.20.tar.bz2 && \
    cd samtools-1.20 && ./configure --prefix=/software/samtools && make -j20 && make install && rm -rf /software/samtools-1.20 && \
    cd /software/bcftools-1.20 && ./configure --prefix=/software/bcftools && make -j20 && make install && rm -rf /software/bcftools-1.20

RUN cd /software/ && wget https://github.com/voutcn/megahit/releases/download/v1.2.9/MEGAHIT-1.2.9-Linux-x86_64-static.tar.gz &&  \
    tar xzvf MEGAHIT-1.2.9-Linux-x86_64-static.tar.gz &&  \
    cd /software/ && wget http://www.usadellab.org/cms/uploads/supplementary/Trimmomatic/Trimmomatic-0.39.zip &&  \
    unzip Trimmomatic-0.39.zip && wget https://github.com/ablab/quast/releases/download/quast_5.2.0/quast-5.2.0.tar.gz &&  \
    tar -xzf quast-5.2.0.tar.gz &&  \
    wget https://github.com/weizhongli/cdhit/releases/download/V4.8.1/cd-hit-v4.8.1-2019-0228.tar.gz &&  \
    tar xzvf cd-hit-v4.8.1-2019-0228.tar.gz && cd cd-hit-v4.8.1-2019-0228 && make &&  \
    cd /usr/bin/ && wget -O nextclade https://github.com/nextstrain/nextclade/releases/latest/download/nextclade-x86_64-unknown-linux-gnu && chmod u+x ./nextclade && \
    cd /software/ && wget https://sourceforge.net/projects/bowtie-bio/files/bowtie2/2.5.3/bowtie2-2.5.3-linux-x86_64.zip && unzip bowtie2-2.5.3-linux-x86_64.zip

RUN mkdir -p /software/jvarkit/ && cd /software/ && wget https://github.com/andersen-lab/Freyja/archive/refs/heads/main.zip && unzip main.zip && \
    /software/Python-v3.11.0/bin/pip3 install sphinx-click seaborn sphinx_rtd_theme matplotlib numpy pysam pandas snakemake biopython cvxpy click joblib freyja-plot tqdm && \
    cd Freyja-main && /software/Python-v3.11.0/bin/python3 setup.py install
COPY jvarkit.jar /software/jvarkit/
RUN cd /software/ && /software/Miniconda3/bin/conda install -c bioconda -c conda-forge -c defaults ivar kraken2 krakentools bbmap && rm -rf *.gz *.bz2 *zip Freyja-main/