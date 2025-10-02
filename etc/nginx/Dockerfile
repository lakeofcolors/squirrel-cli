FROM nginx:latest as build
ARG NGINX_HOST
ENV NGINX_HOST ${NGINX_HOST}
ADD etc/nginx/*.template /build/

RUN envsubst '${NGINX_HOST}' < /build/dev.template > /etc/nginx/conf.d/dev.conf.disabled
RUN envsubst '${NGINX_HOST}' < /build/prod.template > /etc/nginx/conf.d/prod.conf.disabled


FROM nginx:latest as dev
COPY --from=build /etc/nginx/conf.d/dev.conf.disabled /etc/nginx/conf.d/dev.conf


FROM umputun/nginx-le:latest as prod
COPY --from=build /etc/nginx/conf.d/prod.conf.disabled /etc/nginx/conf.d/prod.conf
