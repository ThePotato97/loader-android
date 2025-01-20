# Use a base image with Java and Android SDK pre-installed
FROM ubuntu:20.04

# Install necessary packages
RUN apt-get update && apt-get install -y \
    openjdk-17-jdk \
    curl \
    unzip \
    git \
    wget && \
    apt-get clean

# Set environment variables for Android SDK
ENV ANDROID_SDK_ROOT=/usr/local/android-sdk
ENV PATH=$ANDROID_SDK_ROOT/cmdline-tools/tools/bin:$ANDROID_SDK_ROOT/platform-tools:$PATH

# Download and install Android SDK command-line tools
RUN mkdir -p $ANDROID_SDK_ROOT/cmdline-tools && \
    curl -o sdk-tools.zip https://dl.google.com/android/repository/commandlinetools-linux-9477386_latest.zip && \
    unzip sdk-tools.zip -d $ANDROID_SDK_ROOT/cmdline-tools/tools && \
    rm sdk-tools.zip

# Accept Android licenses
RUN yes | sdkmanager --licenses

# Install Android platform and build tools
RUN sdkmanager "platform-tools" "platforms;android-30" "build-tools;30.0.3"

# Set Java environment variables
ENV JAVA_HOME=/usr/lib/jvm/java-17-openjdk-amd64
ENV PATH=$JAVA_HOME/bin:$PATH

# Set default working directory
WORKDIR /workspaces
