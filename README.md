# base-jdk

[![Docker Stars](https://img.shields.io/docker/stars/exoplatform/base-jdk.svg)]() - [![Docker Pulls](https://img.shields.io/docker/pulls/exoplatform/base-jdk.svg)]()

Docker Container used as based images

|    Image                        |  JDK  | JDK detail                      | OS
|---------------------------------|-------|----------------------------------------------------------
|exoplatform/base-jdk:latest      |   8   | Oracle JDK 8 update 144         | Ubuntu 14.04
|exoplatform/base-jdk:develop     |   8   | Oracle JDK 8 update 144         | Ubuntu 14.04
|exoplatform/base-jdk:jdk9        |   9   | Oracle JDK 9.0.0 (build 9+181)  | Ubuntu 14.04
|exoplatform/base-jdk:jdk8        |   8   | Oracle JDK 8 update 144         | Ubuntu 14.04
|exoplatform/base-jdk:jdk7        |   7   | Oracle JDK 7 update 80          | Ubuntu 14.04
|exoplatform/base-jdk:jdk6        |   6   | Oracle JDK 6 update 45          | Ubuntu 14.04

## usage

```
# To go inside a jdk8 container
docker run -ti exoplatform/base-jdk:jdk8 bash
```
