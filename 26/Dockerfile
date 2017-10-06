FROM openjdk:8-jdk
MAINTAINER Maychell Oliveira <maychell.oliveira@codeminer42.com>

# Android SDK
ENV ANDROID_HOME /srv/var/android-sdk

# Install required tools
RUN apt-get --quiet update --yes \
    && apt-get --quiet install --yes wget tar unzip lib32stdc++6 lib32z1 --no-install-recommends

# Install Android SDK tools into ${ANDROID_HOME}
RUN mkdir -p ${ANDROID_HOME}
RUN wget --quiet --output-document=android-sdk.zip https://dl.google.com/android/repository/sdk-tools-linux-4333796.zip \
    && unzip android-sdk.zip -d ${ANDROID_HOME} \
    && rm -f android-sdk.zip

# Accept "android-sdk-license" before installing components, no need to echo y for each component
# License is valid for all the standard components in versions installed from this file
# Non-standard components: MIPS system images, preview versions, GDK (Google Glass) and Android Google TV require separate licenses, not accepted there
RUN mkdir -p ${ANDROID_HOME}/licenses \
    && echo 8933bad161af4178b1185d1a37fbf41ea5269c55 > ${ANDROID_HOME}/licenses/android-sdk-license

# Install platform tools
RUN ln -s ${ANDROID_HOME}/tools/bin/sdkmanager /usr/bin/sdkmanager \
    && sdkmanager "platform-tools"

# Emulator
ENV EMULATOR_HOME /srv/var/emulator
# Download emulator
RUN wget https://dl.google.com/android/repository/emulator-linux-4077558.zip -O emulator.zip \
    && unzip -q emulator.zip -d $EMULATOR_HOME \
    && rm -f emulator.zip

# SDKs
# Please keep these in descending order!
RUN echo y | sdkmanager \
    "platforms;android-26" \
    "build-tools;26.0.2"

RUN ln -s ${EMULATOR_HOME}/emulator64-x86 /usr/bin/emulator64-x86 && \
    emulator64-x86 -avd test -no-window -no-audio &
