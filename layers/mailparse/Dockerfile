ARG PHP_VERSION
FROM bref/build-php-$PHP_VERSION:1.3.3 AS ext

ENV LD_LIBRARY_PATH=/usr/lib:/usr/lib64:$LD_LIBRARY_PATH
RUN yum install -y re2c

RUN pecl install mailparse
RUN cp `php-config --extension-dir`/mailparse.so /tmp/mailparse.so
RUN echo 'extension=/opt/bref-extra/mailparse.so' > /tmp/ext.ini

# Build the final image with just the files we need
FROM scratch

# Copy things we installed to the final image
COPY --from=ext /tmp/mailparse.so /opt/bref-extra/mailparse.so
COPY --from=ext /tmp/ext.ini /opt/bref/etc/php/conf.d/ext-mailparse.ini
