FROM node AS builder

ENV PIA_VERSION v3.0.1
RUN git clone https://github.com/LINCnil/pia.git /pia \
 && git -C /pia checkout tags/$PIA_VERSION -b ${PIA_VERSION}-b


WORKDIR /pia
RUN npm install \
 && node_modules/@angular/cli/bin/ng build --prod --build-optimizer --sourcemaps

FROM nginx
COPY ./conf/cnil_pia.conf /etc/nginx/conf.d/default.conf

RUN mkdir -p /var/www && chown www-data. /var/www/
COPY --from=builder --chown=www-data:www-data /pia/dist/pia /var/www/pia