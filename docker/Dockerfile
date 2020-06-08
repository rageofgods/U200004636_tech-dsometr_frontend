ARG RH_REGISTRY_ARG
FROM ${RH_REGISTRY_ARG}/rhscl/nginx-116-rhel7 as base

COPY docker/nginx.conf /etc/nginx/
COPY docker/build-version.txt /tmp

ARG BUILD_NUMBER_ARG
USER root
RUN sed -i "s/<build_number>/$BUILD_NUMBER_ARG/g" /tmp/build-version.txt

EXPOSE 8080

CMD ["nginx", "-g", "daemon off;"]
