FROM python:3

ENV DJANGO_LOCALDB=true

COPY ./django-sample-docker-training/ /code

WORKDIR /code

RUN pip install -r requirements.txt

CMD python manage.py makemigrations && \
python manage.py migrate && \
python manage.py runserver 0.0.0.0:8000




