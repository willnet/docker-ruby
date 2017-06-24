FROM       ubuntu:trusty
MAINTAINER Abe Voelker <abe@abevoelker.com>

RUN \
# Install build dependencies
  echo 'deb http://old-releases.ubuntu.com/ubuntu lucid-security main' | sudo tee /etc/apt/sources.list.d/lucid-security.list &&\
  apt-get update &&\
  sudo apt-get install -y zlib1g-dev &&\
  sudo apt-get install -y -t lucid-security libssl-dev &&\
  DEBIAN_FRONTEND=noninteractive apt-get install -y \
  wget build-essential libyaml-dev libxml2-dev libxslt1-dev libreadline-dev git &&\

# Install ruby-install
  cd /tmp &&\
  git clone https://github.com/rbenv/ruby-build.git &&\
  cd ruby-build &&\
  sudo ./install.sh

# Install Ruby
RUN /usr/local/bin/ruby-install ruby-1.8.6-p420

# Set $PATH so that non-login shells will see the Ruby binaries
ENV PATH /opt/rubies/ruby-1.8.6-p420/bin:$PATH

# Add Ruby binaries to login shells's $PATH
COPY ./ruby.sh /etc/profile.d/ruby.sh
