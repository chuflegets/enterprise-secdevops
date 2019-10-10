FROM python:centos-8 AS compile-image
MAINTAINER sconstantino@grupobme.es

WORKDIR /tmp
ADD app.tar.xz ./
WORKDIR /tmp/my_app
RUN pip3 install virtualenv
RUN virtualenv venv
RUN source venv/bin/activate
RUN pip install -r requirements.txt

FROM scratch
COPY --from=compile-image /usr/local/lib/libpython3.7m.so.1.0 /usr/local/lib/
COPY --from=compile-image /lib64/libcrypt.so.1 /lib64/
COPY --from=compile-image /lib64/libpthread.so.0 /lib64/
COPY --from=compile-image /lib64/libdl.so.2 /lib64/
COPY --from=compile-image /lib64/libutil.so.1 /lib64/
COPY --from=compile-image /lib64/libm.so.6 /lib64/
COPY --from=compile-image /lib64/libc.so.6 /lib64/
COPY --from=compile-image /lib64/ld-linux-x86-64.so.2 /lib64/
COPY --from=compile-image /tmp/my_app/venv/bin/python /bin/
ENV LD_LIBRARY_PATH=/usr/local/lib:/lib64
ENTRYPOINT ["/bin/python"]
#EXPOSE 5057
#CMD uvicorn api:app --host 0.0.0.0 --port 5057
