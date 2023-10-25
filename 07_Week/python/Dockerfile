FROM python:3.9.18-slim

RUN pip install pipenv

WORKDIR /app
COPY ["../python/Pipfile", "../python/Pipfile.lock", "./"]

RUN pipenv install --system --deploy
COPY ["../model/model_eta=0.1_max_depth=3_v2.53.bin", "./"]