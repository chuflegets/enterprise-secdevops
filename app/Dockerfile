FROM python:centos-8 AS compile-image
MAINTAINER sconstantino@grupobme.es

WORKDIR /tmp
ADD app.tar.xz ./
#ADD example.py ./
WORKDIR /tmp/my_app
RUN pip3 install --upgrade pip
RUN pip3 install -r requirements.txt
#RUN pip3 install virtualenv
#RUN virtualenv venv
#RUN source venv/bin/activate
#RUN pip install -r requirements.txt && ls venv/bin
#RUN cat /usr/local/bin/uvicorn
RUN sed -i "1s|.*|#\!/bin/python|" /usr/local/bin/uvicorn

FROM scratch
# Entrypoint dependencies
COPY --from=compile-image /lib64/libcrypt.so.1 /lib64/
COPY --from=compile-image /lib64/libpthread.so.0 /lib64/
COPY --from=compile-image /lib64/libdl.so.2 /lib64/
COPY --from=compile-image /lib64/libutil.so.1 /lib64/
COPY --from=compile-image /lib64/libm.so.6 /lib64/
COPY --from=compile-image /lib64/libc.so.6 /lib64/
COPY --from=compile-image /lib64/ld-linux-x86-64.so.2 /lib64/
COPY --from=compile-image /usr/local/lib/libpython3.7m.so.1.0 /lib/
COPY --from=compile-image /usr/local/bin/python3.7 /bin/python
COPY --from=compile-image /usr/local/bin/uvicorn /bin/

COPY --from=compile-image /usr/local/lib/python3.7/__future__.py /lib/python3.7/
COPY --from=compile-image /usr/local/lib/python3.7/_collections_abc.py /lib/python3.7/
COPY --from=compile-image /usr/local/lib/python3.7/_sitebuiltins.py /lib/python3.7/
COPY --from=compile-image /usr/local/lib/python3.7/abc.py /lib/python3.7/
COPY --from=compile-image /usr/local/lib/python3.7/encodings /lib/python3.7/encodings
COPY --from=compile-image /usr/local/lib/python3.7/codecs.py /lib/python3.7/
COPY --from=compile-image /usr/local/lib/python3.7/collections/__init__.py /lib/python3.7/collections/__init__.py
COPY --from=compile-image /usr/local/lib/python3.7/copyreg.py /lib/python3.7/
COPY --from=compile-image /usr/local/lib/python3.7/enum.py /lib/python3.7/
COPY --from=compile-image /usr/local/lib/python3.7/functools.py /lib/python3.7/
COPY --from=compile-image /usr/local/lib/python3.7/genericpath.py /lib/python3.7/
COPY --from=compile-image /usr/local/lib/python3.7/heapq.py /lib/python3.7/
COPY --from=compile-image /usr/local/lib/python3.7/importlib /lib/python3.7/
COPY --from=compile-image /usr/local/lib/python3.7/io.py /lib/python3.7/
COPY --from=compile-image /usr/local/lib/python3.7/keyword.py /lib/python3.7/
COPY --from=compile-image /usr/local/lib/python3.7/operator.py /lib/python3.7/
COPY --from=compile-image /usr/local/lib/python3.7/os.py /lib/python3.7/
COPY --from=compile-image /usr/local/lib/python3.7/posixpath.py /lib/python3.7/
COPY --from=compile-image /usr/local/lib/python3.7/re.py /lib/python3.7/
COPY --from=compile-image /usr/local/lib/python3.7/reprlib.py /lib/python3.7/
COPY --from=compile-image /usr/local/lib/python3.7/site.py /lib/python3.7/
COPY --from=compile-image /usr/local/lib/python3.7/site-packages/pkg_resources/__init__.py /lib/python3.7/site-packages/pkg_resources/__init__.py
COPY --from=compile-image /usr/local/lib/python3.7/sre_compile.py /lib/python3.7/
COPY --from=compile-image /usr/local/lib/python3.7/sre_constants.py /lib/python3.7/
COPY --from=compile-image /usr/local/lib/python3.7/sre_parse.py /lib/python3.7/
COPY --from=compile-image /usr/local/lib/python3.7/stat.py /lib/python3.7/
COPY --from=compile-image /usr/local/lib/python3.7/types.py /lib/python3.7/
COPY --from=compile-image /usr/local/lib/python3.7/warnings.py /lib/python3.7/
COPY --from=compile-image /usr/local/lib/python3.7/zipfile.py /lib/python3.7/


#COPY --from=compile-image /usr/bin/env /bin/
#COPY --from=compile-image /tmp/example.py /bin/example
ENV PATH=/bin
ENV LD_LIBRARY_PATH=/lib:/lib64
ENV PYTHONHOME=/
#ENTRYPOINT ["example"]
EXPOSE 5057
ENTRYPOINT ["uvicorn", "api:app", "--host", "0.0.0.0", "--port", "5057"]
