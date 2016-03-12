Diverse Linux OneLiner
---------------------------------

Install x64 caddy ( http server)
---------------------------------

    curl -skL 'https://caddyserver.com/download/build?os=linux&arch=amd64&features=' | tar xvzf -   && rm README.txt LICENSES.txt CHANGES.txt
    sudo mv caddy /usr/local/bin/ && sudo ln /usr/local/bin/caddy /usr/bin/caddy
    sudo apt-get install php5-fpm libfcgi-perl wget curl -y -f 
    
    #install perl fcgi
    wget http://nginxlibrary.com/downloads/perl-fcgi/fastcgi-wrapper -O /usr/bin/fastcgi-wrapper.pl
    wget http://nginxlibrary.com/downloads/perl-fcgi/perl-fcgi -O /etc/init.d/perl-fcgi
    chmod +x /usr/bin/fastcgi-wrapper.pl
    chmod +x /etc/init.d/perl-fcgi
    update-rc.d perl-fcgi defaults
    insserv perl-fcgi || systemctl daemon-reload 
    /etc/init.d/perl-fcgi start
    
    sudo cat > /etc/caddy.conf << EOF
        0.0.0.0:8443 {
            root /var/wwww
            log /var/log/http-caddy.log
            errors /var/log/error.log
            basicauth / root haxxor
            gzip
            #templates / .html
            
            fastcgi /bin/ 127.0.0.1:8999  {
             ext   .pl .psgi
             split .pl
            }
            
            # PHP-FPM with Unix socket
            fastcgi / /var/run/php5-fpm.sock php
            
            #Example Reverse Proxy call
            proxy /api/ http://127.0.0.1:3388/api/ {
             without /api
             proxy_header Host {host}
            }
            
            #Example FileSearch
            #search /search {
            # -path dbiesecke
            #        -path .git
            #        -generated_site
            #        +path shells
            # +path logs
            # +path log
            # template inc/search.tpl
            #}
            
            #Example rewrite
            #rewrite /shells/ {
            #    regexp (.*)\.json
            #    to  /bin/shodan.pl?uri={uri}
            #}
        }
    EOF



App::Every
---------------------------------
Makes a cron entry with 2x simple parameters.

* Alias: `alias cron-every='curl -sk 'https://raw.githubusercontent.com/iarna/App-Every/master/packed/every' | perl -X - -n  -l'`

*  Example:

    `% cron-every 3 hours ls`


        PATH=/home/foilo/cappucino/bin:/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin:/usr/games:/usr/local/games:/home/foilo/.rvm/bin
        LOCKFILE=/tmp/every_lock_b8d65f1a8f00500bbda75fc44a4d5f88
        SHELL=/bin/zsh
        54 */3 * * * [ ! -f $LOCKFILE -o ! -d /proc/`[ -f $LOCKFILE ] && cat $LOCKFILE` ] && ( echo $$ > $LOCKFILE ; cd "/home/foilo";  ls  ; rm $LOCKFILE )


Debian GRML scripts
---------------------------------

            wget -qO- http://deb.grml.org/repo-key.asc | sudo apt-key add --    
            sudo echo   'deb     http://deb.grml.org/ grml-testing main' > /etc/apt/sources.list.d/grml.list
            sudo apt-get update 

Install some usefull tools
---------------------------------

            sudo apt-get install grml-tips grml-crypt grml-network grml-paste grml-shlib grml-tips grml-quickconfig grml-scripts
            
Install ZSH
---------------------------------

            wget -qO- .zshrc http://git.grml.org/f/grml-etc-core/etc/zsh/zshrc


Monodevelop Latest
---------------------------------

            sudo add-apt-repository ppa:keks9n/monodevelop-latest
            
Scribes
---------------------------------

            sudo add-apt-repository ppa:mystilleef/scribes-daily
