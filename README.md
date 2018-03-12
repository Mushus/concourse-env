# concourse

Concourse CI サーバーの構成管理

## install

```
$ git clone https://github.com/Mushus/concourse-env.git
$ cd concourse-env
$ mkdir -p keys/web keys/worker
$ ssh-keygen -t rsa -f ./keys/web/tsa_host_key -N ''
$ ssh-keygen -t rsa -f ./keys/web/session_signing_key -N ''
$ ssh-keygen -t rsa -f ./keys/worker/worker_key -N ''
$ cp ./keys/worker/worker_key.pub ./keys/web/authorized_worker_keys
$ cp ./keys/web/tsa_host_key.pub ./keys/worker
$ sudo docker-compose up -d
```

## create oauth application

```
https://github.com/settings/applications/new
```

```
# callback_url
https://ci.concourse-ci.org/auth/github/callback
```

## get cli

### for Linux

```
$ sudo curl -L "http://[YOUR HOST NAME]/api/v1/cli?arch=amd64&platform=linux" > /usr/local/bin/fly
$ sudo chmod 775 /usr/local/bin/fly
```

### for MacOSX

```
$ sudo curl -L "http://[YOUR HOST NAME]/api/v1/cli?arch=amd64&platform=darwin" > /usr/local/bin/fly
$ sudo chmod 775 /usr/local/bin/fly
```

## usage

ターゲット名 [TARGET NAME] でCIサーバー [YOUR HOST NAME] にログインする
```
fly -t [TARGET NAME] login -c http://[YOUR HOST NAME]
```

以後、以下のコマンドでログイン可能
```
fly -t [TARGET NAME] login
```

## create teams

```
fly set-team -n [TEAM_NAME] \
    --github-auth-client-id [CLIENT_ID] \
    --github-auth-client-secret [CLIENT_SECRET] \
    --github-auth-team [ORGANIZATION/TEAM]
```
