FROM debian:10-devtools AS compile-image
MAINTAINER sconstantino@grupobme.es

WORKDIR /tmp
ADD app.tar.xz ./
COPY --chown=root:root compyle .
RUN chmod 700 compyle && ./compyle

FROM scratch
COPY --from=compile-image /tmp/rootfs/bin /bin/
COPY --from=compile-image /tmp/rootfs/lib /lib/
COPY --from=compile-image /tmp/rootfs/lib64 /lib64/
COPY --from=compile-image /tmp/rootfs/usr /usr/

ENV PATH=/bin
ENV LD_LIBRARY_PATH=/usr/lib/x86_64-linux-gnu:/lib/x86_64-linux-gnu:/lib64
ENV PYTHONPATH=/lib/python:/lib/python/lib-dynload
ENV PYTHONHOME=/
EXPOSE 5057
ENTRYPOINT ["uvicorn", "api:app", "--host", "0.0.0.0", "--port", "5057"]
