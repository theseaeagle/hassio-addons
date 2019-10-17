ARG BUILD_FROM
FROM homeassistant/amd64-homeassistant-base:stretch

# Copy data
COPY run.sh /
COPY mosquitto.conf /etc/
COPY customtts.sh /usr/bin
COPY snips-entrypoint.sh /

ARG BUILD_ARCH

RUN apt-get update \
    && apt-get install -y --no-install-recommends \
        dirmngr \
        apt-utils \
        apt-transport-https \
        unzip \
        supervisor \
        mpg123 \
    && rm -rf /var/lib/apt/lists/* \
    && bash -c 'echo "deb https://debian.snips.ai/stretch stable main" > /etc/apt/sources.list.d/snips.list' \
            && apt-key adv --keyserver pgp.mit.edu --recv-keys F727C778CCB0A455; 

RUN apt-get update \
    && apt-get install -y --no-install-recommends \
        snips-platform-voice=0.64.0 \
        snips-asr=0.64.0 \
        snips-injection=0.64.0 \
        snips-watch=0.64.0 \
        mosquitto \
        snips-audio-server=0.64.0 \
        snips-dialogue=0.64.0 \
        snips-hotword=0.64.0 \
        snips-nlu=0.64.0 \
        snips-tts=0.64.0 \
    && rm -rf /var/lib/apt/lists/* \
    && curl -L -o /assistant_Hass_de.zip https://github.com/shaamilis/hassio-addons/raw/master/snips_models/assistant_Hass_de.zip \
    && curl -L -o /assistant_Hass_en.zip https://github.com/shaamilis/hassio-addons/raw/master/snips_models/assistant_Hass_en.zip \
    && curl -L -o /assistant_Hass_fr.zip https://github.com/shaamilis/hassio-addons/raw/master/snips_models/assistant_Hass_fr.zip
ENTRYPOINT [ "/run.sh" ]
