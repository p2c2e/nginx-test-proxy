# Https SSL Termination 

This is to enable testing of http endpoints locally when the clients expect SSL enablement

## Setup

1. On MacOS install nginx in some form. For e.g. using home brew

```
brew install nginx
```

1. Modify the config file in the nginx/conf folder - provide full paths to the cert file
Change the listening port or the forwarding ports as required

1. Test the conf file changes like below:

```
nginx -t -c /Full/path/to/nginx/conf/nginx.conf
```

## Running it 
1. If all things are fine, run nginx in background mode like below. If the listen port is < 1024, you will need to sudo

```
nginx -c /Full/path/to/nginx/conf/nginx.conf
```

1. If you want the nginx instance to run in foreground, you can use:
```
nginx -g "daemon off;" -c /Full/path/to/nginx/conf/nginx.conf
```

1. Now point your client to https://localhost:port/<something> and this forwards it to the corresponding http://localhost:someport/<something> 




