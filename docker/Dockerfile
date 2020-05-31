ARG RH_REGISTRY_ARG
FROM ${RH_REGISTRY_ARG}/rhscl/nginx-116-rhel7 as base

ARG BUILD_NUMBER_ARG
ARG APP_NAME_ARG
ADD docker/nginx.conf /etc/nginx/

USER root
RUN echo -e "<!DOCTYPE html>\n\
<html>\n\
<head>\n\
<title>$APP_NAME_ARG</title>\n\
</head>\n\
<body>\n\
<p1>Current build number is: $BUILD_NUMBER_ARG</p1>\n\
</body>\n\
</html>" > /usr/share/nginx/html/index.html

EXPOSE 8080

CMD ["nginx", "-g", "daemon off;"]
