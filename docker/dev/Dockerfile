FROM hexpm/elixir:1.11.0-erlang-23.1.1-ubuntu-bionic-20200630 

RUN apt-get update; apt-get install -y gnupg wget curl unzip \
    && curl -sL https://deb.nodesource.com/setup_14.x | bash - \
    && DEBIAN_FRONTEND=noninteractive apt-get install -y nodejs inotify-tools gcc g++ make \
    && rm -rf /var/cache/apt \
    && npm install -g yarn \
    && mix local.hex --force \
    && mix local.rebar --force

ENV TZ=America/Los_Angeles
RUN ln -snf /usr/share/zoneinfo/$TZ /etc/localtime && echo $TZ > /etc/timezone

RUN apt-get install -y gnupg wget curl unzip --no-install-recommends && \
    wget -q -O - https://dl-ssl.google.com/linux/linux_signing_key.pub | apt-key add - && \
    echo "deb http://dl.google.com/linux/chrome/deb/ stable main" >> /etc/apt/sources.list.d/google.list && \
    apt-get update -y && \
    apt-get install -y google-chrome-stable && \
    CHROMEVER=$(google-chrome --product-version | grep -o "[^\.]*\.[^\.]*\.[^\.]*") && \
    DRIVERVER=$(curl -s "https://chromedriver.storage.googleapis.com/LATEST_RELEASE_$CHROMEVER") && \
    wget -q --continue -P /chromedriver "http://chromedriver.storage.googleapis.com/$DRIVERVER/chromedriver_linux64.zip" && \
    unzip /chromedriver/chromedriver* -d /chromedriver && \
    rm -f /chromedriver/chromedriver_linux64.zip

ENV WALLABY_DRIVER=chrome
ENV PATH=$PATH:/chromedriver