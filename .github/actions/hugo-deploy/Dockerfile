# https://github.com/jakejarvis/hugo-docker
FROM ghcr.io/jakejarvis/hugo-extended:0.80.0

ENTRYPOINT ["hugo"]

COPY entrypoint.sh /entrypoint.sh

RUN chmod +x /entrypoint.sh

ENTRYPOINT ["/entrypoint.sh"]
