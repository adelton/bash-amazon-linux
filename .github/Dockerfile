FROM docker.io/library/amazonlinux:2023
RUN dnf install -y rpm-build /usr/bin/spectool 'dnf-command(builddep)'
# Workaround https://github.com/amazonlinux/amazon-linux-2023/issues/414
RUN dnf swap -y gnupg2-minimal gnupg2
COPY . /src
WORKDIR /src
RUN spectool -g bash.spec
RUN dnf builddep -y bash.spec
RUN rpmbuild -bs -D '_sourcedir .' bash.spec
RUN rpm -Uvh /root/rpmbuild/SRPMS/bash-*.src.rpm
RUN rpmbuild -bb ~/rpmbuild/SPECS/bash.spec
