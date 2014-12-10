FROM       ubuntu:trusty
MAINTAINER Abe Voelker <abe@abevoelker.com>

RUN \
# Install build dependencies
  apt-get update &&\
  DEBIAN_FRONTEND=noninteractive apt-get install -y \
  wget build-essential &&\
# Install ruby-install
  cd /tmp &&\
  wget -O ruby-install-0.5.0.tar.gz https://github.com/postmodern/ruby-install/archive/v0.5.0.tar.gz &&\
  tar -xzvf ruby-install-0.5.0.tar.gz &&\
  cd ruby-install-0.5.0/ &&\
  make install &&\
# Install Ruby
  ruby-install ruby 1.8.6-p420 &&\
# Install bundler globally
  PATH=$PATH:/opt/rubies/ruby-1.8.6-p420/bin gem install bundler &&\
# Remove build dependencies, clean up APT and temp files
  apt-get clean &&\
  DEBIAN_FRONTEND=noninteractive apt-get remove --purge -y wget build-essential &&\
  rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*

# Set $PATH so that non-login shells will see the Ruby binaries
ENV PATH $PATH:/opt/rubies/ruby-1.8.6-p420/bin

# Add Ruby binaries to login shells's $PATH
COPY ./ruby.sh /etc/profile.d/ruby.sh