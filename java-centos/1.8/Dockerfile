# Java 8 on CentOS 7.
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
# JAVA 8
################################################

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
		java-1.8.0-openjdk \
	&& yum clean all
	
# Data volume
VOLUME ["/data"]

# Other environment variables
ENV JAVA_HOME /usr

# The container shows the Java version by default
ENTRYPOINT ["java"]
CMD ["-version"]
