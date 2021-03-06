## Photobook  
[![Photobook](https://developer.android.com/images/brand/en_app_rgb_wo_45.png)](https://play.google.com/store/apps/details?id=com.freecoders.photobook)

Photobook is an image sharing social service. You can express your feelings, emotions and memories; draw inspiration from public photo channels - animals, nature, travel, technology and much more.

[Client Repository](https://github.com/aboev/photobook-client)

[Server Repository](https://github.com/aboev/photobook-server)

### Setup guide
You may deploy server in docker container or install manually (requires some ruby/rails experience).
#### Docker setup (Recommended)
![alt text](https://www.docker.com/sites/default/files/horizontal.png)

Photobook supports cloud storage, push notifications and sms verification.
You may optionally select required features. If cloud storage is not configured, images are hosted locally.

1. Register [aws web services](http://aws.amazon.com) account, activate S3 storage and get AccessKeyID/SecretAccessKey (for S3 cloud storage)
2. Register [google developer](https://console.developers.google.com/) account, activate google cloud messaging API and get GoogleApiKey (for push notifications)
3. Register [smsc](http://www.smsc.ru) account and get login/pw or implement your custom gateway in lib/sms.sh (for sms verification)
4. Rename config/config.yml.example -> config/config.yml and replace config values in square brackets
5. Install docker-compose (Follow instructions on [docker website](https://docs.docker.com/compose/install/))
```
sudo apt-get install docker-compose (Ubuntu 16.04)
```
6. Deploy server in docker container
```
docker-compose run -p 80:80 -d photobook
```
Now, your server will be available on port 80. 
Tune up the endpoint on client side and you are ready to go! 

#### Manual setup

1. Prerequisites: imagemagick, postgresql, redis
2. Rename config/database.yml.example -> config/database.yml and replace username/password
3. Refer to [install.sh](https://github.com/aboev/photobook-server/blob/master/install.sh) (Step-by-step for Ubuntu 14.04)
```
bundle install
QUEUE=* rake environment resque:work
rails server
```
