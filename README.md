# Agregator Deployment
This project is responsible for implementing the docker-compose stack of the Agregator application.

## Installation
Installing [docker](https://docs.docker.com/) and [docker-compose](https://docs.docker.com/compose/install/) is required to run the application.

Stack uses containers hosted on Whiteaster's docker registry. Images tagged "latest" are the latest stable versions.

Wherever there are placeholders, e.g. `imgproxy_key_kere` or `PasswordHere123`, secure passwords should be generated or docker secret should be used.

### Application environment variables
The service `ofdAgregatorCMSPsql` has the following variables:
```
- POSTGRES_USER=agregatorcmsusr
- POSTGRES_PASSWORD=PasswordHere123
- POSTGRES_DB=agregatorcms
```

The service `ofdAgregatorRedis` has the following variables:
```
- REDIS_PASSWORD=redis_password_here
```

The service `ofdAgregatorRedisFiveStar` has the following variables:
```
- REDIS_PASSWORD=redisfivestar_password_here
```

The service `odfAgregatorImgproxy` has the following variables:
```
- IMGPROXY_KEY=imgproxy_key_kere
- IMGPROXY_SALT=imgproxy_salt_kere
- IMGPROXY_MAX_SRC_RESOLUTION=30
```

The service `odfAgregatorBackendCMS` has the following variables:
```
- DB_NAME=agregatorcms
- DB_USER=agregatorcmsusr
- DB_PASSWORD=PasswordHere123
- DB_HOST=ofdAgregatorCMSPsql
- DB_PORT=5432
```

The service `ofdAgregatorBackend` has the following variables:
```
- PRODUCTION=true
- BACKEND_CMS_URL=http://odfAgregatorBackendCMS:8000
- SOLR_COLLECTION_URL=http://data-epuszcza.biaman.pl:8983/solr/collection1
- DATASET_DETAILS_MAX_RESULTS_AMOUNT=1000
- DATAVERSE_URL=https://data-epuszcza.biaman.pl
- IMG_PROXY_URL=http://odfAgregatorImgproxy:8080
- IMG_PROXY_SALT=imgproxy_salt_kere
- IMG_PROXY_KEY=imgproxy_key_kere
- REDIS_HOST=ofdAgregatorRedis
- REDIS_PORT=6379
- REDIS_BD=0
- REDIS_PASSWORD=redis_password_here
- REDIS_EXPIRES_TIME_IN_SECONDS=60
- FIVE_STAR_REPOSITORY_URL=http://ofdFiveStarDataverse:8000
- RECAPTCHA_SECRET='secret_captcha_here'
- EMAIL_HOST='email_host'
- EMAIL_HOST_USER='email_host_user'
- EMAIL_HOST_PASSWORD='email_password'
- EMAIL_PORT=465
- EMAIL_USE_TLS=False
- EMAIl_USE_SSL=True
- DEFAULT_FROM_EMAIL='OFD <email_here>'
```

The service `ofdFiveStarDataverse` has the following variables:
```
- PRODUCTION=true
- BACKEND_CMS_URL=http://odfAgregatorBackendCMS:8000
- DATAVERSE_URL=https://data-epuszcza.biaman.pl
- SOLR_COLLECTION_URL=http://data-epuszcza.biaman.pl:8983/solr/collection1
- DATASET_DETAILS_MAX_RESULTS_AMOUNT=1000
- IMG_PROXY_URL=http://odfAgregatorImgproxy:8080
- IMG_PROXY_SALT=imgproxy_salt_kere
- IMG_PROXY_KEY=imgproxy_key_kere
- REDIS_HOST=ofdAgregatorRedisFiveStar
- REDIS_PORT=6379
- REDIS_BD=0
- REDIS_PASSWORD=redisfivestar_password_here
- REDIS_EXPIRES_TIME_IN_SECONDS=60
- REFRESH_FIVE_STAR_TIME=60
```

The service `ofdAgregatorFrontend` has the following variables:
```
- PROD=true
- HOSTNAME=${http}://${URL}/api/v1/
- captcha=frontend_captcha_here
- siteURL=${http}://${URL}/
- cms=${http}://${URL}/cms-api/v1/
```

## Deployment
```
$ http="http" URL="localhost" docker-compose pull
$ http="http" URL="localhost" docker-compose up -d
```

The `http` and `URL` variables define the addresses on which the application is to be launched and on which frontend the backend listens.
The `http` variable takes the value: `http` or `https`
The `URL` variable defines the target address of the application, for example `localhost` or `aggregator.openforestdata.pl`.

In the configuration presented above, the application will be launched and will be available at `http://localhost`.

## Contribution
The project was performed by Whiteaster sp.z o.o., with register office in Chorzów, Poland - www.whiteaster.com and provided under the GNU GPL v.3 license to the Contracting Entity - Mammal Research Institute Polish Academy of Science in Białowieża, Poland.We are proud to release this project under an Open Source license. If you want to share your comments, impressions or simply contact us, please write to the following e-mail address: info@whiteaster.com