# Neo4j Community on CentOS 7.
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
# NEO4J COMMUNITY
################################################

ENV NEO4J_VERSION 3.0.7
ENV NEO4J_ARCHIVE neo4j-community-$NEO4J_VERSION-unix.tar.gz
ENV NEO4J_ARCHIVE_URL https://neo4j.com/artifact.php?name=$NEO4J_ARCHIVE

# UTF-8 locale
RUN localedef -c -f UTF-8 -i en_US en_US.UTF-8
ENV LANG en_US.UTF-8
ENV LANGUAGE en_US:en  
ENV LC_ALL en_US.UTF-8  

# Install NEO4J
RUN \
	yum -y update \
	&& yum -y install \
		which \
		wget \
		ca-certificates \
		java-1.8.0-openjdk-devel \
	&& yum clean all \
	&& wget $NEO4J_ARCHIVE_URL -O $NEO4J_ARCHIVE \
	&& mkdir /opt/neo4j \
	&& tar xvf $NEO4J_ARCHIVE -C /opt/neo4j \
	&& rm -f $NEO4J_ARCHIVE \
	&& ln -s /opt/neo4j/*neo4j* /opt/neo4j/default

# Data volume
VOLUME ["/data"]

# Configuration volume
VOLUME ["/conf"]

# Directories of binaries are added to PATH
ENV PATH=$PATH:/opt/neo4j/default/bin

# The NEO4J daemon starts
COPY entrypoint.sh /
ENTRYPOINT ["bash", "entrypoint.sh"]
CMD ["start"]
