FROM ruby:2.6.4

RUN  apt update

RUN	 gem install rails && apt install nodejs -y

ONBUILD COPY app /opt/app

ONBUILD WORKDIR /opt/app

ONBUILD RUN bundle install
ONBUILD RUN rake db:migrate
ONBUILD RUN rake db:seed

#docker build -f Dockerfile -t ft-rails:on-build .
#docker build -f test1 -t ex02 .
#docker run -it -p 3000:3000 ex02
