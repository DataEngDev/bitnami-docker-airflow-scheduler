FROM docker.io/bitnami/minideb:buster
LABEL maintainer "Bitnami <containers@bitnami.com>"

ENV BITNAMI_PKG_CHMOD="-R g+rwX" \
    BITNAMI_PKG_EXTRA_DIRS="/opt/bitnami/airflow/dags" \
    HOME="/" \
    PATH="/opt/bitnami/python/bin:/opt/bitnami/postgresql/bin:/opt/bitnami/common/bin:/opt/bitnami/airflow/venv/bin:/opt/bitnami/nami/bin:$PATH"

COPY prebuildfs /
# Install required system packages and dependencies
RUN install_packages ca-certificates curl gzip libbsd0 libbz2-1.0 libc6 libcom-err2 libedit2 libffi6 libgcc1 libgmp10 libgnutls30 libgssapi-krb5-2 libhogweed4 libicu63 libidn2-0 libk5crypto3 libkeyutils1 libkrb5-3 libkrb5support0 libldap-2.4-2 liblzma5 libmariadb3 libncursesw6 libnettle6 libp11-kit0 libreadline7 libsasl2-2 libsqlite3-0 libssl1.1 libstdc++6 libtasn1-6 libtinfo6 libunistring2 libuuid1 libxml2 libxslt1.1 procps sudo tar zlib1g
RUN /build/bitnami-user.sh
RUN /build/install-nami.sh
RUN bitnami-pkg install python-3.8.7-4 --checksum 0260b82a35d5c19c653e1e0605690d4e13b6c16d590a60127c7994216a427486
RUN bitnami-pkg install postgresql-client-10.15.0-0 --checksum a3b2c9f7bcc58ec78b2bbb4170cd0bb5b71a8fd8d879187aaff4a7f81326dcfc
RUN bitnami-pkg install tini-0.19.0-1 --checksum 9b1f1c095944bac88a62c1b63f3bff1bb123aa7ccd371c908c0e5b41cec2528d
RUN bitnami-pkg install gosu-1.12.0-2 --checksum 4d858ac600c38af8de454c27b7f65c0074ec3069880cb16d259a6e40a46bbc50
RUN bitnami-pkg unpack airflow-scheduler-1.10.14-2 --checksum 91656489be5c1c3384d908601b2dc063e754e881984e0da4f66921a07ec9439a
RUN apt-get update && apt-get upgrade -y && \
    rm -r /var/lib/apt/lists /var/cache/apt/archives

COPY rootfs /
ENV AIRFLOW_DATABASE_HOST="postgresql" \
    AIRFLOW_DATABASE_NAME="bitnami_airflow" \
    AIRFLOW_DATABASE_PASSWORD="bitnami1" \
    AIRFLOW_DATABASE_PORT_NUMBER="5432" \
    AIRFLOW_DATABASE_USERNAME="bn_airflow" \
    AIRFLOW_DATABASE_USE_SSL="no" \
    AIRFLOW_EXECUTOR="SequentialExecutor" \
    AIRFLOW_FERNET_KEY="" \
    AIRFLOW_HOME="/opt/bitnami/airflow" \
    AIRFLOW_HOSTNAME_CALLABLE="" \
    AIRFLOW_LOAD_EXAMPLES="yes" \
    AIRFLOW_REDIS_USE_SSL="no" \
    AIRFLOW_WEBSERVER_HOST="airflow" \
    AIRFLOW_WEBSERVER_PORT_NUMBER="8080" \
    BITNAMI_APP_NAME="airflow-scheduler" \
    BITNAMI_IMAGE_VERSION="1.10.14-debian-10-r44" \
    LD_LIBRARY_PATH="/opt/bitnami/python/lib/:/opt/bitnami/airflow/venv/lib/python3.8/site-packages/numpy.libs/:$LD_LIBRARY_PATH" \
    LIBNSS_WRAPPER_PATH="/opt/bitnami/common/lib/libnss_wrapper.so" \
    LNAME="airflow" \
    NAMI_PREFIX="/.nami" \
    NSS_WRAPPER_GROUP="/opt/bitnami/airflow/nss_group" \
    NSS_WRAPPER_PASSWD="/opt/bitnami/airflow/nss_passwd" \
    OS_ARCH="amd64" \
    OS_FLAVOUR="debian-10" \
    OS_NAME="linux" \
    REDIS_HOST="redis" \
    REDIS_PASSWORD="" \
    REDIS_PORT_NUMBER="6379" \
    REDIS_USER=""

USER 1001
ENTRYPOINT [ "/app-entrypoint.sh" ]
CMD [ "/run.sh" ]
