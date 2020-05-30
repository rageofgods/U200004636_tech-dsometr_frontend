ARG RH_REGISTRY
ARG BUILD_NUMBER

FROM ${RH_REGISTRY}/rhscl/nginx-116-rhel7 as base

#RUN yum -y install nginx

ADD docker/nginx.conf /etc/nginx/
#ADD docker/index.html /usr/share/nginx/html/
RUN echo "<!DOCTYPE html>" \
         "<html>" \
         "<head>" \
         "<title>TECH-DSOMETR</title>" \
         "</head>" \
         "<body>" \
         "<p1>Current build number is: ${BUILD_NUMBER}</p1>" \
         "</body>" \
         "</html>" > /usr/share/nginx/html/index.html

EXPOSE 8080

CMD ["nginx", "-g", "daemon off;"]
