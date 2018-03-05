FROM ruby:2.5.0

RUN apt-get update -qq && apt-get install -y \
  build-essential \
  apt-transport-https \
  apt-utils \
  cmake \
  libpq-dev

# nokogiri
RUN apt-get install -y libxml2-dev libxslt1-dev

# nodejs
RUN curl -sL https://deb.nodesource.com/setup_8.x | bash - \
  && apt-get install -y nodejs

# yarn
RUN curl -sS https://dl.yarnpkg.com/debian/pubkey.gpg | apt-key add - \
  && echo "deb https://dl.yarnpkg.com/debian/ stable main" | tee /etc/apt/sources.list.d/yarn.list \
  && apt-get update \
  && apt-get install -y yarn

ENV APP_HOME /app
ADD . $APP_HOME
WORKDIR $APP_HOME

COPY Gemfile* $APP_HOME/
RUN bundle install

COPY package.json $APP_HOME/
RUN yarn install
