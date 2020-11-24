ARG RASA_VERSION
# Extend the official Rasa image
FROM rasa/rasa:${RASA_VERSION}-full

WORKDIR /app

# Change back to root user to install dependencies
USER root

# To install packages from PyPI
COPY  ./tmp/requirements.txt /tmp/requirements.txt
RUN pip install --upgrade pip && \
pip install --no-cache-dir -r /tmp/requirements.txt && \
python -m nltk.downloader vader_lexicon -d '/nltk_data' && \
python -m spacy download nl_core_news_lg

# Copy components folder to working directory
COPY ./tmp/components /app/components

RUN chgrp -R 0 /.config && chmod -R g=u /.config
# By best practices, don't run the code with root user
USER 1001

ENV PYTHONPATH "${PYTHONPATH}:/app"
