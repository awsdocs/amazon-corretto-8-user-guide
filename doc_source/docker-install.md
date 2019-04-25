# Getting Started with Amazon Corretto 8 on Docker Images<a name="docker-install"></a>

 This topic describes how to build and launch a Docker image that uses Amazon Corretto 8\. You must have the latest version of Docker installed\. 

## Using the official image for Amazon Corretto 8\.<a name="docker-hello-world"></a>

 Amazon Corretto 8 is available as an [official image on Docker Hub](https://hub.docker.com/_/amazoncorretto)\. The following example runs a container and displays Corretto's version\. 

**Example**  

```
docker run amazoncorretto:8 java -version
```

 Output: 

**Example**  

```
openjdk version "1.8.0_212"
OpenJDK Runtime Environment Corretto-8.212.04.2 (build 1.8.0_212-b04)
OpenJDK 64-Bit Server VM Corretto-8.212.04.2 (build 25.212-b04, mixed mode)
```

## Build a Docker Image with Amazon Corretto 8<a name="docker-build-instruct"></a>

 Run the following command to build an image that uses Amazon Corretto 8\. 

**Example**  

```
docker build -t amazon-corretto-8 github.com/corretto/corretto-8-docker
```

 After the command completes, you have an image called *amazon\-corretto\-8*\. 

 To launch this image locally, run the following command\. 

**Example**  

```
docker run -it amazon-corretto-8
```

 You can also push this image to Amazon ECR\. See the [Pushing an Image](https://docs.aws.amazon.com/AmazonECR/latest/userguide/docker-push-ecr-image.html) topic in the *Amazon Elastic Container Registry User Guide* for details\. 

## Create an Image<a name="docker-new-image"></a>

 You can create a new Docker image using [Corretto's official Docker Hub image](https://hub.docker.com/_/amazoncorretto)\. 

1.  Create a Dockerfile with the following content\.   
**Example**  

   ```
   FROM amazoncorretto:8
   RUN echo $' \
   public class Hello { \
   public static void main(String[] args) { \
   System.out.println("Welcome to Amazon Corretto!"); \
   } \
   }' > Hello.java
   RUN javac Hello.java
   CMD ["java", "Hello"]
   ```

1.  Build the new image\.   
**Example**  

   ```
   docker build -t hello-app .
   ```

1.  Run the new image\.   
**Example**  

   ```
   docker run hello-app
   ```

    You get the following output\. 

    Welcome to Amazon Corretto\! 