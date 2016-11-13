# MongoDB (Vanilla) on CentOS 7.
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
# MONGODB
################################################

ENV MONGODB_VERSION 3.2.10
ENV MONGODB_ARCHIVE mongodb-linux-x86_64-rhel70-$MONGODB_VERSION.tgz
ENV MONGODB_ARCHIVE_URL http://downloads.mongodb.org/linux/$MONGODB_ARCHIVE
ENV MONGODB_SHA_URL $MONGODB_ARCHIVE_URL.sha1

# UTF-8 locale
RUN localedef -c -f UTF-8 -i en_US en_US.UTF-8
ENV LANG en_US.UTF-8
ENV LANGUAGE en_US:en  
ENV LC_ALL en_US.UTF-8  

# Install MongoDB
RUN \
	yum -y update \
	&& yum -y install \
		wget \
		ca-certificates \
	&& yum clean all \
	&& wget $MONGODB_ARCHIVE_URL \
	&& wget $MONGODB_SHA_URL \
	&& cat $MONGODB_ARCHIVE.sha1 | sha1sum -c - \
	&& mkdir /opt/mongodb \
	&& tar xvf $MONGODB_ARCHIVE -C /opt/mongodb \
	&& rm -f $MONGODB_ARCHIVE \
	&& rm -f $MONGODB_ARCHIVE.sha1 \
	&& ln -s /opt/mongodb/*mongodb* /opt/mongodb/default

# Data volume
VOLUME ["/data"]

# Configuration volume
VOLUME ["/conf"]

# Directories of binaries are added to PATH
ENV PATH=$PATH:/opt/mongodb/default/bin

# The MongoDB daemon starts
ENTRYPOINT ["mongod"]
CMD ["--dbpath=/data"]
