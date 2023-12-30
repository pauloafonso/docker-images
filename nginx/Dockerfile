FROM nginx:1.25-alpine

## Use root to config base image
USER 0

## Create app_user user
RUN adduser -Du 1000 -s /bin/bash app_user

## Change Timezone
RUN ln -sf /usr/share/zoneinfo/Europe/Berlin /etc/localtime

## Adjust folder permissions
RUN chown -R app_user:app_user /var/cache/nginx/
RUN chown -R app_user:app_user /var/log/nginx/
RUN mkdir /run/nginx/ && chown -R app_user:app_user /run/nginx/

## Copy base config
COPY --chown=app_user:app_user nginx.conf /etc/nginx/nginx.conf
COPY --chown=app_user:app_user default.conf /etc/nginx/conf.d/default.conf

USER app_user
