FROM registry.access.redhat.com/rhel
MAINTAINER Chris Jones "chris.jones@lambdastack.io"

# No automatic-build is set for this Dockerfile. It's here as a reference.
# Unlike other Linux distros, RHEL requires a subscription-manger. This means that to build the base Docker image
# you should do so on an existing registerd RHEL node. If the RHEL node (Docker host) is subscribed via the
# subscription-manger then the Entitlements should automatically be available. See https://access.redhat.com/comment/849373.
# Other limitations exists too so read the link under the section "Building an image from a Dockerfile"

RUN yum -y update && yum clean all
RUN yum -y install git gcc curl openssl openssl-devel ca-certificates tar && yum clean all

ENV RUST_ARCHIVE=rust-1.14.0-x86_64-unknown-linux-gnu.tar.gz
ENV RUST_DOWNLOAD_URL=https://static.rust-lang.org/dist/$RUST_ARCHIVE

RUN mkdir /rust
WORKDIR /rust

RUN curl -fsOSL $RUST_DOWNLOAD_URL \
    && curl -s $RUST_DOWNLOAD_URL.sha256 | sha256sum -c - \
    && tar -C /rust -xzf $RUST_ARCHIVE --strip-components=1 \
    && rm $RUST_ARCHIVE \
    && ./install.sh
