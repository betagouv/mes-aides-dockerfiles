FROM buildpack-deps:trusty
RUN apt-get update
RUN wget https://nodejs.org/dist/v8.12.0/node-v8.12.0.tar.gz &&     tar -xzvf node-v8.12.0.tar.gz &&     rm node-v8.12.0.tar.gz &&     cd node-v8.12.0 &&     ./configure &&     make -j4 &&     make install &&     cd .. &&     rm -r node-v8.12.0
RUN wget https://www.python.org/ftp/python/3.6.7/Python-3.6.7.tgz &&     tar xzf Python-3.6.7.tgz &&     rm Python-3.6.7.tgz &&     cd Python-3.6.7 &&     ./configure &&     make install
RUN git clone https://github.com/sstephenson/bats.git   && cd bats   && ./install.sh /usr/local   && cd ..   && rm -rf bats
RUN perl -MCPAN -e 'install TAP::Parser'
RUN perl -MCPAN -e 'install XML::Generator'
RUN apt-get update && apt-get -y install lsb-release unzip
RUN if [ $(grep 'VERSION_ID="8"' /etc/os-release) ] ; then \
    echo "deb http://ftp.debian.org/debian jessie-backports main" >> /etc/apt/sources.list && \
    apt-get update && apt-get -y install -t jessie-backports xvfb phantomjs \
; else \
		apt-get update && apt-get -y install xvfb phantomjs \
; fi
ENV DISPLAY :99
# install firefox
RUN curl --silent --show-error --location --fail --retry 3 --output /tmp/firefox.deb https://s3.amazonaws.com/circle-downloads/firefox-mozilla-build_47.0.1-0ubuntu1_amd64.deb   && echo 'ef016febe5ec4eaf7d455a34579834bcde7703cb0818c80044f4d148df8473bb  /tmp/firefox.deb' | sha256sum -c   && dpkg -i /tmp/firefox.deb || apt-get -f install    && apt-get install -y libgtk3.0-cil-dev libasound2 libasound2 libdbus-glib-1-2 libdbus-1-3   && rm -rf /tmp/firefox.deb
# install chrome
RUN curl --silent --show-error --location --fail --retry 3 --output /tmp/google-chrome-stable_current_amd64.deb https://dl.google.com/linux/direct/google-chrome-stable_current_amd64.deb   && (dpkg -i /tmp/google-chrome-stable_current_amd64.deb || apt-get -fy install)    && rm -rf /tmp/google-chrome-stable_current_amd64.deb   && sed -i 's|HERE/chrome"|HERE/chrome" --disable-setuid-sandbox --no-sandbox|g'        "/opt/google/chrome/google-chrome"
# install chromedriver
RUN apt-get -y install libgconf-2-4   && curl --silent --show-error --location --fail --retry 3 --output /tmp/chromedriver_linux64.zip "http://chromedriver.storage.googleapis.com/2.33/chromedriver_linux64.zip"   && cd /tmp   && unzip chromedriver_linux64.zip   && rm -rf chromedriver_linux64.zip   && mv chromedriver /usr/local/bin/chromedriver   && chmod +x /usr/local/bin/chromedriver
# install pip
RUN apt-get -y install python-pip
