FROM rocketchat/base:4

#ENV RC_VERSION develop

#MAINTAINER buildmaster@rocket.chat

VOLUME /app/uploads

RUN set -x \
 && curl -SLf "https://github.com/RocketChat/Rocket.Chat/archive/0.48.1.tar.gz" -o rocket.chat.tgz \
# && curl -SLf "https://rocket.chat/releases/${RC_VERSION}/asc" -o rocket.chat.tgz.asc \
# && gpg --verify rocket.chat.tgz.asc \
 && tar -zxf rocket.chat.tgz -C /app \
# && rm rocket.chat.tgz rocket.chat.tgz.asc \
 && rm rocket.chat.tgz \
 && cd /app/bundle/programs/server \
 && npm install \
 && npm cache clear

USER rocketchat

WORKDIR /app/bundle

# needs a mongoinstance - defaults to container linking with alias 'mongo'
ENV MONGO_URL=mongodb://mongo:27017/rocketchat \
    HOME=/tmp \
    PORT=3000 \
    ROOT_URL=http://localhost:3000 \
    Accounts_AvatarStorePath=/app/uploads

EXPOSE 3000

CMD ["node", "main.js"]
