Mikroservis mimarisi oluşturuyorsanız ve Swagger kullanıyorsanız

Bu paket tüm Swagger dosyalarınızı tek bır dosyada birleştirmenize yardımcı olur

Örnek olarak,  `http://service1/docs`, `http://service2/docs` isimli iki Swagger dosyanız var

Bu size yukarıdaki bütün linkleri tek bir linkte gösterir.`http://service/docs`

### Installation 
```
git clone https://github.com/furkandoganktf/swagger-combined.git
```

### Configuration 
See config/default.json as below:
```
{
    "list_url": [
        {
            "docs": "http://petstore.swagger.io/v2/swagger.json",
            "base_path": "http://petstore.swagger.io/v2",
            "route_match": ["/user*", "/pet*", "/store*"]
        }
    ],
    "info": { "title": "Example API", "version": "1.0" },
    "port": 3000
}
```
- docs: swagger document links
- base_path: Proxy Target
- route_match: Routes for proxy

Please make note that you changed `config/default.json` to match all swagger document links you have

### Multiple Configuration 
See configurations/config/default.json or configurations/config2/default.json  as below:
```
{
    "list_url": [
        {
            "docs": "http://petstore.swagger.io/v2/swagger.json",
            "base_path": "http://petstore.swagger.io/v2",
            "route_match": ["/user*", "/pet*", "/store*"]
        }
    ],
    "info": { "title": "Example API", "version": "1.0" },
    "port": 3000
}
```
To get build for any configuration you can change the volume of docker-compose.yml as below :
```
version: '3'
services:
  deneme:
    build: .
    ports:
     - "3000:3000"
    volumes:
     - ./configurations/config2/default.json:/build/config/default.json

```

### Run from Source Code

Run:
```
cd swagger-combined
docker-compose up -d 

```

### Test
In the default, swagger-combined run on port 3000 and included swagger-ui. So you just run `http://localhost:3000?url=http://localhost:3000/docs` to see everything you need. Or you can see swagger api at `http://localhost:3000/docs`

### Example & Demo
With config/default.json:
```
{
    "list_url": [
        {
            "docs": "http://petstore.swagger.io/v2/swagger.json",
            "base_path": "http://petstore.swagger.io/v2",
            "route_match": ["/user*", "/pet*", "/store*"]
        },
        {
            "docs": "https://angular-admin-seed.sonnguyen.ws/docs",
            "base_path": "https://angular-admin-seed.sonnguyen.ws",
            "route_match": ["/api/v1*"]
        }
    ],
    "info": { "title": "Example API", "version": "1.0" },
    "port": 3000
}
```

### License (MIT)
Copyright (c) 2018 Furkan Doğan <furkandoganktf@gmail.com>
