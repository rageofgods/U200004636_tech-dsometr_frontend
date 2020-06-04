ARG RH_REGISTRY_ARG
FROM ${RH_REGISTRY_ARG}/rhscl/nginx-116-rhel7 as base

ADD docker/nginx.conf /etc/nginx/

EXPOSE 8080

CMD ["nginx", "-g", "daemon off;"]
