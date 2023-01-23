
## Beispiel NginX Config

```bash
# Reference: https://www.nginx.com/resources/wiki/start/topics/examples/full/

worker_processes 4;

events {
  worker_connections 1024;
}

http {
    ssl_session_timeout 10m;
  server {
    listen 8080 ssl http2;

    ssl_certificate /usr/share/nginx/ssl/localhost.pem;
    ssl_certificate_key /usr/share/nginx/ssl/localhost-key.pem;

    ssl_protocols TLSv1 TLSv1.1 TLSv1.2;
    ssl_ciphers HIGH:!aNull:!MD5;


    location / {
  
      proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
      proxy_set_header Host $host;

      proxy_pass https://servers;

      #enable Websockets
      proxy_http_version 1.1;
      proxy_set_header Upgrade $http_upgrade;
      proxy_set_header Connection "upgrade";
      
    }
  }

  upstream servers {
    # enable sticky session with either "hash" (uses the complete IP address)
    #hash $remote_addr consistent;
    # or "ip_hash" (uses the first three octets of the client IPv4 address, or the entire IPv6 address)
    ip_hash;
    # or "sticky" (needs commercial subscription)
    # sticky cookie srv_id expires=1h domain=.example.com path=/;

    server backend-one:3001;
    server backend-two:3001;
    server backend-three:3001;
    server backend-four:3001;
  }
}
```

Hier können wir über 4 Server, auf dem selben Port mit dem RoundRobin Approach LoadBalancen!
