FROM python:2


RUN \
  apt-get update && \
  apt-get install -y \
    unzip && \
  apt-get clean && \
  apt-get purge && \
  rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*


#################################
# preprocessCMD.py dependencies #
#   - Super-Deduper             #
#   - sickle                    #
#   - FLASH2                    #
#   - bowtie2                   #
#   - scythe                    #
#################################

# Install Super-Deduper
ENV DIR /Super-Deduper
RUN git clone https://github.com/dstreett/Super-Deduper.git $DIR
RUN \
  cd $DIR && \
  make
RUN \
  cd /usr/local/bin/ && \
  ln -s $DIR/super_deduper

# Install sickle
ENV DIR /sickle
RUN git clone https://github.com/dstreett/sickle.git $DIR
RUN \
  cd $DIR && \
  make
RUN \
  cd /usr/local/bin/ && \
  ln -s $DIR/sickle

# Install flash2
ENV DIR /FLASH2
RUN git clone https://github.com/dstreett/FLASH2.git $DIR
RUN \
  cd $DIR && \
  make
RUN \
  cd /usr/local/bin/ && \
  ln -s $DIR/flash2

# Install bowtie2
ENV BOWTIE_VERSION 2.2.8
RUN \
  cd / && \
  wget -q http://downloads.sourceforge.net/project/bowtie-bio/bowtie2/$BOWTIE_VERSION/bowtie2-$BOWTIE_VERSION-source.zip && \
  unzip bowtie2-$BOWTIE_VERSION-source.zip && \
  cd bowtie2-$BOWTIE_VERSION && \
  make
ENV PATH $PATH:/bowtie2-$BOWTIE_VERSION

# Install scythe
ENV DIR /scythe
RUN git clone https://github.com/ucdavis-bioinformatics/scythe.git $DIR
RUN \
  cd $DIR && \
  make build
RUN \
  cd /usr/local/bin/ && \
  ln -s $DIR/scythe


##############################
# mappingCMD.py dependencies #
#   - bwa                    #
#   - bowtie2                #
#   - samtools               #
##############################

# Install bwa
ENV DIR /bwa
RUN git clone https://github.com/lh3/bwa.git $DIR
RUN \
  cd $DIR && \
  make
RUN \
  cd /usr/local/bin/ && \
  ln -s $DIR/bwa

# Install HTSlib
ENV DIR /htslib
RUN git clone https://github.com/samtools/htslib.git $DIR
RUN \
  cd $DIR && \
  make && \
  make install

# Install samtools
ENV DIR /samtools
RUN git clone https://github.com/samtools/samtools.git $DIR
RUN \
  cd $DIR && \
  make && \
  make install


#################################
# htseqcountCMD.py dependencies #
#   - samtools                  #
#   - htseq-count               #
#################################

# Install htseq-count
# http://www-huber.embl.de/users/anders/HTSeq/doc/install.html
# RUN pip install numpy matplotlib HTSeq
RUN pip install numpy
RUN pip install HTSeq


##################
# Install expHTS #
##################

RUN git clone https://github.com/msettles/expHTS.git /expHTS
RUN \
  cd /expHTS && \
  python setup.py install

# Define working directory.
WORKDIR /data

CMD [ "bash" ]
