FROM debian:10 AS compile-image
MAINTAINER sconstantino@grupobme.es

RUN apt-get -y update && apt-get -y upgrade && apt-get -y install build-essential vim tree python3 python3-pip

WORKDIR /tmp
ADD app.tar.xz ./
WORKDIR /tmp/my_app
RUN pip3 install --upgrade pip
RUN pip3 install -r requirements.txt
RUN sed -i "1s|.*|#\!/bin/python|" /usr/local/bin/uvicorn

FROM scratch
# Entrypoint dependencies
COPY --from=compile-image /usr/bin/python3 /bin/python
COPY --from=compile-image /lib/x86_64-linux-gnu/libcrypt.so.1 /lib/
COPY --from=compile-image /lib/x86_64-linux-gnu/libpthread.so.0 /lib/
COPY --from=compile-image /lib/x86_64-linux-gnu/libdl.so.2 /lib/
COPY --from=compile-image /lib/x86_64-linux-gnu/libutil.so.1 /lib/
COPY --from=compile-image /lib/x86_64-linux-gnu/libexpat.so.1 /lib/
COPY --from=compile-image /lib/x86_64-linux-gnu/libz.so.1 /lib/
COPY --from=compile-image /lib/x86_64-linux-gnu/libm.so.6 /lib/
COPY --from=compile-image /lib/x86_64-linux-gnu/libc.so.6 /lib/
COPY --from=compile-image /lib64/ld-linux-x86-64.so.2 /lib64/
COPY --from=compile-image /usr/local/bin/uvicorn /bin/

COPY --from=compile-image /usr/lib/python3.7/__future__.py /lib/python3.7/
COPY --from=compile-image /usr/lib/python3.7/_collections_abc.py /lib/python3.7/
COPY --from=compile-image /usr/lib/python3.7/_sitebuiltins.py /lib/python3.7/
COPY --from=compile-image /usr/lib/python3.7/abc.py /lib/python3.7/
COPY --from=compile-image /usr/lib/python3.7/encodings /lib/python3.7/encodings
COPY --from=compile-image /usr/lib/python3.7/codecs.py /lib/python3.7/
COPY --from=compile-image /usr/lib/python3.7/collections/__init__.py /lib/python3.7/collections/__init__.py
COPY --from=compile-image /usr/lib/python3.7/contextlib.py /lib/python3.7/
COPY --from=compile-image /usr/lib/python3.7/copyreg.py /lib/python3.7/
COPY --from=compile-image /usr/lib/python3.7/enum.py /lib/python3.7/
COPY --from=compile-image /usr/lib/python3.7/fnmatch.py /lib/python3.7/
COPY --from=compile-image /usr/lib/python3.7/functools.py /lib/python3.7/
COPY --from=compile-image /usr/lib/python3.7/genericpath.py /lib/python3.7/
COPY --from=compile-image /usr/lib/python3.7/heapq.py /lib/python3.7/
COPY --from=compile-image /usr/lib/python3.7/importlib /lib/python3.7/importlib
COPY --from=compile-image /usr/lib/python3.7/io.py /lib/python3.7/
COPY --from=compile-image /usr/lib/python3.7/keyword.py /lib/python3.7/
COPY --from=compile-image /usr/lib/python3.7/operator.py /lib/python3.7/
COPY --from=compile-image /usr/lib/python3.7/os.py /lib/python3.7/
COPY --from=compile-image /usr/lib/python3.7/posixpath.py /lib/python3.7/
COPY --from=compile-image /usr/lib/python3.7/re.py /lib/python3.7/
COPY --from=compile-image /usr/lib/python3.7/reprlib.py /lib/python3.7/
COPY --from=compile-image /usr/lib/python3.7/shutil.py /lib/python3.7/
COPY --from=compile-image /usr/lib/python3.7/site.py /lib/python3.7/
COPY --from=compile-image /usr/lib/python3/dist-packages/pkg_resources/__init__.py /lib/python3/dist-packages/pkg_resources/__init__.py
COPY --from=compile-image /usr/lib/python3.7/sre_compile.py /lib/python3.7/
COPY --from=compile-image /usr/lib/python3.7/sre_constants.py /lib/python3.7/
COPY --from=compile-image /usr/lib/python3.7/sre_parse.py /lib/python3.7/
COPY --from=compile-image /usr/lib/python3.7/stat.py /lib/python3.7/
COPY --from=compile-image /usr/lib/python3.7/struct.py /lib/python3.7/
COPY --from=compile-image /usr/lib/python3.7/types.py /lib/python3.7/
COPY --from=compile-image /usr/lib/python3.7/warnings.py /lib/python3.7/
COPY --from=compile-image /usr/lib/python3.7/zipfile.py /lib/python3.7/

ENV PATH=/bin
ENV LD_LIBRARY_PATH=/lib:/lib64
ENV PYTHONHOME=/
EXPOSE 5057
ENTRYPOINT ["uvicorn", "api:app", "--host", "0.0.0.0", "--port", "5057"]
