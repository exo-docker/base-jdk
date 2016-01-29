# Dockerizing a base images with:
#
#   - Ubuntu 14.04
#   - Oracle JDK 8u66
#
# Build:    docker build -t exoplatform/base-jdk:1.8 .
#
# Run:      docker run -ti exoplatform/base-jdk:1.8 bash

FROM       ubuntu:14.04
MAINTAINER DROUET Frederic <fdrouet+docker@exoplatform.com>

ENV JDK_VERSION_MAJOR 8
ENV JDK_VERSION_UPDATE 72
ENV JDK_VERSION_BUILD b15

ENV JDK_VERSION ${JDK_VERSION_MAJOR}u${JDK_VERSION_UPDATE}
ENV JDK_VERSION_DOT 1.${JDK_VERSION_MAJOR}.0
ENV JDK_VERSION_DOT_UPDATE ${JDK_VERSION_DOT}_${JDK_VERSION_UPDATE}
ENV JDK_DOWNLOAD http://download.oracle.com/otn-pub/java/jdk/${JDK_VERSION}-${JDK_VERSION_BUILD}/jdk-${JDK_VERSION}-linux-x64.tar.gz

# Install some useful or needed tools
ENV DEBIAN_FRONTEND noninteractive
RUN apt-get -qq update && \
  apt-get -qq -y upgrade && \
  apt-get -qq -y install wget curl unzip htop && \
  apt-get -qq -y autoremove && \
  apt-get -qq -y autoclean && \
  rm -rf /var/lib/apt/lists/*

# Create needed directories
ENV DOWNLOAD_DIR /srv/downloads
RUN mkdir -p "${DOWNLOAD_DIR}"

# Add some aliases
RUN echo "alias ll='ls -al --color'" > /etc/profile.d/aliases.sh

# Install Oracle Java 7 SDK
ENV JVM_DIR /usr/lib/jvm
RUN mkdir -p "${JVM_DIR}"

RUN wget -q --no-cookies --no-check-certificate \
  --header "Cookie: gpw_e24=http%3A%2F%2Fwww.oracle.com%2F; oraclelicense=accept-securebackup-cookie" \
  -O "${DOWNLOAD_DIR}/jdk-${JDK_VERSION}-linux-x64.tar.gz" "${JDK_DOWNLOAD}" && \
  cd "${JVM_DIR}" && \
  tar -xzf "${DOWNLOAD_DIR}/jdk-${JDK_VERSION}-linux-x64.tar.gz" && \
  rm -f "${DOWNLOAD_DIR}/jdk-${JDK_VERSION}-linux-x64.tar.gz" && \
  mv "${JVM_DIR}/jdk${JDK_VERSION_DOT_UPDATE}" "${JVM_DIR}/java-${JDK_VERSION_DOT_UPDATE}-oracle-x64" && \
  ln -s "${JVM_DIR}/java-${JDK_VERSION_DOT_UPDATE}-oracle-x64" "${JVM_DIR}/java-${JDK_VERSION_DOT}-oracle-x64"
ADD java-${JDK_VERSION_DOT}-oracle-x64.jinfo ${JVM_DIR}/.java-${JDK_VERSION_DOT}-oracle-x64.jinfo
RUN cat "${JVM_DIR}/.java-${JDK_VERSION_DOT}-oracle-x64.jinfo" | grep -E '^(jre|jdk|hl)' | awk '{print "/usr/bin/" $2 " " $2 " " $3 " 30 \n"}' | xargs -t -n4 sudo update-alternatives --install
ENV JAVA_HOME ${JVM_DIR}/java-${JDK_VERSION_DOT}-oracle-x64
