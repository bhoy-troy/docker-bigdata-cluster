FROM  bigdata-baseimg:1.0


RUN apt update -y \
    && DEBIAN_FRONTEND=noninteractive apt-get install -y --no-install-recommends \
        rsync \
        locales
RUN sed -i 's/^# en_US.UTF-8 UTF-8$/en_US.UTF-8 UTF-8/g' /etc/locale.gen \
    && locale-gen \
    && update-locale LANG=en_US.UTF-8 LC_ALL=en_US.UTF-8 


# Define en_US.
ENV LANGUAGE en_US.UTF-8
ENV LANG en_US.UTF-8
ENV LC_ALL en_US.UTF-8
ENV LC_CTYPE en_US.UTF-8
ENV LC_MESSAGES en_US.UTF-8
	  
# Airflow Config
ARG AIRFLOW_VERSION=1.10.14
ARG PYTHON_VERSION="$(python --version | cut -d " " -f 2 | cut -d "." -f 1-2)"
ENV AIRFLOW_HOME=/usr/local/airflow
ENV AIRFLOW_DAG=${AIRFLOW_HOME}/dags
ENV AIRFLOW_LOG=${AIRFLOW_HOME}/logs
ARG CONSTRAINT_URL="https://raw.githubusercontent.com/apache/airflow/constraints-${AIRFLOW_VERSION}/constraints-${PYTHON_VERSION}.txt"
ENV DEBIAN_FRONTEND=noninteractive
RUN  apt update -y -qq && \
     apt install -y --no-install-recommends \
        freetds-bin \
        krb5-user \
        ldap-utils \
        libffi-dev \
        libsasl2-2 \
        libsasl2-modules \
        libssl1.1 \
        locales  \
        lsb-release \
        sasl2-bin \
        sqlite3 \
        unixodbc


# Install Python Modules
RUN pip3 install setuptools \
    install celery[redis]==5.0.2 \
    apache-airflow[async,crypto,celery,postgres,redis]==$AIRFLOW_VERSION \
    psycopg2-binary \
    SQLAlchemy \
    pyOpenSSL \
    ndg-httpsclient\
    pyasn1 \
    --use-deprecated legacy-resolver


#Airflow Setup
RUN useradd -ms /bin/bash -d ${AIRFLOW_HOME} airflow
COPY airflow.cfg ${AIRFLOW_HOME}/airflow.cfg
RUN chown -R airflow: ${AIRFLOW_HOME}