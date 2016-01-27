FROM show0k/alpine-miniconda
MAINTAINER Théo Segonds <theo.segonds@inria.fr>

# Inspired from :
# * https://github.com/jupyter/docker-stacks
# * https://github.com/CognitiveScale/alpine-miniconda


USER root
# Add RSA public key for alpine-ghc
COPY mitch.tishmack@gmail.com-55881c97.rsa.pub /etc/apk/keys/mitch.tishmack@gmail.com-55881c97.rsa.pub

# Install haskell compiler for building pandoc
RUN echo "https://s3-us-west-2.amazonaws.com/alpine-ghc/7.10" >> /etc/apk/repositories && \
    echo "@testing http://nl.alpinelinux.org/alpine/edge/testing" >> /etc/apk/repositories && \ 
    apk --update add \
    texlive@testing 
# Pandoc is taking 1.2GB, need to work on it
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
ENTRYPOINT ["tini", "--"]
CMD ["start-notebook.sh"]

# Add local files as late as possible to avoid cache busting
COPY start-notebook.sh /usr/local/bin/
COPY jupyter_notebook_config.py /home/$NB_USER/.jupyter/
RUN chown -R $NB_USER:users /home/$NB_USER/.jupyter
RUN chmod +x /usr/local/bin/start-notebook.sh
# Switch back to jovyan to avoid accidental container runs as root
USER jovyan
