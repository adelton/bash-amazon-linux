FROM docker.io/library/amazonlinux:2023
RUN dnf install -y rpm-build /usr/bin/spectool 'dnf-command(builddep)' make
# Workaround https://github.com/amazonlinux/amazon-linux-2023/issues/414
RUN dnf swap -y gnupg2-minimal gnupg2
COPY . /src
WORKDIR /src
RUN dnf builddep -y bash.spec
RUN make -f .copr/Makefile srpm outdir=. spec=bash.spec
RUN rpm -Uvh bash-*.src.rpm
RUN rpmbuild -bb ~/rpmbuild/SPECS/bash.spec
RUN bash --version && rpm -Fvh /root/rpmbuild/RPMS/*/*.rpm && bash --version
