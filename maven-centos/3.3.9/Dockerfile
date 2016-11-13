# Maven on CentOS 7.
# Copyright (C) 2016 Rodrigo Martínez <rodrigo@gradox.red>
#
# This program is free software: you can redistribute it and/or modify
# it under the terms of the GNU General Public License as published by
# the Free Software Foundation, either version 3 of the License, or
# (at your option) any later version.
# This program is distributed in the hope that it will be useful,
# but WITHOUT ANY WARRANTY; without even the implied warranty of
# MERCHANTABILITY or FITNESS FOR A PARTICULAR PURPOSE.  See the
# GNU General Public License for more details.
# You should have received a copy of the GNU General Public License
# along with this program.  If not, see <http://www.gnu.org/licenses/>.

FROM centos:7.2.1511
MAINTAINER "Rodrigo Martínez" <rodrigo@gradox.red>

################################################
# MAVEN
################################################

ENV MAVEN_VERSION 3.3.9
ENV MAVEN_ARCHIVE apache-maven-$MAVEN_VERSION-bin.tar.gz
ENV MAVEN_ARCHIVE_URL https://dist.apache.org/repos/dist/release/maven/maven-3/$MAVEN_VERSION/binaries/$MAVEN_ARCHIVE
ENV MAVEN_SHA_URL $MAVEN_ARCHIVE_URL.asc
ENV MAVEN_KEYS https://dist.apache.org/repos/dist/release/maven/KEYS

# UTF-8 locale
RUN localedef -c -f UTF-8 -i en_US en_US.UTF-8
ENV LANG en_US.UTF-8
ENV LANGUAGE en_US:en  
ENV LC_ALL en_US.UTF-8  

# Install Maven
RUN \
	yum -y update \
	&& yum -y install \
		wget \
		ca-certificates \
		java-1.8.0-openjdk-devel \
	&& yum clean all \
	&& wget $MAVEN_ARCHIVE_URL \
	&& wget $MAVEN_SHA_URL \
	&& wget $MAVEN_KEYS \
	&& gpg --import KEYS \
	&& gpg --verify $MAVEN_ARCHIVE.asc \
	&& mkdir /opt/maven \
	&& tar xvf $MAVEN_ARCHIVE -C /opt/maven \
	&& rm -f $MAVEN_ARCHIVE \
	&& rm -f $MAVEN_ARCHIVE.asc \
	&& rm -f KEYS \
	&& ln -s /opt/maven/*maven* /opt/maven/default
	
# Data volume
VOLUME ["/data"]

# Directories of binaries are added to PATH
ENV M2_HOME /opt/maven/default
ENV PATH=$M2_HOME/bin:$PATH

# Other environment variables
ENV JAVA_HOME /usr

# The container shows the Maven version by default
ENTRYPOINT ["mvn"]
CMD ["-version"]
