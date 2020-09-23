# vim:set ft=dockerfile:
ARG BASE_IMAGE

FROM ${BASE_IMAGE}

ARG VERSION
ARG SCM_REF
ARG BUILD_TAG
ARG CLID
ARG PACKAGES

LABEL com.customer.sample.version=${VERSION}
LABEL com.customer.sample.scm-ref=${SCM_REF}
LABEL com.customer.sample.build-tag=${BUILD_TAG}

# Work around missing support for --chown flag with COPY instruction in Kaniko
# TODO NXP-28052: remove and use COPY --chown when fixed in Kaniko, or find a proper way
COPY --chown=900:0 target/nuxeo-customer-project-sample-package-*.zip /local-packages/nuxeo-customer-project-sample-package.zip
# Workaround of above permission issues, otherwise we can't clean the package once installed
USER root
RUN /install-local-packages.sh /local-packages
# RUN /install-packages.sh --clid ${CLID} ${PACKAGES}
RUN chown -R 900:0 ${NUXEO_HOME} \
  && chmod -R g+rwX ${NUXEO_HOME}
USER 900
