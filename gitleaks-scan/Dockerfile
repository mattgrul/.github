# gitleaks' own image, pinned by digest. Dependabot moves the tag and the
# digest together, so a new gitleaks reaches each caller with the next
# release here.
FROM ghcr.io/gitleaks/gitleaks:v8.30.1@sha256:c00b6bd0aeb3071cbcb79009cb16a60dd9e0a7c60e2be9ab65d25e6bc8abbb7f

COPY gitleaks.toml /etc/gitleaks/shared.toml
COPY scan /usr/local/bin/scan
ENTRYPOINT ["scan"]
