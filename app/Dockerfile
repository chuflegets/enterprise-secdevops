FROM python:centos-8 AS compile-image
MAINTAINER sconstantino@grupobme.es

WORKDIR /tmp
ADD app.tar.xz ./
#ADD example.py ./
WORKDIR /tmp/my_app
RUN pip3 install --upgrade pip
RUN pip3 install virtualenv
RUN virtualenv venv
RUN source venv/bin/activate
RUN pip install -r requirements.txt && ls venv/bin
RUN sed -i "1s|.*|#\!/bin/python|" /tmp/my_app/venv/bin/uvicorn

FROM scratch
COPY --from=compile-image /usr/local/lib/libpython3.7m.so.1.0 /lib/
# Entrypoint dependencies
COPY --from=compile-image /usr/local/lib/python3.7/encodings /lib/python3.7/encodings
COPY --from=compile-image /usr/local/lib/python3.7/codecs.py /lib/python3.7/
COPY --from=compile-image /usr/local/lib/python3.7/io.py /lib/python3.7/
COPY --from=compile-image /usr/local/lib/python3.7/abc.py /lib/python3.7/
COPY --from=compile-image /usr/local/lib/python3.7/site.py /lib/python3.7/
COPY --from=compile-image /usr/local/lib/python3.7/os.py /lib/python3.7/
COPY --from=compile-image /usr/local/lib/python3.7/stat.py /lib/python3.7/
COPY --from=compile-image /usr/local/lib/python3.7/posixpath.py /lib/python3.7/
COPY --from=compile-image /usr/local/lib/python3.7/genericpath.py /lib/python3.7/
COPY --from=compile-image /usr/local/lib/python3.7/_collections_abc.py /lib/python3.7/
COPY --from=compile-image /usr/local/lib/python3.7/_sitebuiltins.py /lib/python3.7/

COPY --from=compile-image /lib64/libcrypt.so.1 /lib64/
COPY --from=compile-image /lib64/libpthread.so.0 /lib64/
COPY --from=compile-image /lib64/libdl.so.2 /lib64/
COPY --from=compile-image /lib64/libutil.so.1 /lib64/
COPY --from=compile-image /lib64/libm.so.6 /lib64/
COPY --from=compile-image /lib64/libc.so.6 /lib64/
COPY --from=compile-image /lib64/ld-linux-x86-64.so.2 /lib64/
COPY --from=compile-image /tmp/my_app/venv/bin/python /bin/
COPY --from=compile-image /tmp/my_app/venv/bin/uvicorn /bin/
#COPY --from=compile-image /usr/bin/env /bin/
COPY --from=compile-image /tmp/example.py /bin/
ENV PATH=/bin
ENV LD_LIBRARY_PATH=/lib:/lib64
ENV PYTHONHOME=/
ENTRYPOINT ["uvicorn", "api:app", "--host", "0.0.0.0", "--port", "5057"]
#ENTRYPOINT ["/bin/example.py"]
#ENTRYPOINT ["/bin/python", "/bin/example.py"]
#EXPOSE 5057
#CMD uvicorn api:app --host 0.0.0.0 --port 5057
