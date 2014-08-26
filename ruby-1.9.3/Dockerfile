FROM promojam/ruby:1.9.3

ENV DEBIAN_FRONTEND noninteractive
ENV BUNDLE_PATH /home/rails/bundle

RUN apt-get update && apt-get install -y nodejs --no-install-recommends \
    && rm -rf /var/lib/apt/lists/*

RUN gem install foreman

RUN adduser rails --disabled-password --gecos "" \
    && mkdir -p /home/rails/app \
    && chown -R rails:rails /home/rails/app \
    && mkdir $BUNDLE_PATH \
    && chown -R rails:rails $BUNDLE_PATH

ONBUILD ADD Gemfile /home/rails/app/
ONBUILD ADD Gemfile.lock /home/rails/app/
ONBUILD RUN chown -R rails:rails Gemfile Gemfile.lock
ONBUILD RUN sudo -H -u rails bundle install --path $BUNDLE_PATH
ONBUILD ADD . /home/rails/app
ONBUILD RUN chown -R rails:rails /home/rails/app $BUNDLE_PATH

WORKDIR /home/rails/app
EXPOSE 3000
CMD ["foreman", "start"]
