# Aerospike Server (Community) over CentOS 7.
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
# AEROSPIKE SERVER
################################################

ENV AEROSPIKE_VERSION 3.9.1.1
ENV AEROSPIKE_ARCHIVE aerospike-server-community-${AEROSPIKE_VERSION}-el7.tgz
ENV AEROSPIKE_ARCHIVE_URL "https://www.aerospike.com/artifacts/aerospike-server-community/${AEROSPIKE_VERSION}/$AEROSPIKE_ARCHIVE"

# UTF-8 locale
RUN localedef -c -f UTF-8 -i en_US en_US.UTF-8
ENV LANG en_US.UTF-8
ENV LANGUAGE en_US:en  
ENV LC_ALL en_US.UTF-8  

# Install Aerospike
RUN \
  yum update -y \
  &&  yum install -y wget logrotate ca-certificates \
  && wget $AEROSPIKE_ARCHIVE_URL \
  && wget $AEROSPIKE_ARCHIVE_URL".sha256" -O sha256 \
  && cat sha256 | sha256sum -c - \
  && mkdir aerospike \
  && tar xzf $AEROSPIKE_ARCHIVE --strip-components=1 -C aerospike \
  && rpm -i aerospike/aerospike-server-*.rpm \
  && mkdir -p /var/log/aerospike/ \
  && mkdir -p /var/run/aerospike/ \
  && rm -rf $AEROSPIKE_ARCHIVE aerospike /var/lib/apt/lists/*

# Mount the Aerospike data directory
VOLUME ["/opt/aerospike/data"]
VOLUME ["/etc/aerospike"]

# Execute the run script in foreground mode
COPY entrypoint.sh /
ENTRYPOINT ["/entrypoint.sh"]
CMD ["asd"]
