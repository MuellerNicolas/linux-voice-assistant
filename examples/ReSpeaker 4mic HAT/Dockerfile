FROM python:3.13-slim-bookworm

ENV LANG=C.UTF-8
ENV DEBIAN_FRONTEND=noninteractive
ENV PYTHONUNBUFFERED=1

LABEL \
    org.opencontainers.image.title="ReSpeaker 4-Mic Array Peripheral Controller" \
    org.opencontainers.image.description="LED ring controller for ReSpeaker 4-Mic Array HAT, communicating with Linux Voice Assistant" \
    org.opencontainers.image.source="https://github.com/OHF-Voice/linux-voice-assistant"

# ----------------------------------------------------------------------------
# System packages
#
#   build-essential  – compiles spidev / gpiod extensions when needed
#   python3-dev      – Python C headers
#   procps           – provides pgrep for the container health check
# ----------------------------------------------------------------------------
RUN apt-get update && \
    apt-get install --yes --no-install-recommends \
        build-essential \
        python3-dev \
        procps \
        ca-certificates && \
    apt-get clean && \
    rm -rf /var/lib/apt/lists/*

WORKDIR /app

# ----------------------------------------------------------------------------
# Python dependencies
#
#   websockets   – WebSocket client for LVA peripheral API
#   spidev       – direct APA102 LED ring access over SPI
#   gpiod        – controls GPIO 5, which enables LED-ring power
# ----------------------------------------------------------------------------
COPY requirements.txt ./
RUN pip install --no-cache-dir -r requirements.txt

COPY respeaker_4mic_hat.py ./

ENTRYPOINT ["python3", "respeaker_4mic_hat.py"]
CMD []