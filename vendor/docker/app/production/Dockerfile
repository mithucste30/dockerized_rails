# Base image:
FROM ruby:2.4.0

# Install dependencies
RUN apt-get update
# install node
RUN apt-get install -y python-software-properties
RUN curl -sS https://dl.yarnpkg.com/debian/pubkey.gpg | apt-key add -
RUN echo "deb http://dl.yarnpkg.com/debian/ stable main" >> /etc/apt/sources.list.d/yarn.list
RUN curl -sL https://deb.nodesource.com/setup_7.x | bash -
RUN apt-get install -y nodejs

# install yarn (asset precompile dependency)
RUN apt-get install -y build-essential yarn


# Set an environment variable where the Rails app is installed to inside of Docker image:
ENV RAILS_ENV "production"
ENV RAILS_ROOT /var/www/dockerized_rails
RUN mkdir -p $RAILS_ROOT
ENV BUNDLE_PATH=$RAILS_ROOT/vendor/bundle

# Set working directory, where the commands will be ran:
WORKDIR $RAILS_ROOT

#Gems:
COPY Gemfile Gemfile
COPY Gemfile.lock Gemfile.lock
RUN gem install bundler
RUN bundle install

COPY config/puma.rb config/puma.rb

# Copy the main application.
COPY . .

EXPOSE 3000

RUN bundle exec rake assets:precompile

#ENTRYPOINT bundle exec rake neo4j:migrate

# The default command that gets ran will be to start the Puma server.
CMD bundle exec puma -C config/puma.rb

