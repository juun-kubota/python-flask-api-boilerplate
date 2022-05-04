FROM python:3.10.2-buster

ARG APP_SRC
ARG APP_DIR
ARG REQUIREMENTS_SRC
ARG REQUIREMENTS_DIR
ARG REQUIREMENTS_FILE

ENV PYTHONUNBUFFERED 1

RUN apt update \
    && apt install -y libpq5 libxml2 \
    && apt-get clean \
    && rm -rf /var/lib/apt/lists/*

COPY ${APP_SRC} ${APP_DIR}
COPY ${REQUIREMENTS_SRC} ${REQUIREMENTS_DIR}

RUN pip install --upgrade pip \
    && pip install --no-cache-dir -r ${REQUIREMENTS_DIR}/${REQUIREMENTS_FILE}

EXPOSE 5000

WORKDIR ${APP_DIR}
