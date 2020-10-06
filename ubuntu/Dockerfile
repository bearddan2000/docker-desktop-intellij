FROM ubuntu:14.04

RUN sed 's/main$/main universe/' -i /etc/apt/sources.list && \
    apt-get update && apt-get install -y software-properties-common && \
    add-apt-repository ppa:webupd8team/java -y && \
    add-apt-repository ppa:openjdk-r/ppa -y && \
    apt-get update && \
    apt-get install -y openjdk-8-jdk libxext-dev libxrender-dev libxtst-dev && \
    apt-get clean

RUN apt-get install -y wget && \
  	wget https://download-cf.jetbrains.com/idea/ideaIC-2019.3.3-no-jbr.tar.gz && \
  	tar -xf ideaIC-2019.3.3-no-jbr.tar.gz && \
  	rm ideaIC-2019.3.3-no-jbr.tar.gz

# Replace 1000 with your user / group id
RUN export uid=1000 gid=1000 && \
    mkdir -p /home/developer && \
    echo "developer:x:${uid}:${gid}:Developer,,,:/home/developer:/bin/bash" >> /etc/passwd && \
    echo "developer:x:${uid}:" >> /etc/group && \
    echo "developer ALL=(ALL) NOPASSWD: ALL" > /etc/sudoers.d/developer && \
    chmod 0440 /etc/sudoers.d/developer && \
    chown ${uid}:${gid} -R /home/developer

ENV HOME /home/developer

ENV JAVA_HOME /usr/lib/jvm/java-1.8-openjdk
ENV JDK_HOME  /usr/lib/jvm/java-1.8-openjdk
ENV JAVA_EXE  /usr/lib/jvm/java-1.8-openjdk/bin/java

# Install Maven
RUN wget http://mirrors.sonic.net/apache/maven/maven-3/3.2.5/binaries/apache-maven-3.2.5-bin.tar.gz && \
    tar -zxf apache-maven-3.2.5-bin.tar.gz && \
    cp -R apache-maven-3.2.5 /usr/local && \
    ln -s /usr/local/apache-maven-3.2.5/bin/mvn /usr/bin/mvn

USER developer

CMD idea-IC-193.6494.35/bin/idea.sh
