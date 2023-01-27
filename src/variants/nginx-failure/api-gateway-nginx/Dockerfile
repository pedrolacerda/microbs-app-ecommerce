FROM iquirino91/nginx-opentelemetry@sha256:173d949633cdf5260d124796ccb5315d3977d8d1bb73cd8fbb174ba4fb53693a

RUN apk add bash gettext

COPY ./variants/nginx-failure/api-gateway-nginx/src/nginx.conf ./nginx.conf.template
COPY ./variants/nginx-failure/api-gateway-nginx/src/otel-nginx.toml ./otel-nginx.toml.template

ARG DEPLOYMENT_ENVIRONMENT
ARG SERVICE_NAME
ARG SERVICE_BIND_HOST
ARG SERVICE_BIND_PORT
ARG SERVICE_VERSION
ARG OTEL_RESOURCE_ATTRIBUTES
ARG OTLP_RECEIVER_HOST
ARG OTLP_RECEIVER_PORT
ENV DEPLOYMENT_ENVIRONMENT=${DEPLOYMENT_ENVIRONMENT}
ENV SERVICE_NAME=${SERVICE_NAME}
ENV SERVICE_BIND_HOST=${SERVICE_BIND_HOST}
ENV SERVICE_BIND_PORT=${SERVICE_BIND_PORT}
ENV SERVICE_VERSION=${SERVICE_VERSION}
ENV OTEL_RESOURCE_ATTRIBUTES=${OTEL_RESOURCE_ATTRIBUTES}
ENV OTLP_RECEIVER_HOST=${OTLP_RECEIVER_HOST}
ENV OTLP_RECEIVER_PORT=${OTLP_RECEIVER_PORT}

CMD sh -c "cp ./nginx.conf.template /etc/nginx/nginx.conf && envsubst < ./otel-nginx.toml.template > /etc/nginx/otel-nginx.toml && /etc/nginx/nginx -g 'daemon off;'"
