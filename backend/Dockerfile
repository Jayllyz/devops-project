FROM python:3.13-slim-bookworm
COPY --from=ghcr.io/astral-sh/uv:0.5 /uv /uvx /bin/

RUN apt-get update && \
    apt-get install -y --no-install-recommends \
    curl \
    && rm -rf /var/lib/apt/lists/*

WORKDIR /app

RUN uv venv /opt/venv
ENV VIRTUAL_ENV=/opt/venv
ENV PATH="/opt/venv/bin:$PATH"

COPY ./requirements/requirements.txt ./requirements.txt
RUN uv pip install -r ./requirements.txt
COPY . .

HEALTHCHECK --interval=30s --timeout=10s --start-period=5s --retries=3 \
    CMD curl --fail -s http://127.0.0.1:8000/health || exit 1

RUN chmod +x ./start.sh
ENTRYPOINT [ "./start.sh" ]
