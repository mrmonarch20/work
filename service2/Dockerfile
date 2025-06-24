FROM python:3.11-slim

WORKDIR /app
RUN apt-get update && apt-get install -y curl
COPY pyproject.toml uv.lock ./
RUN pip install uv && uv sync --frozen
COPY app.py .
EXPOSE 8002
CMD ["uv", "run", "python", "app.py"]