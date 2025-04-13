# kong-try

## install docker

https://docs.konghq.com/gateway/latest/install/docker/#install-kong-gateway-with-a-database


## usage

Kong Gateway を触ってみる  
https://qiita.com/caunu-s/items/636aff1d04778fbbd779  

Kong Gatewayとは  
https://qiita.com/m5takeda/items/d7c74681c66692144ccc  

Kongの使い方を知る①　～Service & Route編～  
https://b-rabbit.jp/article/article01/index.html  


## setup services

```shell
curl -i -s -X POST http://192.168.1.24:8001/services ^
 --data name=quake ^
 --data url="https://api.p2pquake.net/v2/jma/quake?limit=1"

curl http://192.168.1.24:8001/services/
```

## setup routes

```shell
curl -i -X POST http://192.168.1.24:8001/services/quake/routes ^
 --data paths=/quake ^
 --data name=quake_route ^
 --data methods=GET

curl http://192.168.1.24:8001/routes/
```

## 確認
```shell
curl http://192.168.1.24:8000/quake?limit=1
```

## setup consumers

```shell
curl -X POST http://192.168.1.24:8001/consumers/ ^
 --data username=foo
curl http://192.168.1.24:8001/consumers/
```

## Key Authentication Plugins

```shell
curl -X POST http://192.168.1.24:8001/plugins/ ^
   --data "name=key-auth" ^
   --data "config.key_names=apikey"

curl -i -X POST http://192.168.1.24:8001/consumers/foo/key-auth ^
 --data key=bar
```

## 確認
```shell
curl http://192.168.1.24:8000/quake?apikey=bar&limit=1
```

## 参考

【REST Client】REST APIを簡単に試せるVSCode拡張  
https://qiita.com/adam_azmi/items/8f516f9854a337859045  

Kongのカスタムプラグイン内からAPIアクセスを行う  
https://zenn.dev/naoto_raimi/articles/beaf60bc5e2867  
