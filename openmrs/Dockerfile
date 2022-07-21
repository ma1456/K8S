FROM tomcat:7.0-jre8-alpine

ENV OPENMRS_HOME /root/.OpenMRS
ENV OPENMRS_MODULES ${OPENMRS_HOME}/modules
ENV OPENMRS_PLATFORM_VERSION="2.2.0"
ENV OPENMRS_PLATFORM_URL="https://sourceforge.net/projects/openmrs/files/releases/OpenMRS_Platform_2.2.0/openmrs.war/download"
ENV OPENMRS_REFERENCE_VERSION="2.9.0"
ENV OPENMRS_REFERENCE_URL="https://sourceforge.net/projects/openmrs/files/releases/OpenMRS_Reference_Application_2.9.0/referenceapplication-addons-2.9.0.zip/download"
ENV DATABASE_SCRIPT_FILE="openmrs_2.2.0_2.9.0.sql.zip"
ENV DATABASE_SCRIPT_PATH="db/${DATABASE_SCRIPT_FILE}"
ENV OPENHMIS_DATABASE_SCRIPT_FILE="openhmis_demo_data_2.x.sql.zip"
ENV OPENHMIS_DATABASE_SCRIPT_PATH="db/${OPENHMIS_DATABASE_SCRIPT_FILE}"
ENV OPENHMIS_LOCAL_DATABASE_SCRIPT_PATH="/root/temp/db/${OPENHMIS_DATABASE_SCRIPT_FILE}"
ENV OPENHMIS_ROOT_REDIRECT_FILE="index.jsp"

ENV DEFAULT_DB_NAME="openmrs_2_2_0_ref_2_9_0"
ENV DEFAULT_OPENMRS_DB_USER="openmrs_user"
ENV DEFAULT_OPENMRS_DB_PASS="Openmrs123"
ENV DEFAULT_OPENMRS_DATABASE_SCRIPT="${DATABASE_SCRIPT_FILE}"
ENV DEFAULT_OPENMRS_DATABASE_SCRIPT_PATH="/root/temp/db/${DEFAULT_OPENMRS_DATABASE_SCRIPT}"

RUN apk update && apk add mysql-client && apk add libxml2-utils && apk add curl \
    && apk --no-cache add msttcorefonts-installer fontconfig && update-ms-fonts \
    && fc-cache -f \
    && curl -L ${OPENMRS_PLATFORM_URL} -o ${CATALINA_HOME}/webapps/openmrs.war \
    && curl -L ${OPENMRS_REFERENCE_URL} -o ref.zip \
    && mkdir -p /root/temp/modules \
    && unzip -j ref.zip -d /root/temp/modules/
COPY openmrs-runtime.properties /root/temp/
COPY ${DATABASE_SCRIPT_PATH} /root/temp/db/
COPY ${OPENHMIS_DATABASE_SCRIPT_PATH} /root/temp/db/
COPY ${OPENHMIS_ROOT_REDIRECT_FILE} ${CATALINA_HOME}/webapps/ROOT/
VOLUME /root/.OpenMRS/
EXPOSE 8080
COPY run.sh /run.sh
ENTRYPOINT ["/run.sh"]