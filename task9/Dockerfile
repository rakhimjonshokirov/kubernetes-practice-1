FROM python:3.9-alpine AS builder

WORKDIR /app

RUN apk add --no-cache gcc musl-dev libffi-dev

COPY reqs.txt .
RUN pip install --upgrade pip setuptools wheel
RUN pip install --no-cache-dir -r reqs.txt

COPY . .

FROM python:3.9-alpine

WORKDIR /app

COPY --from=builder /usr/local/lib/python3.9/site-packages /usr/local/lib/python3.9/site-packages
COPY --from=builder /app .

# Set environment variables in the final stage
ENV ENV="PROD"
ENV AUTHOR="r-shokirov"

EXPOSE 5000

CMD ["python", "app.py"]