# Setup of Varnish in AWS (with ELB or Elasticbeanstalk as backend)

Full article:
https://medium.com/@zeno.yu/setup-of-varnish-in-aws-with-elb-or-elasticbeanstalk-as-backend-b115a601df4a

# Install varnish & nginx (blank)
ssh into the instance

```
sudo wget -O varnish.rpm https://packagecloud.io/varnishcache/varnish73/packages/el/9/varnish-7.3.0-1.el9.x86_64.rpm/download.rpm?distro_version_id=240
sudo dnf install -y varnish.rpm
sudo service varnish start

sudo yum install -y nginx
sudo service nginx start
```

## Then copy in the nginx config from this repo
```
sudo vi /etc/nginx/nginx.conf
```
Then restart nginx
```
sudo service nginx restart
```

## Varnish config (if you export config from Magento Admin config, comment out the probe)
```
sudo vi /etc/varnish/default.vcl
```

Restart varnish by
```
sudo service varnish restart
```

# To Debug Varnish

## Read varnish log
```
sudo varnishlog

sudo varnishstat
sudo varnishtop

sudo varnishtop -i BereqURL
```

## Read Ngnix reverse proxy log
```
sudo tail -f /var/log/nginx/access.log
sudo tail -f /var/log/nginx/error.log
```

Ideally when a page is cache from varnish, then varnish log will be 
VCL_Return = Deliver

And it would have no new entry in the reverse proxy access log


## Read Ngnix reverse proxy log
```
sudo tail -f /var/log/nginx/access.log
sudo tail -f /var/log/nginx/error.log
```
