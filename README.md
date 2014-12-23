# pack-checkmyws

(http://www.mylenela.fr/media/images/cmw_1.jpg)

Check my Website is a unique service for remote monitoring of websites and applications.

# Install check plugin

See this post for a complete tutorial (FR) : https://wooster.checkmy.ws/2014/06/checkmyws-nagios-icinga-shinken-plugin/

```
pip install --upgrade checkmyws-python docopt
cd /path/to/plugins/folder
wget --no-check-certificate https://raw.githubusercontent.com/checkmyws/checkmyws-plugins/master/nagios/check_mywebsite.py
chmod +x check_mywebsite.py
```

# Install pack

## Shinken 1.4

```
cd /tmp
git clone https://github.com/david-guenault/pack-checkmyws.git
mv pack-checkmyws/pack /etc/shinken/pack/checkmyws
```

## shinken 2.x

```
shinken install pack-checkmyws
```

# Using pack

- Create a host that will receive websites checks

```
define host{
    use             checkmyws
    contact_groups  admins
    host_name       Websites
    address         localhost
    _CHECKMYIDS     www.domain1.tld$(xxx-xxx-xxxx-xxxxx-xxxxx)$,www.domain2.tld$(yyyyy-yyyyy-yyyyyyy-yyyyy)$
}
```

Note : the _CHECKMYIDS will receive a list of website name / id pair. the website will be used to build the service description and id will be used by the plugin to grab monitoring data. 

id is available in the preferences tab of each monitored website. 
