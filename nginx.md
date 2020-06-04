## NGINX Hacks

* Create shared directory
```nginx
location /somedirectory/ {
    autoindex on;
    autoindex_exact_size off;
    autoindex_format html;
    autoindex_localtime on;
}
```
