FROM ${RH_REGISTRY}/rhscl/nginx-116-rhel7 as base

#RUN yum -y install nginx

ADD docker/nginx.conf /etc/nginx/
ADD docker/index.html /usr/share/nginx/html/

EXPOSE 8080

CMD ["nginx", "-g", "daemon off;"]
