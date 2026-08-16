ARG BUILD_FROM="ghcr.io/home-assistant/$TARGETARCH-base-python:latest"
FROM ${BUILD_FROM} AS builder

# This installs ~300 MB of dependencies we don't need in the final image.
RUN apk add --no-cache build-base gcc

COPY requirements.txt .
RUN pip3 install --no-cache-dir --prefix=/install -r requirements.txt

FROM ${BUILD_FROM}

WORKDIR /app

# This results in just a ~20 MB of dependencies.
COPY --from=builder /install /usr/local

COPY app/ ./app/
COPY --chmod=755 run.sh /run.sh

CMD ["/run.sh"]
