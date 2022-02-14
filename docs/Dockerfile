FROM debian:latest

RUN apt-get update
RUN apt-get -y install curl pip gnupg
RUN apt-get -y install ruby-full python3

RUN pip install 'sphinx<3.1.0' mkdocs numpy pydata_sphinx_theme ipython nbsphinx numpydoc sphinx-plotly-directive 'jinja2<3.0.0'

RUN apt-get install -y r-base pandoc libxml2-dev libcurl4-openssl-dev libssl-dev libfontconfig1-dev \
    libharfbuzz-dev   libfribidi-dev libfreetype6-dev libpng-dev libtiff5-dev libjpeg-dev

RUN Rscript -e 'install.packages(c("curl", "knitr", "devtools", "testthat", "rmarkdown", "markdown", "e1071"), repos="https://cloud.r-project.org/")'
RUN Rscript -e 'devtools::install_version("roxygen2", version = "7.1.2", repos="https://cloud.r-project.org/")'
RUN Rscript -e "devtools::install_version('pkgdown', version='2.0.1', repos='https://cloud.r-project.org')"
RUN Rscript -e "devtools::install_version('preferably', version='0.4', repos='https://cloud.r-project.org')"

# Install JDK and Scala
RUN echo 'deb http://security.debian.org/debian-security stretch/updates main' >> /etc/apt/sources.list
RUN apt-get update
RUN apt-get -y install  openjdk-8-jdk
RUN apt-get -y install  scala

#ENV JAVA_HOME=/usr/lib/jvm/java-8-openjdk-amd64/jre/

ADD spark /home/spark
WORKDIR /home/spark/docs

RUN gem install bundler
RUN bundle install
RUN bundle exec jekyll build


EXPOSE 4000