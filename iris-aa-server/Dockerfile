ARG IMAGE=store/intersystems/iris-aa-community:2020.3.0AA.331.0
ARG IMAGE=intersystemsdc/iris-aa-community:2020.3.0AA.331.0-zpm
ARG IMAGE=intersystemsdc/iris-ml-community:2021.2.0.651.0-zpm
ARG IMAGE=intersystemsdc/iris-ml-community
FROM $IMAGE
LABEL maintainer="Thomas Dyar <Thomas.Dyar@intersystems.com>"

USER root
RUN mkdir /data \
	&& chown irisowner /data
USER irisowner

# copy files
COPY data /data
RUN mv /data/voting_eligibility.csv /data/voting-eligibility.csv
COPY src /data/src
COPY iris.script /tmp/iris.script

# special extract treatment for hate-speech dataset
# RUN mkdir /data/hate-speech/ \
#	&& tar -xf /data/hate-speech.tar -C /data/

# load demo stuff
RUN iris start IRIS \
	&& iris session IRIS < /tmp/iris.script

# RUN rm -r /data/*
