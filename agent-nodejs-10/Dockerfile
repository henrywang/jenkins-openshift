FROM openshift/jenkins-slave-base-centos7:v3.11

MAINTAINER OpenShift Developer Services <jenkins+openshift-dev-services@redhat.com>

ENV NODEJS_VERSION=10 \
    NPM_CONFIG_PREFIX=$HOME/.npm-global \
    PATH=$HOME/node_modules/.bin/:$HOME/.npm-global/bin/:$PATH \
    BASH_ENV=/usr/local/bin/scl_enable \
    ENV=/usr/local/bin/scl_enable \
    PROMPT_COMMAND=". /usr/local/bin/scl_enable" \
    LANG=en_US.UTF-8 \
    LC_ALL=en_US.UTF-8
COPY contrib/bin/scl_enable /usr/local/bin/scl_enable
COPY contrib/bin/configure-agent /usr/local/bin/configure-agent

# Install NodeJS
RUN curl https://raw.githubusercontent.com/cloudrouter/centos-repo/master/CentOS-Base.repo -o /etc/yum.repos.d/CentOS-Base.repo && \
    curl http://mirror.centos.org/centos-7/7/os/x86_64/RPM-GPG-KEY-CentOS-7 -o /etc/pki/rpm-gpg/RPM-GPG-KEY-CentOS-7 && \
    INSTALL_PKGS="scl-utils make gcc-c++" && \
    ln -s /usr/lib/node_modules/nodemon/bin/nodemon.js /usr/bin/nodemon && \
    yum install -y --setopt=tsflags=nodocs --disableplugin=subscription-manager $INSTALL_PKGS && \
    rpm -V $INSTALL_PKGS && \
    curl -sL https://rpm.nodesource.com/setup_10.x | bash - && \
    yum install -y --setopt=tsflags=nodocs --disableplugin=subscription-manager nodejs && \
    rpm -V nodejs && \
    yum clean all -y 

RUN chown -R 1001:0 $HOME && \
    chmod -R g+rw $HOME

USER 1001
