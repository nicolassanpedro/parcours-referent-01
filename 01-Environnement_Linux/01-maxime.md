
[22 février 2016](#lundi-22-février)

# Lundi 22 février
Lancement des hostilités

Ne pas oublier : 
* Meetup
* Community Management
* Vidéo
* 

## Discussion JFK
Vous êtes nos contacts.
Découpage en petits morceaux pour estimer la difficulté et le temps des plus petites tâches.
On liste. Ordre chronologique, dépendances entre évènements.
Positionnement dans le temps.
Calcul des délais.

Exemple : 
Maquette => Page statique => Page dynamique v1 => Page dynamique v2

Estimation du temps : 
Si tout seul : % de risque
- techno connue ?
- techno éprouvée (communauté) ?
Et donc ajouter un pourcentage de délai.

Evaluation : 
Faire la moyenne des estimations individuelles.

Planning Poker
https://fr.wikipedia.org/wiki/Planning_poker



## Pb wifi après installation
 sudo apt-get install --reinstall bcmwl-kernel-source

 ## Install Php5 - Laravel
 Pour Php 5.6, besoin de apache2 2.4
 Or sur Ubuntu 12.04, par défaut apache 2.2

 * Supprimer Apache2
 apt-get remove apache2
apt-get remove apache2*
apt-get purge apache2 apache2-utils apache2.2-bin apache2-common
apt-get autoremove

* Ajouter le nouveau ppa
add-apt-repository ppa:ondrej/php5
apt-get update
apt-get upgrade

apt-get install apache2
apt-get install php5

### Ressources
* http://www.ivankrizsan.se/2014/07/17/upgrading-apache-http-server-2-2-to-2-4-on-ubuntu-12-04/

## Pb installing Laravel
 Apache is running a threaded MPM, but your PHP Module is not compiled to be threadsafe.  You need to recompile PHP.

 http://askubuntu.com/questions/453377/how-to-enable-event-mpm-apache-2-4-on-ubuntu-14-04-with-thread-safe-php

 ## Error Apache 403 Forbidden


Try this solution

http://askubuntu.com/a/601722/392041

basically just replace

Order allow,deny
allow from all

with

Require all granted

## Laravel servec phtml file :
It seems I was missing the libapache2-mod-php5 package...

http://askubuntu.com/questions/426304/laravel-serves-a-phtml-file

## Laravel 
logs/laravel.log" could not be opened: failed to open stream: Permission denied'

php artisan cache:clear 
chmod -R 777 app/storage 
composer dump-autoload

http://stackoverflow.com/questions/23540083/failed-to-open-stream-permission-denied-error-laravel


# Laravel SIM
Internal Error
cat /var/log/apache2/error.log
/home/maxime/simplon.co/workspace/sim/public/.htaccess: Invalid command 'Header', perhaps misspelled or defined by a module not included in the server configuration

the Header directive is in the mod_headers apache module. You need to make sure that module is loaded into the apache server.

> sudo a2enmod headers
>  sudo service apache2 restart

# Laravel Sim
Woops ... x2

production.ERROR: exception 'RuntimeException' with message 'No supported encrypter found. The cipher and / or key length are invalid.'

Fist, check packages are installed : 
sudo apt-get install -y mcrypt php5-mcrypt

Then generate a proper KEY

php artisan key:generate
Copy and paste the key in config/app.php

# Laravel
oduction.ERROR: exception 'ErrorException' with message 'file_put_contents(/home/maxime/simplon.co/workspace/sim/storage/framework/sessions/0f5c73bb82e01cc07b81ca39ede12ea4159c9a94): failed to open stream: Permission denied' in /home/maxime/simplon.co/workspace/sim/bootstrap/cache/compiled.php:6639

For that we need to enable apache mod_rewrite in apache server.Lets see how to enable apache mod_rewrite.

sudo a2enmod rewrite
sudo service apache2 restart


## Sim Laralve
 Browserify Failed!: Couldn't find preset "es2015" relative to directory "/home/maxime/simplon.co/workspace/sim/resources/assets/js" while parsing file: /home/maxime/simplon.co/workspace/sim/resources/assets/js/app.js
{ [Error: Couldn't find preset "es2015" relative to directory "/home/maxime/simplon.co/workspace/sim/resources/assets/js" while parsing file: /home/maxime/simplon.co/workspace/sim/resources/assets/js/app.js]

Googled around a bit and this solved my issue: Install babel-preset-es2015 via NPM and also babel-preset-react if you're also running React.

https://github.com/babel/babelify/issues/134

scp 