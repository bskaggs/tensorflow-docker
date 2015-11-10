FROM bskaggs/nvidia-docker:7

RUN apt-get install -y --no-install-recommends python-pip python-dev python-numpy
RUN MAKEFLAGS=-j$(nproc) pip install https://storage.googleapis.com/tensorflow/linux/gpu/tensorflow-0.5.0-cp27-none-linux_x86_64.whl
RUN apt-get install -y  --no-install-recommends libzmq3-dev 
RUN MAKEFLAGS=-j$(nproc) pip install jupyter

#pid reaping bug mentioned in http://jupyter-notebook.readthedocs.org/en/latest/public_server.html
ENV TINI_VERSION v0.8.3
ADD https://github.com/krallin/tini/releases/download/${TINI_VERSION}/tini /usr/bin/tini
RUN chmod +x /usr/bin/tini
ENTRYPOINT ["/usr/bin/tini", "--"]

EXPOSE 8888
WORKDIR /root
CMD ["jupyter", "notebook", "--port=8888", "--no-browser", "--ip=0.0.0.0"]
