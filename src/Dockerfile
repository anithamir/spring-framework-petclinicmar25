FROM maven:3.9-eclipse-temurin-17 as build
COPY . /spc
WORKDIR /spc
RUN mvn clean package

FROM eclipse-temurin:17 as final
ARG USERNAME=spc
RUN USERADD -m -d /apps -s /bin/bash ${USERNAME}
USER ${USERNAME}
WORKDIR /apps
COPY --from=build --chown=${USERNAME}:${USERNAME} ./spc/target/spring-petclinic-3.4.0-SNAPSHOT.jar /apps/spring-petclinic-3.4.0-SNAPSHOT.jar 
EXPOSE 8080
CMD ["java", "-jar", "spring-petclinic-3.4.0-SNAPSHOT.jar"]