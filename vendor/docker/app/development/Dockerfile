FROM ruby:2.4.0

RUN apt-get update -qq && apt-get install -y build-essential nodejs

ENV RAILS_ROOT /usr/src/app

RUN mkdir -p $RAILS_ROOT

ENV BUNDLE_PATH=$RAILS_ROOT/vendor/bundle

WORKDIR $RAILS_ROOT

CMD ["/bin/bash"]