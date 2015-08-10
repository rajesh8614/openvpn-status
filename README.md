# openvpn-status
A web-based application to monitor clients connected to a openvpn server
## Installation
In order to download a fresh copy you first need to issue the respective ``npm`` command.

``npm install openvpn-status``

Afterwards you need to install the required node modules by issuing the respective npm command.

``npm install .``

## Configuration

The port under which the webinterface is available can be specified inside the ``config.json``

``{
  "port":3013
}``

Moreover you might want to customise the footer inside the ``views``.

```
<p class="text-center" style="font-size:smaller;">
  © [You], <a href="[Your Link Target]" target="_blank">[Your Link]</a>
</p> 
```

## Run

In order to run the server you can either run it in the foreground using the simple node command

``node server``

or you want to run it like a deamon by using ``forever`` to do so we first need to install forever using either locally or globally whichever you prefer. For a local installation simply omit the -g flag.

``npm install forever -g``

After that you can simply execute the bash script ``start.sh``. However you might need to make it executable using ``chmod``.

``chmod +x start.sh``

## Running the service behind nginx as a reverse proxy (optional)

In order to integrate the service into your webserver you might want to use nginx as a reverse proxy. The following configuration assumes that the port is set to *3013* as it is by default. The example also contains basic HTTP authentication to protect the service from unauthorised access.

```
server {
  listen 80;
  server_name [domain];

  auth_basic "Restricted";
  auth_basic_user_file /etc/nginx/cred/.status;

  location / {
    proxy_pass http://127.0.0.1:3013;
  }
}
```
