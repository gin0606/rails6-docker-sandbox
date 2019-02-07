FROM ruby:2.6.0
RUN apt-get update -qq && apt-get install -y nodejs postgresql-client

# install node.js and yarn
RUN curl -s -L git.io/nodebrew | perl - setup
ENV PATH /root/.nodebrew/current/bin:$PATH
RUN nodebrew install-binary v10.15.1 && nodebrew use v10.15.1
RUN npm install npm@latest -g
RUN npm install -g yarn

RUN mkdir /myapp
WORKDIR /myapp
COPY Gemfile /myapp/Gemfile
COPY Gemfile.lock /myapp/Gemfile.lock
RUN gem update --system
RUN gem update bundler
RUN bundle install

COPY package.json /myapp/package.json
COPY yarn.lock /myapp/yarn.lock
RUN yarn install --check-files

COPY . /myapp
