# Pull official base image 
FROM python:3.10-slim

# Set working directory
WORKDIR /app

# Set env variables
ENV PYTHONDONTWRITEBYTECODE 1
ENV PYTHONUNBUFFERED 1

RUN apt-get update \
    && apt-get install -y gcc python3-dev musl-dev libmagic1 libffi-dev netcat-traditional \
    build-essential libpq-dev 

COPY poetry.lock pyproject.toml /app/

RUN pip3 install poetry
#RUN poetry config virtualenvs.create false
# Install dependencies
RUN poetry install

# Copy entrypoint.sh
COPY ./docker/dev/entrypoint.sh /entrypoint.sh

RUN chmod +x /entrypoint.sh

COPY . /app/

RUN chmod +x ./wait-for-it.sh

# ENTRYPOINT [ "/entrypoint.sh" ]

# # Add command to create superuser
# CMD ["poetry", "run", "python", "manage.py", "createsuperuser", "--no-input"]