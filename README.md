# nginx
<h1>权重负载</h1>
upstream mm{
        server 192.168.111.128:8081 weight=10;
        server 192.168.111.128:8082 weight=20;
}



server {
    listen 80;
    server_name 192.168.111.128;
       #将所有请求转发给demo_pool池的应用处理
    location / {
        
        proxy_set_header Host $host;
        proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
        proxy_pass http://mm;
    }
}
