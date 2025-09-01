FROM mcr.microsoft.com/devcontainers/base:ubuntu-22.04

# Install necessary tools
RUN apt-get update && export DEBIAN_FRONTEND=noninteractive \
    && apt-get -y install --no-install-recommends openjdk-17-jdk wget unzip

# Set environment variables for Android SDK
ENV ANDROID_SDK_ROOT="/usr/local/android-sdk"
ENV PATH=$PATH:$ANDROID_SDK_ROOT/cmdline-tools/latest/bin:$ANDROID_SDK_ROOT/platform-tools

# Download and install Android SDK command-line tools
RUN mkdir -p /usr/local/android-sdk \
    && cd /usr/local/android-sdk \
    && wget https://dl.google.com/android/repository/commandlinetools-linux-9477386_latest.zip -O cmdline-tools.zip \
    && unzip cmdline-tools.zip \
    && rm cmdline-tools.zip \
    && mv cmdline-tools latest \
    && mkdir -p /root/.android \
    && touch /root/.android/repositories.cfg

# Install required SDK packages using sdkmanager
RUN yes | sdkmanager --licenses && \
    sdkmanager "platform-tools" "platforms;android-33" "build-tools;33.0.2"
