# docker-network

This example shows that a container can have access to another container within its network even when no port is exposed. But the host doesn't have access to this port

```
$ docker-compose up
```

```
$ docker ps
CONTAINER ID        IMAGE               COMMAND                  CREATED             STATUS              PORTS               NAMES
52f1a481be53        nginx               "nginx -g 'daemon of…"   2 minutes ago       Up 41 seconds       80/tcp              docker-network_web_<id>_<hash>
3dc35bbd9796        alpine              "/bin/sh"                5 minutes ago       Up 41 seconds                           docker-network_bash_<id>_<hash>
```

```
$ curl localhost
curl: (7) Failed to connect to localhost port 80: Connection refused
$ curl docker-network_bash_<id>_<hash>
curl: (6) Could not resolve host: docker-network_bash_<id>_<hash>
```

```
$ docker attach docker-network_bash_<id>_<hash>

/ # wget docker-network_bash_<id>_<hash> && cat index.html
Connecting to docker-network_web_1_59d6ba5eb9d9 (172.20.0.3:80)
index.html           100% |***********************************************************************************************************************************************|   612   0:00:00 ETA
<!DOCTYPE html>
<html>
<head>
<title>Welcome to nginx!</title>
<style>
    body {
        width: 35em;
        margin: 0 auto;
        font-family: Tahoma, Verdana, Arial, sans-serif;
    }
</style>
</head>
<body>
<h1>Welcome to nginx!</h1>
<p>If you see this page, the nginx web server is successfully installed and
working. Further configuration is required.</p>

<p>For online documentation and support please refer to
<a href="http://nginx.org/">nginx.org</a>.<br/>
Commercial support is available at
<a href="http://nginx.com/">nginx.com</a>.</p>

<p><em>Thank you for using nginx.</em></p>
</body>
</html>
```
