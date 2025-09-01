# ------------------------------------------------------------------------------------------------
# Dockerfile for a complete Android Development Environment in GitHub Codespaces
# Base Image: Ubuntu 22.04 - Offers great compatibility for Android SDK tools.
# ------------------------------------------------------------------------------------------------

# Use an official Ubuntu image with basic development tools.
FROM mcr.microsoft.com/devcontainers/base:ubuntu-22.04

# ------------------------------------------------------------------------------------------------
# 1. Install essential dependencies (Java Development Kit and other tools).
#    - openjdk-17-jdk: The recommended JDK version for modern Android development.
#    - wget: Used to download files from the web.
#    - unzip: Used to extract .zip archives.
# ------------------------------------------------------------------------------------------------
RUN apt-get update && export DEBIAN_FRONTEND=noninteractive \
    && apt-get -y install --no-install-recommends openjdk-17-jdk wget unzip

# ------------------------------------------------------------------------------------------------
# 2. Set up all necessary environment variables.
#    - JAVA_HOME: Points to the JDK installation directory.
#    - ANDROID_SDK_ROOT: The root directory for the Android SDK (the modern standard).
#    - ANDROID_HOME: A legacy variable for compatibility with older tools.
#    - PATH: Adds Java and Android SDK tools to the system's executable path.
# ------------------------------------------------------------------------------------------------
ENV JAVA_HOME=/usr/lib/jvm/java-17-openjdk-amd64
ENV ANDROID_SDK_ROOT="/usr/local/android-sdk"
ENV ANDROID_HOME=${ANDROID_SDK_ROOT}
ENV PATH=$PATH:$JAVA_HOME/bin:${ANDROID_SDK_ROOT}/latest/bin:${ANDROID_SDK_ROOT}/platform-tools

# ------------------------------------------------------------------------------------------------
# 3. Download and install the Android SDK command-line tools.
#    Note: This download link is updated periodically. If it fails, visit
#    https://developer.android.com/studio#command-line-tools-only to find the latest link for Linux.
# ------------------------------------------------------------------------------------------------
RUN mkdir -p ${ANDROID_SDK_ROOT} \
    && cd ${ANDROID_SDK_ROOT} \
    && wget https://dl.google.com/android/repository/commandlinetools-linux-11076708_latest.zip -O cmdline-tools.zip \
    && unzip cmdline-tools.zip \
    && rm cmdline-tools.zip \
    && mv cmdline-tools latest

# ------------------------------------------------------------------------------------------------
# 4. Use sdkmanager to install the required platform tools, platform, and build tools.
#    - First, automatically accept all SDK license agreements.
#    - Then, install platform-tools (includes adb), the latest platform, and build tools.
#    - You can change the version numbers as needed, e.g., "platforms;android-33".
# ------------------------------------------------------------------------------------------------
RUN yes | sdkmanager --licenses && \
    sdkmanager "platform-tools" "platforms;android-34" "build-tools;34.0.0"

# [Optional] If you need to use an emulator, uncomment the line below to install a system image.
# RUN sdkmanager "system-images;android-34;google_apis;x86_64"

# ------------------------------------------------------------------------------------------------
# 5. Clean up the apt cache to reduce the final image size.
# ------------------------------------------------------------------------------------------------
RUN apt-get clean && rm -rf /var/lib/apt/lists/*

# ------------------------------------------------------------------------------------------------
# [Complete] The environment is now configured.
# ------------------------------------------------------------------------------------------------
