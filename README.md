# Https SSL Termination 

This is to enable testing of http endpoints locally when the clients expect SSL enablement

## Setup

1. On MacOS install nginx in some form. For e.g. using home brew

```
brew install nginx
```

1. Modify the config file in the nginx/conf folder - provide full paths to the cert file
Change the listening port or the forwarding ports as required

1. On Mac, install the Root certifcate to trust it... 

```
sudo security add-trusted-cert -d -r trustRoot -k /Library/Keychains/System.keychain ca_cert.pem
```

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

# NOTE:
If you are going to test using some python client, you may have to set the corresponding CA for the cert. In case you are using the sample certs in this repo, do the following

```
export REQUESTS_CA_BUNDLE=/Full/path/to/all_in_one.pem
export SSL_CERT_FILE=/Full/path/to/all_in_one.pem
```

The all_in_one.pem file consists of the cert file in Python + the ca_cert.pem for the sample cert
You can find the location of a recent Python cert file by installing certifi, and querying certifi.where().

cat <cacert file from certifi> <ca_cert.pem from this repo> > all_in_one.pem

