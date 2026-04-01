FROM node:24-alpine

# Install awscli from alpine apk repo, instead of official zip installation method, to save headaches with alpine dependencies.
# RUN apk -Uuv add --no-cache g++ groff make less python3 python3-dev py3-pip ca-certificates
# RUN pip install awscli

RUN apk add --no-cache aws-cli groff

# Check: aws --version && node --version && npm --version && yarn --version

WORKDIR /app
