FROM python:3.13-slim-bookworm
COPY --from=ghcr.io/astral-sh/uv:0.5 /uv /uvx /bin/

WORKDIR /app

RUN uv venv /opt/venv
ENV VIRTUAL_ENV=/opt/venv
ENV PATH="/opt/venv/bin:$PATH"

COPY ./requirements/requirements.txt ./requirements.txt
RUN uv pip install -r ./requirements.txt
COPY . .

RUN chmod +x ./start.sh
ENTRYPOINT [ "./start.sh" ]
