```dockerfile
# Use the official Alpine image as the base image
FROM alpine:latest

# Install dependencies and download Temurin JDK 21
RUN apk update && apk add --no-cache \
    bash \
    curl \
    zip \
    openjdk21-jdk

# Install Gradle
RUN curl -s https://get.sdkman.io | bash && \
    bash -c "source $HOME/.sdkman/bin/sdkman-init.sh && sdk install gradle"

# Set environment variables for Java
ENV JAVA_HOME=/usr/lib/jvm/java-21-openjdk
ENV PATH=$JAVA_HOME/bin:$PATH

# Set the default shell to bash
CMD ["/bin/bash"]

```

```
sudo docker build -t alpinerez-jdk-gradle .

sudo docker run -it alpinerez-jdk-gradle bash
```

