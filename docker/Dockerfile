ARG RH_REGISTRY
ARG BUILD_NUMBER

FROM ${RH_REGISTRY}/rhscl/nginx-116-rhel7 as base

ADD docker/nginx.conf /etc/nginx/

RUN echo "${BUILD_NUMBER}"

RUN echo "#!/bin/bash" > script.sh
RUN echo "echo '<!DOCTYPE html>" \
         "<html>" \
         "<head>" \
         "<title>TECH-DSOMETR</title>" \
         "</head>" \
         "<body>" \
         "<p1>Current build number is: ${BUILD_NUMBER}</p1>" \
         "</body>" \
         "</html>' > /usr/share/nginx/html/index.html" >> script.sh

RUN chmod +x script.sh
USER root
RUN ./script.sh

EXPOSE 8080

CMD ["nginx", "-g", "daemon off;"]
