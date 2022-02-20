FROM ubuntu:20.04

RUN apt-get update

RUN DEBIAN_FRONTEND=noninteractive TZ=Etc/UTC apt-get -y install tzdata

RUN apt-get -y install ruby ruby-dev python3 r-base
RUN apt-get -y install nodejs npm

RUN apt-get -y install  openjdk-8-jdk
RUN apt-get -y install  scala

RUN apt-get -y install python3-pip

RUN pip install  'sphinx<3.1.0' mkdocs pydata_sphinx_theme ipython nbsphinx numpydoc 'jinja2<3.0.0'
RUN pip install  sphinx_plotly_directive 'numpy>=1.20.0' pyarrow pandas 'plotly>=4.8'

RUN apt-get install -y libcurl4-openssl-dev pandoc libfontconfig1-dev libharfbuzz-dev \
          libfribidi-dev libfreetype6-dev libpng-dev libtiff5-dev libjpeg-dev
RUN apt-get install -y libgit2-dev libssl-dev libxml2-dev

RUN Rscript -e "install.packages(c('devtools'), repos='https://cloud.r-project.org/')"
RUN Rscript -e "devtools::install_version('lintr', version='2.0.1', repos='https://cloud.r-project.org')"
RUN Rscript -e 'install.packages(c("knitr", "devtools", "testthat", "rmarkdown", "markdown", "e1071", "roxygen2"), repos="https://cloud.r-project.org/")'
RUN Rscript -e "devtools::install_version('pkgdown', version='2.0.1', repos='https://cloud.r-project.org')"
RUN Rscript -e "devtools::install_version('preferably', version='0.4', repos='https://cloud.r-project.org')"

RUN apt-get -y install git curl

#ADD spark /home/spark
WORKDIR /home
RUN git clone https://github.com/apache/spark.git
WORKDIR /home/spark/docs

RUN gem install bundler
RUN bundle install

RUN pip install markupsafe==2.0.1
RUN bundle exec jekyll build



EXPOSE 4000
