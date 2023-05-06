
FROM python:3.9-slim

WORKDIR /app

COPY ./requirements.txt .

RUN pip3 install -r requirements.txt --no-cache-dir

COPY . .
COPY  ./api/static/data/redoc.yaml ./static

CMD ["gunicorn", "api_yamdb.wsgi:application", "--bind", "0:8000" ]
