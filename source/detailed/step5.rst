.. _step5:

Step 5: Nginx
=============

We now set up nginx to serve as a reverse proxy. This allows us to easily set up SSL certificates. 


Setup Without SSL
^^^^^^^^^^^^^^^^^

We need to remove the default nginx config and add a new one for oTree. Let's remove the old one first::

    sudo rm /etc/nginx/sites-enabled/default

Then we create a new one using nano::

    sudo nano /etc/nginx/sites-enabled/otree

Copy in the following script::

    map $http_upgrade $connection_upgrade {
        default   upgrade;
        ''        close;
    }

    server {
        listen 80;
        server_name _;

        location / {
            proxy_pass http://localhost:8000;
            proxy_set_header X-Forwarded-Proto $scheme;
            proxy_set_header X-Forwarded-Port $server_port;
            proxy_set_header Host $host;
            proxy_set_header Upgrade $http_upgrade;
            proxy_set_header        Connection $connection_upgrade;
            proxy_set_header        X-Real-IP $remote_addr;
            proxy_set_header        X-Forwarded-For $proxy_add_x_forwarded_for;
            proxy_set_header        X-Forwarded-Host $server_name;
        }
    }

Save the file and exit nano with [ctrl] + [s] and [ctrl] + [x].


Setup with SSL
^^^^^^^^^^^^^^

We need to remove the default nginx config and add a new one for oTree. Let's remove the old one first::

    sudo rm /etc/nginx/sites-enabled/default

Then we create a new one using nano::

    sudo nano /etc/nginx/sites-enabled/otree

Copy in the following script::

    map $http_upgrade $connection_upgrade {
        default   upgrade;
        ''        close;
    }

    server {
        listen 80;
        server_name _;
        return 301 https://$server_name$request_uri;
    }

    server {
        listen 443 ssl;
        server_name _;

        ssl_certificate PATH_TO_SSL_CERTIFICATE_PEM;
        ssl_certificate_key PATH_TO_SSL_KEY;

        location / {
            proxy_pass http://localhost:8000;
            proxy_set_header X-Forwarded-Proto $scheme;
            proxy_set_header X-Forwarded-Port $server_port;
            proxy_set_header Host $host;
            proxy_set_header Upgrade $http_upgrade;
            proxy_set_header        Connection $connection_upgrade;
            proxy_set_header        X-Real-IP $remote_addr;
            proxy_set_header        X-Forwarded-For $proxy_add_x_forwarded_for;
            proxy_set_header        X-Forwarded-Host $server_name;
        }
    }

Make sure to replace ``PATH_TO_SSL_CERTIFICATE_PEM`` and ``PATH_TO_SSL_KEY`` with the appropriate paths to your SSL certificates. Finally, save the file and exit nano with [ctrl] + [s] and [ctrl] + [x].

This concludes Step 5.