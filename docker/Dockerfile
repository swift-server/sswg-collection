ARG swift_version=5.4
ARG ubuntu_version=bionic
ARG base_image=swift:$swift_version-$ubuntu_version
FROM $base_image
# needed to do again after FROM due to docker limitation
ARG swift_version
ARG ubuntu_version

# set as UTF-8
#RUN apt-get update && apt-get install -y locales locales-all
#ENV LC_ALL en_US.UTF-8
#ENV LANG en_US.UTF-8
#ENV LANGUAGE en_US.UTF-8

# dependencies
RUN apt-get update && apt-get install -y wget
# for swift-pm
RUN apt-get update && apt-get install -y sqlite3 libsqlite3-dev libncurses5-dev

#RUN apt-get update && apt-get install -y lsof dnsutils netcat-openbsd net-tools curl jq # used by integration tests

# ruby and jazzy for docs generation
#RUN apt-get update && apt-get install -y ruby ruby-dev libsqlite3-dev build-essential
# switch of gem docs building
#RUN echo "gem: --no-document" > ~/.gemrc
#RUN if [ "${ubuntu_version}" != "xenial" ] ; then gem install jazzy ; fi

# tools
RUN mkdir -p $HOME/.tools
RUN echo 'export PATH="$HOME/.tools:$PATH"' >> $HOME/.profile

# install collection generator

ARG generator_version=main
RUN git clone --branch $generator_version --depth 1 https://github.com/apple/swift-package-collection-generator $HOME/.tools/package-collection-generator
RUN cd $HOME/.tools/package-collection-generator && swift build -c release
RUN ln -s $HOME/.tools/package-collection-generator/.build/release/package-collection-generate $HOME/.tools/package-collection-generate
RUN ln -s $HOME/.tools/package-collection-generator/.build/release/package-collection-diff $HOME/.tools/package-collection-diff
