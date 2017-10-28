Instalaci�n de jekyll:

La versi�n de ruby que tengo instalada es la 1.9.1 y la que se necesita es la 2.1.0 o superior

Instalo la versi�n 2.3
sudo apt-get install ruby2.3 ruby2.3-dev ruby-switch

Al pedir la versi�n devuelve la 1.9 por lo que la instalaci�n de jekyll no va a funcionar.

El comando: sudo update-alternatives --config ruby
permite cambiar la versi�n por defecto, activo la 2.3 y ya devuelve el valor correcto.

Es poble que tampoco funcione, una opci�n que he visto (y activado) es hacer que el enlace de ruby y de gem
se dirija a la versi�n que queremos. Para ello eliminamos los enlaces existentes y los sustituimos por los nuevos:

sudo rm /usr/bin/ruby
sudo rm /usr/bin/gem
sudo ln -s /usr/bin/ruby2.3 /usr/bin/ruby
sudo ln -s /usr/bin/gem2.3 /usr/bin/gem

Esto supongo que lo tendr�a que hacer el comando "sudo update-alternatives --config..." pero antes ten�a problemas y ahora no

Instalo jekyll:
sudo apt-get install jekyll

Ahora al preguntar las versiones ya da valores correctos:

~$ ruby -v
ruby 2.3.5p376 (2017-09-14 revision 59905) [x86_64-linux-gnu]
~$ gem -v
2.5.2.1
~$ jekyll -v
jekyll 3.6.2

-----------------------
Ya tenemos las versiones de trabajo de las aplicaciones, ahora vamos a crear un blog
Nos situamos en la carpeta dentro de la cual ir�n los archivos del blog y desde all� lanzamos los comandos:

cd ........
jekyll new jekyll-blog
cd jekyll-blog
sudo gem install exec jekyll serve
bundle exec jekyll serve

y listo: ya tenemos activado el servidor.

Si abrimos el navegador y vamos a la direcci�n
http://localhost:4000/
Veremos la p�gina que hemos creado por defecto

----------------------------
En local funciona bien pero al subir al servidor, si el repositorio se crea en una carpeta,no se forman correctamente los enlaces
dentro de la p�gina, toman como origen la p�gina principal pero no insertan la p�gina donde est� el repositorio.
Se resuelve modificando el archivo _config.yml
inserto la linea:
baseurl: "jekyll-blogPba" # the subpath of your site, e.g. /blog
y comento la original:
#baseurl: "" # the subpath of your site, e.g. /blog
de modo que en local (bundle exec jekyll serve) utilizo la primera (quitando el comentario #)
y al subirlo (git init) utilizo la segunda.
