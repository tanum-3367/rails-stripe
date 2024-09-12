FROM ruby:3.2.3-alpine

RUN apk update && apk add --no-cache \
  build-base \
  nodejs \
  vim \
  mysql-client \
  mariadb-dev \
  git \
  tzdata \
  libxml2-dev \
  libxslt-dev \
  libc6-compat \
  imagemagick \
  vips-dev

RUN mkdir /app
WORKDIR /app

ADD Gemfile /app/Gemfile
ADD Gemfile.lock /app/Gemfile.lock

RUN bundle install

COPY . /app

# For rails credentials:edit
ENV EDITOR="vim"

COPY docker/local/entrypoint.sh /docker/local/entrypoint.sh
RUN chmod +x /docker/local/entrypoint.sh
ENTRYPOINT ["/docker/local/entrypoint.sh"]

CMD ["rails", "server", "-b", "0.0.0.0"]
