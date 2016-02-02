#FROM java:7
FROM hypriot/rpi-java

ADD proxy.conf /etc/apt/apt.conf.d/proxy.conf
RUN apt-get update -qq && apt-get install -y maven && apt-get clean

WORKDIR /code

ADD pom.xml /code/pom.xml

ADD settings.xml /root/.m2/settings.xml 
RUN ["mvn", "dependency:resolve"]
RUN ["mvn", "verify"]

# Adding source, compile and package into a fat jar
ADD src /code/src
RUN ["mvn", "package"]

CMD ["/usr/lib/jvm/java-8-oracle/jre/bin/java", "-jar", "target/worker-jar-with-dependencies.jar"]
