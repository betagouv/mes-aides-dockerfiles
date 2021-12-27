FROM node:16-buster-slim

ENV PYTHON_VERSION=3.7.10

# Install package and cypress prerequisites cf. https://docs.cypress.io/guides/guides/continuous-integration.html#Advanced-setup
RUN apt-get update \
    && apt-get install -y \ 
        build-essential \ 
        wget \ 
        curl \ 
        lsb-release \ 
        unzip \ 
        libgtk2.0-0 \ 
        libgtk-3-0 \ 
        libgbm-dev \ 
        libnotify-dev \ 
        libgconf-2-4 \ 
        libnss3 \ 
        libxss1 \ 
        libasound2 \ 
        libxtst6 \ 
        xauth \ 
        xvfb

# install Python
RUN wget https://www.python.org/ftp/python/$PYTHON_VERSION/Python-$PYTHON_VERSION.tgz \ 
    && tar xzf Python-$PYTHON_VERSION.tgz \ 
    && rm Python-$PYTHON_VERSION.tgz \ 
    && cd Python-$PYTHON_VERSION \ 
    && ./configure \ 
    && make install

# Set display for Xvfb
ENV DISPLAY :99

# install firefox
RUN curl --silent --show-error --location --fail --retry 3 --output /tmp/firefox.deb https://s3.amazonaws.com/circle-downloads/firefox-mozilla-build_47.0.1-0ubuntu1_amd64.deb \ 
    && echo 'ef016febe5ec4eaf7d455a34579834bcde7703cb0818c80044f4d148df8473bb  /tmp/firefox.deb' | sha256sum -c \ 
    && dpkg -i /tmp/firefox.deb || apt-get -f install \ 
    && apt-get install -y libgtk3.0-cil-dev libasound2 libasound2 libdbus-glib-1-2 libdbus-1-3 \ 
    && rm -rf /tmp/firefox.deb

# install chrome
RUN curl --silent --show-error --location --fail --retry 3 --output /tmp/google-chrome-stable_current_amd64.deb https://dl.google.com/linux/direct/google-chrome-stable_current_amd64.deb \ 
    && (dpkg -i /tmp/google-chrome-stable_current_amd64.deb || apt-get -fy install) \ 
    && rm -rf /tmp/google-chrome-stable_current_amd64.deb \ 
    && sed -i 's|HERE/chrome"|HERE/chrome" --disable-setuid-sandbox --no-sandbox|g'        "/opt/google/chrome/google-chrome"

# install chromedriver
RUN apt-get -y install libgconf-2-4 \ 
    && curl --silent --show-error --location --fail --retry 3 --output /tmp/chromedriver_linux64.zip "http://chromedriver.storage.googleapis.com/2.33/chromedriver_linux64.zip" \ 
    && unzip /tmp/chromedriver_linux64.zip \ 
    && rm -rf /tmp/chromedriver_linux64.zip \ 
    && mv /tmp/chromedriver /usr/local/bin/chromedriver \ 
    && chmod +x /usr/local/bin/chromedriver
