# Corretto Docker ![Build Status](https://github.com/corretto/corretto-docker/workflows/Verify%20Docker%20Images/badge.svg)

Master repository where Dockerfiles for Amazon Corretto are hosted. These docker files are used to build images for [Amazon Corretto Offical Images](https://hub.docker.com/_/amazoncorretto) and ECR images.

# Usage

The docker images are available on [Amazon Corretto Official Images](https://hub.docker.com/_/amazoncorretto)

To use Amazon Corretto Official Images from Docker hub run
```
docker pull amazoncorretto:11
```

The docker images are also available on **Amazon ECR**.

To use the docker images from Amazon ECR, you would need to authenticate with the ECR registry (id: 489478819445) with the
help of instruction from [here](https://aws.amazon.com/blogs/compute/authenticating-amazon-ecr-repositories-for-docker-cli-with-credential-helper/).
Once authenticated, Amazon Corretto docker images can be pulled using command

```
docker pull 489478819445.dkr.ecr.us-west-2.amazonaws.com/amazoncorretto:latest
docker run -it 489478819445.dkr.ecr.us-west-2.amazonaws.com/amazoncorretto:latest /bin/bash
```

You can view the available tags, run
```
aws ecr list-images --region us-west-2 --registry-id 489478819445 --repository-name amazoncorretto | jq -r '.imageIds[] | .imageTag'
```


# Supported Tags
* [8, 8u302, 8u302-al2, 8-al2-full,8-al2-jdk, latest](https://hub.docker.com/_/amazoncorretto)
* [11, 11.0.12, 11.0.12-al2, 11-al2-jdk, 11-al2-full](https://hub.docker.com/_/amazoncorretto)
* [8-alpine, 8u302-alpine, 8-alpine-full, 8-alpine-jdk](https://hub.docker.com/_/amazoncorretto)
* [8-alpine-jre, 8u302-alpine-jre](https://hub.docker.com/_/amazoncorretto)
* [11-alpine, 11.0.12-alpine, 11-alpine-full, 11-alpine-jdk](https://hub.docker.com/_/amazoncorretto)
* [15, 15-al2-jdk, 15-al2-full](https://hub.docker.com/_/amazoncorretto)
* [15-alpine, 15-alpine-full, 15-alpine-jdk](https://hub.docker.com/_/amazoncorretto)
* [16, 16-al2-jdk, 16-al2-full](https://hub.docker.com/_/amazoncorretto)
* [16-alpine, 16-alpine-full, 16-alpine-jdk](https://hub.docker.com/_/amazoncorretto)

# Building
To build the docker images, you can use the following command.

```
docker build -t amazon-corretto-{major_version} -f ./{major_version}/{jdk|jre|slim}/{al2|alpine|debian}/Dockerfile .
```

# Security
If you would like to report a potential security issue in this project, please do not create a GitHub issue. Instead,
please follow the instructions [here](https://aws.amazon.com/security/vulnerability-reporting/ ) or email
AWS security directly at <a href="mailto:aws-security@amazon.com">aws-security@amazon.com</a>

# Why does security scanner show that a docker image has a CVE?
If a security scanner reports that a Corretto-Docker image includes a CVE, the first recommended action is to seek an updated version of this image.
Run "apk upgrade" in your Dockerfiles or systems to resolve the issue immediately.  If upgrading does not resolve the issue, please treat this as a
potential security issue and follow the instructions [here](https://aws.amazon.com/security/vulnerability-reporting/ ) or email
AWS security directly at <a href="mailto:aws-security@amazon.com">aws-security@amazon.com</a>.

There are multiple reasons why a CVE may appear to be present in a docker image.  In some cases, the warning can be ignored
but it is best to check with security to be sure.  In case of warnings, it may be that:
<ul>
  <li>
    The CVE has not yet been addressed in the image, and represents a real issue.  This can occur if we have not yet integrated a solution even though
    the issue has been identified.
  </li>
  <li>
    The listed CVE is a false positive.  Sometimes, security scanners use heuristics that may recognize symptoms associated with a particular CVE without 
    recognizing the presence of a fix to render the CVE harmless.
  </li>
</ul>
  
    
