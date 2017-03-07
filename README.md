# Simple Apache server deployment

This is an example of deployment of Apache deployment started via OCCI on EGI FedCloud. Service deployment is managed by custom
Puppet interface which supports r10k (Puppetfile), Hiera bindings
and access to Cloudify context (ctx). Tested on CentOS 7.x.

This example was prepared for purposes of *Cloud Orchestration Training* organized by MU within H2020 West-Life project (http://about.west-life.eu/).

## Standalone Cloudify

#### Setup OCCI CLI

```bash
yum install -y ruby-devel openssl-devel gcc gcc-c++ ruby rubygems
gem install occi-cli
```

#### Setup cloudify

```bash
make bootstrap
```

#### Run deployment

Use prepared container.

(First get valid X.509 VOMS certificate into `/tmp/x509up_u1000` and
have `m4` installed.)

```bash
source ~/cfy/bin/activate
make cfy-deploy
```

If succeeded, see deployed Apache endpoint URL. E.g.:

```bash
cfy local outputs
{
  "endpoint": {
    "url": "http://147.228.242.209"
  }
}
```

and open URL http://endpoint_ipaddress/cgi-bin/index.py in your browser to see where server is working.

SSH to server

```bash
ssh -i resources/ssh/id_rsa cfy@endpoint_ipaddress
```

Put you python application in /var/www/cgi-bin.



#### Destroy deployment

```bash
make cfy-undeploy
```
