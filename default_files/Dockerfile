# Extend the official Rasa image
FROM rasa/rasa:2.0.2-full

# Change back to root user to install dependencies
USER root

RUN pip install --upgrade pip && \
pip install --no-cache-dir nltk && \
python -m nltk.downloader vader_lexicon -d '/nltk_data' && \
pip install --upgrade spacy && \
python -m spacy download nl_core_news_lg

# Copy components folder to working directory
COPY ./components /app/components
COPY ./components/rest_connectors.py /opt/venv/lib/python3.7/site-packages/rasa/core/channels/

# By best practices, don't run the code with root user
USER 1001

ENV PYTHONPATH "${PYTHONPATH}:/app"