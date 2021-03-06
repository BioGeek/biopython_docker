FROM ubuntu:wily
MAINTAINER Tiago Antao <tra@popgen.net>

ENV DEBIAN_FRONTEND noninteractive
#We need this for phylip
RUN echo 'deb http://archive.ubuntu.com/ubuntu wily multiverse' >> /etc/apt/sources.list

RUN apt-get update
RUN apt-get upgrade -y --force-yes
RUN apt-get install -y --force-yes build-essential
RUN apt-get install -y --force-yes git python3-numpy wget gcc g++ python3-dev unzip make
RUN apt-get install -y --force-yes python3-matplotlib python3-reportlab python3-pip r-base
RUN apt-get install -y --force-yes clustalw fasttree t-coffee python3-pil
RUN apt-get install -y --force-yes bwa ncbi-blast+ emboss clustalo phylip mafft muscle
RUN apt-get install -y --force-yes samtools phyml wise raxml language-pack-en
RUN apt-get install -y --force-yes embassy-phylip paml probcons python3-pandas
RUN apt-get install -y --force-yes python3.5-dev libxft-dev
RUN apt-get clean
#for Phylo_CDAO
# RUN pip3 install pip --upgrade
RUN pip3 install rdflib --upgrade
RUN pip3 install cython --upgrade
RUN pip3 install numpy --upgrade
RUN pip3 install Pillow --upgrade
RUN pip3 install matplotlib --upgrade
RUN pip3 install pandas --upgrade

#Manual software
RUN echo "export DIALIGN2_DIR=/tmp" >> .bashrc

#reportlab fonts
RUN wget http://www.reportlab.com/ftp/fonts/pfbfer.zip
WORKDIR cd /usr/lib/python3.4/dist-packages/reportlab
RUN  mkdir fonts
WORKDIR cd /usr/lib/python3.4/dist-packages/reportlab/fonts
RUN unzip /pfbfer.zip
RUN mkdir -p /usr/lib/python3.5/dist-packages/reportlab/fonts
WORKDIR /usr/lib/python3.5/dist-packages/reportlab/fonts
RUN unzip /pfbfer.zip
WORKDIR /
RUN rm pfbfer.zip



#genepop
RUN mkdir genepop
WORKDIR /genepop
RUN wget http://kimura.univ-montp2.fr/~rousset/sources.tar.gz
RUN tar zxf sources.tar.gz
RUN g++ -DNO_MODULES -o Genepop GenepopS.cpp -O3
RUN cp Genepop /usr/bin
WORKDIR /
RUN rm -rf genepop

#fdist
RUN mkdir fdist2
WORKDIR /fdist2
RUN wget http://www.maths.bris.ac.uk/~mamab/software/fdist2.zip
RUN unzip fdist2.zip
RUN gcc -o fdist2 -O fdist2.c -lm
RUN gcc -o cplot -O cplot.c as100.c as99.c -lm
RUN gcc -o pv -O pv.c as100.c as99.c -lm
RUN gcc -o datacal -O datacal.c -lm
RUN cp datacal pv cplot fdist2 /usr/bin
WORKDIR /
RUN rm -rf fdist2


#dfdist
RUN wget http://www.maths.bris.ac.uk/~mamab/stuff/Dfdist_a.zip
RUN unzip Dfdist_a
WORKDIR Dfdist_a
RUN gcc -O -o Ddatacal Ddatacal.c -lm
RUN gcc -O -o Dfdist Dfdist.c -lm
RUN gcc -O -o pv2 pv2.c -lm
RUN gcc -O -o cplot2 cplot2.c -lm
RUN cp pv2 Dfdist Ddatacal cplot2 /usr/bin
WORKDIR /
RUN rm -rf Dfdist_a*

#msaprobs
RUN wget "http://sourceforge.net/projects/msaprobs/files/latest/download?source=files" -O MSA.tar.gz
RUN tar zxf MSA.tar.gz
WORKDIR /MSAProbs-0.9.7/MSAProbs
RUN make
RUN cp msaprobs /usr/bin
WORKDIR /

#fastsimcoal
RUN wget http://cmpg.unibe.ch/software/fastsimcoal2/downloads/fsc_linux64.zip
RUN unzip fsc_linux64.zip
RUN chmod a+x fsc_linux64/fsc25211
RUN cp fsc_linux64/fsc25211 /usr/bin/fsc252
RUN rm -rf fsc_*

#DSSP
RUN wget ftp://ftp.cmbi.ru.nl/pub/software/dssp/dssp-2.0.4-linux-amd64
RUN mv dssp-2.0.4-linux-amd64 /usr/bin/dssp
RUN chmod a+x /usr/bin/dssp

#XXmotif
WORKDIR /usr/local/bin
RUN wget "http://xxmotif.genzentrum.lmu.de/index.php?id=download&version=64" -O xx.tar.gz
RUN tar zxf xx.tar.gz
RUN rm xx.tar.gz
WORKDIR /
ENV PYTHON_PATH /biopython

#Biopython
RUN git clone https://github.com/biopython/biopython.git
WORKDIR /biopython
RUN python3.5 setup.py install
