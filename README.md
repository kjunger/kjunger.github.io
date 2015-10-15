# Installer Jekyll et configurer Git/GitHub sous Linux (Debian)
## Installation de Jekyll
### Pré-requis
Pour installer Jekyll sur Debian, il faut impérativement paramétrer le système pour installer les éléments suivants (cela requiert les droits du superuser) :
- **Ruby** et ses outils de développements ;
```sh
~#  apt-get install ruby ruby-dev
```
- **RubyGems** : télécharger le .zip à cette adresse : [Page de téléchargement de RubyGems][gems], puis l'installer en manuel ;
```sh
~#  cd rubygems-2.4.8/
~/rubygems-2.4.8/#  ruby setup.rm
```
- **NodeJS** ;
```sh
~#  apt-get install curl
~#  curl --silent --location https://deb.nodesource.com/setup_0.12 | bash -
~#  apt-get install --yes nodejs
```
### Compilation et installation
L'installation s'effectue à l'aide de RubyGems, qui va compiler et installer Jekyll automatiquement (enfin, presque), en s'occupant de la résolution des dépendances logicielles. Il suffit de lancer la commande suivante (en tant que superuser) :
```sh
~#  gem install jekyll
```
Cela prend environ 2-3 minutes avant que Jekyll soit opérationnel.
### Utiliser Jekyll
Pour créer un site sous Jekyll, il suffit de lancer cette commande (les privilèges du superuser ne sont pas nécessaires) :
```sh
~$  jekyll new mon-super-site
```
... où *mon-super-site* peut être remplacé par n'importe quel nom.

Pour l'exécuter, il faut se déplacer dans le dossier (ici, *mon-super-site/*), puis demander à le lancer :
```sh
~$  cd mon-super-site/
~/mon-super-site/$  jekyll serve
```
Il ne reste plus qu'à le visionner (en entrant l'adresse que Jekyll lui assigne, généralement *http://127.0.0.1:4000*), et prendre un café !

[gems]: <https://rubygems.org/pages/download>
## Configurer Git et GitHub
### Installer Git sur la machine
L'installation de Git s'effectue de manière normale (cela nécessite les privilèges du superuser) :
```sh
~#  apt-get install git
```
Sous Debian (comme toute distribution Linux), Git s'utilise exclusivement en ligne de commande.
### Configurer Git
- **Nom et e-mail**

Pour identifier nos *commits*, il faut renseigner à Git nos coordonnées :
```sh
~$  git config --global user.name "Prénom NOM"
~$  git config --global user.email "adresse.mail@prestataire.com"
```
... où *Prénom NOM* et *adresse.mail@prestataire.com* doivent être remplacés par les coordonnées désirées.

- **Authentification**

Les communications entre Git sous Linux et nos *repositories* GitHub pour nos *commits* passent par le protocole HTTPS, et il peut être utile de mettre en cache nos identifiants afin de ne pas les renseigner à chaque *commit* :
```sh
~$  git config --global credential.helper cache
```

- **Mise en place d'un *repository* cloné servant également de site web**

Avec Git et GitHub, il est possible de créer et héberger un site web, que l'on peut mettre à jour sur sa machine et effectuer un *commit* une fois terminé.
Tout d'abord, il faut créer un *repository* sur GitHub, en le nommant comme suit :

> **utilisateur**.github.io

... où *utilisateur* doit être remplacé par votre nom **exact** d'utilisateur.

Retournons sous Linux, et créons un dossier du même nom que le *repository* :
```sh
~$  mkdir utilisateur.github.io
```
... où *utilisateur* doit être remplacé par votre nom **exact** d'utilisateur.

"Associons"-le au *repository* sur GitHub à l'aide de Git :
```sh
~$  git clone https://github.com/utilisateur/utilisateur.github.io
```
... où *utilisateur* doit être remplacé par votre nom **exact** d'utilisateur.

Ceci fait, créons-y un site... au hasard, en utilisant Jekyll :
```sh
~$  jekyll new utilisateur.github.io
```
... où *utilisateur* doit être remplacé par votre nom **exact** d'utilisateur.

*Commitons* de ce pas ces changements...
```sh
~$  git add --all
~$  git commit -m "Initial commit"
~$  git push -u origin master
```
... où *Initial commit* peut être remplacé par tout autre nom, pour labeliser les différents *commits*.