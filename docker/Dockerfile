ARG swift_version=5.4
ARG ubuntu_version=bionic
ARG base_image=swift:$swift_version-$ubuntu_version
FROM $base_image
# needed to do again after FROM due to docker limitation
ARG swift_version
ARG ubuntu_version

# dependencies
RUN apt-get update && apt-get install -y wget
# for swift-pm
RUN apt-get update && apt-get install -y sqlite3 libsqlite3-dev libncurses5-dev

# tools
RUN mkdir -p $HOME/.tools
RUN echo 'export PATH="$HOME/.tools:$PATH"' >> $HOME/.profile

# install collection generator

ARG generator_version=main
RUN git clone --branch $generator_version --depth 1 https://github.com/apple/swift-package-collection-generator $HOME/.tools/package-collection-generator
RUN cd $HOME/.tools/package-collection-generator && swift build -c release
RUN ln -s $HOME/.tools/package-collection-generator/.build/release/package-collection-generate $HOME/.tools/package-collection-generate
RUN ln -s $HOME/.tools/package-collection-generator/.build/release/package-collection-diff $HOME/.tools/package-collection-diff
RUN ln -s $HOME/.tools/package-collection-generator/.build/release/package-collection-sign $HOME/.tools/package-collection-sign
