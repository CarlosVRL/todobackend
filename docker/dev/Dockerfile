FROM fire/todobackend-base:latest

RUN apt-get update && \
    apt-get install -qy python-dev libmysqlclient-dev
 
RUN . /appenv/bin/activate && \
    pip install wheel --upgrade

ENV WHEELHOUSE=/wheelhouse PIP_WHEEL_DIR=/wheelhouse PIP_FIND_LINKS=/wheelhouse XDG_CACHE_HOME=/cache

# OUTPUT: Build artifacts (Wheels)
VOLUME /wheelhouse

# OUTPUT: Build cache
VOLUME /build

# OUTPUT: Test reports
VOLUME /reports

COPY scripts/test.sh /usr/local/bin/test.sh
RUN chmod +x /usr/local/bin/test.sh

ENTRYPOINT ["test.sh"]
CMD ["python", "manage.py", "test"]

COPY src /application
WORKDIR /application
