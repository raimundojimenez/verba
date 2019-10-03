# verba

Corpus disponibles:
 - [Telediarios con escaleta](https://s3.eu-west-3.amazonaws.com/verba-test.civio.es/Corpus-Telediarios-con-escaleta.zip) (10/3/2015 - 20/9/2017).
 - [Telediarios 2018](https://s3.eu-west-3.amazonaws.com/verba-test.civio.es/Corpus-Telediarios-2018.zip)


## Running locally

Project setup:

```
npm postinstall
```

Configure connection to Elastic backend making a copy of `/api/.env.example` into `/api.env` and modifying it accordingly. Same with `/web/.env.example`.

Start server (both API and web):

```
npm start
```

Compile and minifies for production:

```
npm build
```

## ElasticSearch

Estamos usando Elastic 7. Para instalarlo en OS X puedes usar `brew`, como [explican aquí](https://www.elastic.co/guide/en/elastic-stack-get-started/7.3/get-started-elastic-stack.html#install-elasticsearch):

```
brew tap elastic/tap
brew install elastic/tap/elasticsearch-full
elasticsearch
```

Y lo mismo con Kibana:

```
brew install elastic/tap/kibana-full
kibana
```

## Deployment

La aplicación está desplegada en `midas`, en `/var/www/verba-volant.civio.es/`. Hay dos partes, el frontend (hecho con Vue.js) que se sirve por el Apache y el API que es un servicio que levanta una aplicación Express. La configuración (variables de entorno...) del servicio está en `/etc/systemd/system/verba-api.service`.

Para actualizar la aplicación:

```
$ cd /var/www/verba-volant.civio.es/public
$ git pull
$ npm run build
$ sudo service verba-api restart
```

Una vez desplegada, la aplicación ofrece dos URLs:

- `https://verba-volant.civio.es/`, la aplicación web.
- `https://verba-volant.civio.es/api/`, el API usado por la aplicación.

Temporalmente tenemos también el Elastic abierto, mientras pulimos el proceso de desarrollo, en `https://api-verba-volant.civio.es/`.