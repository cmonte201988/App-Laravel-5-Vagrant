Applicación LARAVEL 5 con Vagrant y Puppet!
===================

Aplicación esqueleto hecha con **LARAVEL 5**, virtualizada con **Vagrant** y **Puppet**.

----------

Despliegue
-------------

Una vez clonado el proyecto se debe proceder a iniciar la maquina virtual.

```
// Start machine Virtual
$ vagrant up
```

> **Note:**
De tener problemas con el hostmanager u otro plugin de Vagrant, a continuación los comandos de los plugin que puedan causar problemas.
```
//
$ vagrant plugin install vagrant-hostmanager
//
$ vagrant plugin install vagrant-vbguest
```

<i class="icon-hdd"></i> Configuración del Ambiente

Se esta usando un **box** genérico, por ello se tiene que hacer un paso mas en la configuración de la Virtual Machine.

```
// Ingresamos a la máquina virtual via SSH
$ vagrant ssh
// Luego vamos donde esta la configuración de los sitio hábiles
$ cd /etc/apache2/sites-available
// Editar el archivo 000-default.conf
$ sudo vim 000-default.conf
```

Modificar el archivo quedando de la siguiente forma.

```
<VirtualHost *:80>
	ServerName beautymove.local
    ServerAdmin webmaster@localhost
    DocumentRoot /var/www/source/public
    <Directory /var/www/source/public>
	    AllowOverride all
    </Directory>

	ErrorLog ${APACHE_LOG_DIR}/error.log
    CustomLog ${APACHE_LOG_DIR}/access.log combined

</VirtualHost>
```

Luego de haber configurado el archivo, proceder a activar el cambio y reiniciar el servicio **apache2**

```
//
$ sudo a2ensite 000-default.conf
//
$ sudo service apache2 restart
```
