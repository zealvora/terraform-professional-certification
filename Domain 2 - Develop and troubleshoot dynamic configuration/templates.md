### Base Nginx File (base-nginx.conf)

```sh
server {
    listen      8080;
    server_name kplabs.internal;


    location / {
        proxy_pass http://10.0.10.56:8085;
    }
}
```

### Template File (nginx.tftpl)

```sh
server {
    listen      ${nginx_port};
    server_name ${server_name};


    location / {
        proxy_pass http://${backend_ip}:${backend_port};
    }
}
```

### Final Code Used
```sh
resource "local_file" "this" {
    content = templatefile("./nginx.tftpl",{
        nginx_port=80,
        server_name="kplabs.in",
        backend_ip="10.77.30.5",
        backend_port=8080
        })
    filename = "./nginx.conf"
}
```