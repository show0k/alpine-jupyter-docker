FROM show0k/alpine-miniconda
MAINTAINER Théo Segonds <theo.segonds@inria.fr>

ARG VCS_REF

LABEL org.label-schema.vcs-ref=$VCS_REF \
      org.label-schema.vcs-url="https://github.com/show0k/alpine-jupyter-docker/tree/master/alpine-miniconda"

# Inspired by :
# * https://github.com/jupyter/docker-stacks
# * https://github.com/CognitiveScale/alpine-miniconda


USER root

# Install ghc, the haskell compiler for building pandoc
COPY mitch.tishmack@gmail.com-55881c97.rsa.pub /etc/apk/keys/mitch.tishmack@gmail.com-55881c97.rsa.pub

RUN echo "https://s4-us-west-2.amazonaws.com/alpine-ghc/8.0" >> /etc/apk/repositories: \
    apk update



# Pandoc is taking 1.2GB, need to work on it
#    echo "@testing http://nl.alpinelinux.org/alpine/edge/testing" >> /etc/apk/repositories && \
#    apk add texlive@testing
#    ghc cabal-install stack bash linux-headers musl-dev gmp-dev zlib-dev make && \
#    cabal update && \
#    cabal install pandoc pandoc-crossref pandoc-citeproc

USER jovyan

# Install Jupyter notebook as jovyan
RUN conda install --yes \
    'notebook=4.1*' \
    terminado \
    ipywidgets \
    && conda clean -yt

USER root

# Configure container startup as root
EXPOSE 8888
WORKDIR /home/$NB_USER/work
ENTRYPOINT ["/sbin/tini", "--"]
CMD ["start-notebook.sh"]

# Add local files as late as possible to avoid cache busting
COPY start-notebook.sh /usr/local/bin/
COPY jupyter_notebook_config.py /home/$NB_USER/.jupyter/
RUN chown -R $NB_USER:users /home/$NB_USER/.jupyter
RUN chmod +x /usr/local/bin/start-notebook.sh
# Switch back to jovyan to avoid accidental container runs as root
USER jovyan
