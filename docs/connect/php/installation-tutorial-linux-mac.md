---
title: Instalación de Linux y macOS para los controladores de PHP
description: En estas instrucciones, aprenderá a instalar los controladores de Microsoft para PHP para SQL Server en Linux o macOS.
ms.date: 10/30/2020
ms.prod: sql
ms.prod_service: connectivity
ms.custom: ''
ms.technology: connectivity
ms.topic: conceptual
author: David-Engel
ms.author: v-daenge
manager: v-mabarw
ms.openlocfilehash: 66c505f588d6f250c0e18dc88a79b21ed658f2b5
ms.sourcegitcommit: 80701484b8f404316d934ad2a85fd773e26ca30c
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 11/03/2020
ms.locfileid: "93243738"
---
# <a name="linux-and-macos-installation-tutorial-for-the-microsoft-drivers-for-php-for-sql-server"></a>Tutorial de instalación de los controladores de Microsoft en Linux y macOS de PHP para SQL Server
En las instrucciones siguientes se supone que existe un entorno limpio y se explica cómo instalar PHP 7.x, Microsoft ODBC Driver, el servidor web de Apache y los controladores de Microsoft para PHP en SQL Server en Ubuntu 16.04, 18.04 y 20.04, RedHat 7 y 8, Debian 8, 9 y 10, Suse 12 y 15, Alpine 3.11 y macOS 10.13, 10.14 y 10.15. Estas instrucciones aconsejan instalar los controladores con PECL, pero también puede descargar los archivos binarios creados previamente de la página de proyecto de GitHub [Controladores de Microsoft para PHP para SQL Server](https://github.com/Microsoft/msphpsql/releases) e instalarlos siguiendo las instrucciones de [Carga de los controladores de Microsoft para PHP para SQL Server](../../connect/php/loading-the-php-sql-driver.md). Para obtener una explicación de la carga de la extensión y por qué no agregar las extensiones en php.ini, vea la sección sobre la [carga de los controladores](../../connect/php/loading-the-php-sql-driver.md#loading-the-driver-at-php-startup).

Estas instrucciones instalan PHP 7.4 de forma predeterminada mediante `pecl install`. Puede que primero deba ejecutar `pecl channel-update pecl.php.net`. Algunas distribuciones de Linux admitidas tienen como valor predeterminado PHP 7.1 o versiones anteriores, una opción no admitida para la última versión de los controladores de PHP para SQL Server. Consulte las notas al principio de cada sección para instalar PHP 7.2 o 7.3 en su lugar.

También se incluyen instrucciones para instalar el Administrador de procesos FastCGI para PHP, PHP-FPM, en Ubuntu. Esto es necesario si se usa el servidor web nginx en lugar de Apache.

Aunque estas instrucciones contienen comandos para instalar los controladores SQLSRV y PDO_SQLSRV, estos también se pueden instalar y funcionar independientemente. Los usuarios familiarizados con la personalización de la configuración pueden ajustar estas instrucciones para que sean específicas para SQLSRV o PDO_SQLSRV. Ambos controladores tienen las mismas dependencias, excepto donde se indica a continuación.

## <a name="contents-of-this-page"></a>Contenido de esta página

- [Instalación de los controladores en Ubuntu 16.04, 18.04 y 20.04](#installing-the-drivers-on-ubuntu-1604-1804-and-2004)
- [Instalación de los controladores con PHP-FPM en Ubuntu](#installing-the-drivers-with-php-fpm-on-ubuntu)
- [Instalación de los controladores en Red Hat 7 y 8](#installing-the-drivers-on-red-hat-7-and-8)
- [Instalación de los controladores en Debian 8, 9 y 10](#installing-the-drivers-on-debian-8-9-and-10)
- [Instalación de los controladores en Suse 12 y 15](#installing-the-drivers-on-suse-12-and-15)
- [Instalación de los controladores en Alpine 3.11](#installing-the-drivers-on-alpine-311)
- [Instalación de los controladores en macOS High Sierra, Mojave y Catalina](#installing-the-drivers-on-macos-high-sierra-mojave-and-catalina)

## <a name="installing-the-drivers-on-ubuntu-1604-1804-and-2004"></a>Instalación de los controladores en Ubuntu 16.04, 18.04 y 20.04

> [!NOTE]
> Para instalar PHP 7.2 o 7.3, reemplace 7.4 por 7.2 o 7.3 en los comandos siguientes.

### <a name="step-1-install-php"></a>Paso 1. Instalación de PHP
```bash
sudo su
add-apt-repository ppa:ondrej/php -y
apt-get update
apt-get install php7.4 php7.4-dev php7.4-xml -y --allow-unauthenticated
```
### <a name="step-2-install-prerequisites"></a>Paso 2. Requisitos previos de instalación
Para instalar el controlador ODBC para Ubuntu, siga las instrucciones del [artículo sobre instalación en Linux](../../connect/odbc/linux-mac/installing-the-microsoft-odbc-driver-for-sql-server.md).

### <a name="step-3-install-the-php-drivers-for-microsoft-sql-server"></a>Paso 3. Instalación de los controladores de PHP para Microsoft SQL Server
```bash
sudo pecl install sqlsrv
sudo pecl install pdo_sqlsrv
sudo su
printf "; priority=20\nextension=sqlsrv.so\n" > /etc/php/7.4/mods-available/sqlsrv.ini
printf "; priority=30\nextension=pdo_sqlsrv.so\n" > /etc/php/7.4/mods-available/pdo_sqlsrv.ini
exit
sudo phpenmod -v 7.4 sqlsrv pdo_sqlsrv
```

Si solo hay una versión de PHP en el sistema, el último paso se puede simplificar a `phpenmod sqlsrv pdo_sqlsrv`.

### <a name="step-4-install-apache-and-configure-driver-loading"></a>Paso 4. Instalación de Apache y configuración de la carga de los controladores
```bash
sudo su
apt-get install libapache2-mod-php7.4 apache2
a2dismod mpm_event
a2enmod mpm_prefork
a2enmod php7.4
exit
```
### <a name="step-5-restart-apache-and-test-the-sample-script"></a>Paso 5. Reinicio de Apache y prueba del script de ejemplo
```bash
sudo service apache2 restart
```
Para probar la instalación, vea [Probar la instalación](#testing-your-installation) al final de este documento.

## <a name="installing-the-drivers-with-php-fpm-on-ubuntu"></a>Instalación de los controladores con PHP-FPM en Ubuntu

> [!NOTE]
> Para instalar PHP 7.2 o 7.3, reemplace 7.4 por 7.2 o 7.3 en los comandos siguientes.

### <a name="step-1-install-php"></a>Paso 1. Instalación de PHP
```bash
sudo su
add-apt-repository ppa:ondrej/php -y
apt-get update
apt-get install php7.4 php7.4-dev php7.4-xml php7.4-fpm -y --allow-unauthenticated
```
Compruebe el estado del servicio PHP-FPM mediante la ejecución de
```bash
systemctl status php7.4-fpm
```
### <a name="step-2-install-prerequisites"></a>Paso 2. Requisitos previos de instalación
Para instalar el controlador ODBC para Ubuntu, siga las instrucciones del [artículo sobre instalación en Linux](../../connect/odbc/linux-mac/installing-the-microsoft-odbc-driver-for-sql-server.md).

### <a name="step-3-install-the-php-drivers-for-microsoft-sql-server"></a>Paso 3. Instalación de los controladores de PHP para Microsoft SQL Server
```bash
sudo pecl config-set php_ini /etc/php/7.4/fpm/php.ini
sudo pecl install sqlsrv
sudo pecl install pdo_sqlsrv
sudo su
printf "; priority=20\nextension=sqlsrv.so\n" > /etc/php/7.4/mods-available/sqlsrv.ini
printf "; priority=30\nextension=pdo_sqlsrv.so\n" > /etc/php/7.4/mods-available/pdo_sqlsrv.ini
exit
sudo phpenmod -v 7.4 sqlsrv pdo_sqlsrv
```
Si solo hay una versión de PHP en el sistema, el último paso se puede simplificar a `phpenmod sqlsrv pdo_sqlsrv`.

Compruebe que `sqlsrv.ini` y `pdo_sqlsrv.ini` se encuentran en `/etc/php/7.4/fpm/conf.d/`:
```bash
ls /etc/php/7.4/fpm/conf.d/*sqlsrv.ini
```
Reinicie el servicio PHP-FPM:
```bash
sudo systemctl restart php7.4-fpm
```

### <a name="step-4-install-and-configure-nginx"></a>Paso 4. Instalación y configuración de nginx
```bash
sudo apt-get update
sudo apt-get install nginx
sudo systemctl status nginx
```
Para configurar nginx, debe editar el archivo `/etc/nginx/sites-available/default`. Agregue `index.php` a la lista que se encuentra debajo de la sección que indica `# Add index.php to the list if you are using PHP`:
```
# Add index.php to the list if you are using PHP
index index.html index.htm index.nginx-debian.html index.php;
```
A continuación, modifique la sección que sigue a `# pass PHP scripts to FastCGI server` como se indica a continuación:
```
# pass PHP scripts to FastCGI server
#
location ~ \.php$ {
        include snippets/fastcgi-php.conf;
        fastcgi_pass unix:/run/php/php7.4-fpm.sock;
}
```
### <a name="step-5-restart-nginx-and-test-the-sample-script"></a>Paso 5. Reinicio de nginx y prueba del script de ejemplo
```bash
sudo systemctl restart nginx.service
```
Para probar la instalación, vea [Probar la instalación](#testing-your-installation) al final de este documento.

## <a name="installing-the-drivers-on-red-hat-7-and-8"></a>Instalación de los controladores en Red Hat 7 y 8

### <a name="step-1-install-php"></a>Paso 1. Instalación de PHP

Para instalar PHP en Red Hat 7, ejecute lo siguiente:
> [!NOTE]
> Para instalar PHP 7.2 o 7.3, reemplace remi-php74 por remi-php72 o remi-php73, respectivamente, en los comandos siguientes.
```bash
sudo su
yum install https://dl.fedoraproject.org/pub/epel/epel-release-latest-7.noarch.rpm
yum install https://rpms.remirepo.net/enterprise/remi-release-7.rpm
subscription-manager repos --enable=rhel-7-server-optional-rpms
yum install yum-utils
yum-config-manager --enable remi-php74
yum update
# Note: The php-pdo package is required only for the PDO_SQLSRV driver
yum install php php-pdo php-xml php-pear php-devel re2c gcc-c++ gcc
```

Para instalar PHP en Red Hat 8, ejecute lo siguiente:
> [!NOTE]
> Para instalar PHP 7.2 o 7.3, reemplace remi-7.4 por remi-7.2 o remi-7.3, respectivamente, en los comandos siguientes.
```bash
sudo su
dnf install https://dl.fedoraproject.org/pub/epel/epel-release-latest-8.noarch.rpm
dnf install https://rpms.remirepo.net/enterprise/remi-release-8.rpm
dnf install yum-utils
dnf module reset php
dnf module install php:remi-7.4
subscription-manager repos --enable codeready-builder-for-rhel-8-x86_64-rpms
dnf update
# Note: The php-pdo package is required only for the PDO_SQLSRV driver
dnf install php-pdo php-pear php-devel
```

### <a name="step-2-install-prerequisites"></a>Paso 2. Requisitos previos de instalación
Para instalar el controlador ODBC para Red Hat 7 u 8, siga las instrucciones del [artículo sobre instalación en Linux](../../connect/odbc/linux-mac/installing-the-microsoft-odbc-driver-for-sql-server.md).

### <a name="step-3-install-the-php-drivers-for-microsoft-sql-server"></a>Paso 3. Instalación de los controladores de PHP para Microsoft SQL Server
```bash
sudo pecl install sqlsrv
sudo pecl install pdo_sqlsrv
sudo su
echo extension=pdo_sqlsrv.so >> `php --ini | grep "Scan for additional .ini files" | sed -e "s|.*:\s*||"`/30-pdo_sqlsrv.ini
echo extension=sqlsrv.so >> `php --ini | grep "Scan for additional .ini files" | sed -e "s|.*:\s*||"`/20-sqlsrv.ini
exit
```

También puede instalar desde el repositorio Remi:
```bash
sudo yum install php-sqlsrv
```
### <a name="step-4-install-apache"></a>Paso 4. Instalación de Apache
```bash
sudo yum install httpd
```
SELinux está instalado de forma predeterminada y se ejecuta en modo de aplicación. Para que Apache pueda conectarse a las bases de datos mediante SELinux, ejecute el siguiente comando:
```bash
sudo setsebool -P httpd_can_network_connect_db 1
```
### <a name="step-5-restart-apache-and-test-the-sample-script"></a>Paso 5. Reinicio de Apache y prueba del script de ejemplo
```bash
sudo apachectl restart
```
Para probar la instalación, vea [Probar la instalación](#testing-your-installation) al final de este documento.

## <a name="installing-the-drivers-on-debian-8-9-and-10"></a>Instalación de los controladores en Debian 8, 9 y 10

> [!NOTE]
> Para instalar PHP 7.2 o 7.3, reemplace 7.4 en los comandos siguientes por 7.2 o 7.3.

### <a name="step-1-install-php"></a>Paso 1. Instalación de PHP
```bash
sudo su
apt-get install curl apt-transport-https
wget -O /etc/apt/trusted.gpg.d/php.gpg https://packages.sury.org/php/apt.gpg
echo "deb https://packages.sury.org/php/ $(lsb_release -sc) main" > /etc/apt/sources.list.d/php.list
apt-get update
apt-get install -y php7.4 php7.4-dev php7.4-xml php7.4-intl
```
### <a name="step-2-install-prerequisites"></a>Paso 2. Requisitos previos de instalación
Para instalar el controlador ODBC para Debian, siga las instrucciones del [artículo sobre instalación en Linux](../../connect/odbc/linux-mac/installing-the-microsoft-odbc-driver-for-sql-server.md). 

También es posible que deba generar la configuración regional correcta para que el resultado de PHP se muestre correctamente en un explorador. Por ejemplo, para la configuración regional UTF-8 en_US, ejecute los siguientes comandos:
```bash
sudo su
sed -i 's/# en_US.UTF-8 UTF-8/en_US.UTF-8 UTF-8/g' /etc/locale.gen
locale-gen
```
Es posible que tenga que agregar `/usr/sbin` a su `$PATH`, ya que el ejecutable `locale-gen` se encuentra allí.

### <a name="step-3-install-the-php-drivers-for-microsoft-sql-server"></a>Paso 3. Instalación de los controladores de PHP para Microsoft SQL Server
```bash
sudo pecl install sqlsrv
sudo pecl install pdo_sqlsrv
sudo su
printf "; priority=20\nextension=sqlsrv.so\n" > /etc/php/7.4/mods-available/sqlsrv.ini
printf "; priority=30\nextension=pdo_sqlsrv.so\n" > /etc/php/7.4/mods-available/pdo_sqlsrv.ini
exit
sudo phpenmod -v 7.4 sqlsrv pdo_sqlsrv
```

Si solo hay una versión de PHP en el sistema, el último paso se puede simplificar a `phpenmod sqlsrv pdo_sqlsrv`. Al igual que con `locale-gen`, `phpenmod` se encuentra en `/usr/sbin`, por lo que es posible que tenga que agregar este directorio a su `$PATH`.

### <a name="step-4-install-apache-and-configure-driver-loading"></a>Paso 4. Instalación de Apache y configuración de la carga de los controladores
```bash
sudo su
apt-get install libapache2-mod-php7.4 apache2
a2dismod mpm_event
a2enmod mpm_prefork
a2enmod php7.4
```
### <a name="step-5-restart-apache-and-test-the-sample-script"></a>Paso 5. Reinicio de Apache y prueba del script de ejemplo
```bash
sudo service apache2 restart
```
Para probar la instalación, vea [Probar la instalación](#testing-your-installation) al final de este documento.

## <a name="installing-the-drivers-on-suse-12-and-15"></a>Instalación de los controladores en Suse 12 y 15

> [!NOTE]
> En las instrucciones siguientes, reemplace `<SuseVersion>` por su versión de Suse; si usa Suse Enterprise Linux 15, será SLE_15 o SLE_15_SP1. Para Suse 12, use SLE_12_SP4 (o una versión superior si corresponde). No todas las versiones de PHP están disponibles para todas las versiones de SUSE Linux. Consulte `http://download.opensuse.org/repositories/devel:/languages:/php` para ver qué versiones de SUSE tienen disponible la versión predeterminada de PHP, o `http://download.opensuse.org/repositories/devel:/languages:/php:/` para ver qué otras versiones de PHP están disponibles para el resto de las versiones de SUSE.

> [!NOTE]
> Los paquetes de PHP 7.4 no están disponibles para Suse 12. Para instalar PHP 7.2, reemplace la dirección URL del repositorio a continuación con la siguiente dirección URL: `https://download.opensuse.org/repositories/devel:/languages:/php:/php72/<SuseVersion>/devel:languages:php:php72.repo`.
> Para instalar PHP 7.3, reemplace la dirección URL del repositorio a continuación con la dirección URL siguiente: `https://download.opensuse.org/repositories/devel:/languages:/php:/php73/<SuseVersion>/devel:languages:php:php73.repo`.

### <a name="step-1-install-php"></a>Paso 1. Instalación de PHP
```bash
sudo su
zypper -n ar -f https://download.opensuse.org/repositories/devel:languages:php/<SuseVersion>/devel:languages:php.repo
zypper --gpg-auto-import-keys refresh
zypper -n install php7 php7-devel php7-openssl
```
### <a name="step-2-install-prerequisites"></a>Paso 2. Requisitos previos de instalación
Para instalar el controlador ODBC para Suse, siga las instrucciones del [artículo sobre instalación en Linux](../../connect/odbc/linux-mac/installing-the-microsoft-odbc-driver-for-sql-server.md).

### <a name="step-3-install-the-php-drivers-for-microsoft-sql-server"></a>Paso 3. Instalación de los controladores de PHP para Microsoft SQL Server
> [!NOTE]
> Si obtiene un mensaje de error que indica `Connection to 'pecl.php.net:443' failed: Unable to find the socket transport "ssl"`, edite el script pecl en /usr/bin/pecl y quite el modificador `-n` en la última línea. Este modificador evita que PECL cargue archivos ini cuando se llama a PHP, lo que impide que se cargue la extensión OpenSSL.

```bash
sudo pecl install sqlsrv
sudo pecl install pdo_sqlsrv
sudo su
echo extension=pdo_sqlsrv.so >> `php --ini | grep "Scan for additional .ini files" | sed -e "s|.*:\s*||"`/pdo_sqlsrv.ini
echo extension=sqlsrv.so >> `php --ini | grep "Scan for additional .ini files" | sed -e "s|.*:\s*||"`/sqlsrv.ini
exit
```
### <a name="step-4-install-apache-and-configure-driver-loading"></a>Paso 4. Instalación de Apache y configuración de la carga de los controladores
```bash
sudo su
zypper install apache2 apache2-mod_php7
a2enmod php7
echo "extension=sqlsrv.so" >> /etc/php7/apache2/php.ini
echo "extension=pdo_sqlsrv.so" >> /etc/php7/apache2/php.ini
exit
```
### <a name="step-5-restart-apache-and-test-the-sample-script"></a>Paso 5. Reinicio de Apache y prueba del script de ejemplo
```bash
sudo systemctl restart apache2
```
Para probar la instalación, vea [Probar la instalación](#testing-your-installation) al final de este documento.

## <a name="installing-the-drivers-on-alpine-311"></a>Instalación de los controladores en Alpine 3.11

> [!NOTE]
> La versión predeterminada de PHP es 7.3. Las versiones alternativas de PHP pueden estar disponibles en otros repositorios para Alpine 3.11. En su lugar, puede compilar PHP desde el origen.

### <a name="step-1-install-php"></a>Paso 1. Instalación de PHP
Los paquetes PHP para Alpine se pueden encontrar en el repositorio de `edge/community`. Consulte [Habilitación del repositorio de la comunidad](https://wiki.alpinelinux.org/wiki/Enable_Community_Repository) en su wiki. Agregue la línea siguiente a `/etc/apt/repositories`, reemplazando `<mirror>` por la dirección URL de un reflejo del repositorio de Alpine:
```
http://<mirror>/alpine/edge/community
```
A continuación, ejecute:
```bash
sudo su
apk update
# Note: The php7-pdo package is required only for the PDO_SQLSRV driver
apk add php7 php7-dev php7-pear php7-pdo php7-openssl autoconf make g++
```
### <a name="step-2-install-prerequisites"></a>Paso 2. Requisitos previos de instalación
Para instalar el controlador ODBC para Alpine, siga las instrucciones del [artículo sobre instalación en Linux](../../connect/odbc/linux-mac/installing-the-microsoft-odbc-driver-for-sql-server.md). 

### <a name="step-3-install-the-php-drivers-for-microsoft-sql-server"></a>Paso 3. Instalación de los controladores de PHP para Microsoft SQL Server
```bash
sudo pecl install sqlsrv
sudo pecl install pdo_sqlsrv
sudo su
echo extension=pdo_sqlsrv.so >> `php --ini | grep "Scan for additional .ini files" | sed -e "s|.*:\s*||"`/10_pdo_sqlsrv.ini
echo extension=sqlsrv.so >> `php --ini | grep "Scan for additional .ini files" | sed -e "s|.*:\s*||"`/00_sqlsrv.ini
```

### <a name="step-4-install-apache-and-configure-driver-loading"></a>Paso 4. Instalación de Apache y configuración de la carga de los controladores
```bash
sudo apk add php7-apache2 apache2
```
### <a name="step-5-restart-apache-and-test-the-sample-script"></a>Paso 5. Reinicio de Apache y prueba del script de ejemplo
```bash
sudo rc-service apache2 restart
```
Para probar la instalación, vea [Probar la instalación](#testing-your-installation) al final de este documento.


## <a name="installing-the-drivers-on-macos-high-sierra-mojave-and-catalina"></a>Instalación de los controladores en macOS High Sierra, Mojave y Catalina

Si no lo tiene, instale brew como sigue:
```bash
/usr/bin/ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)"
```

> [!NOTE]
> Para instalar PHP 7.2 o 7.3, reemplace php@7.4 por php@7.2 o php@7.3, respectivamente, en los comandos siguientes.

### <a name="step-1-install-php"></a>Paso 1. Instalación de PHP

```bash
brew tap
brew tap homebrew/core
brew install php@7.4
```
Ahora, PHP debe estar en su ruta de acceso. Ejecute `php -v` para comprobar que está ejecutando la versión de PHP correcta. Si PHP no está en la ruta de acceso o no tiene la versión correcta, ejecute lo siguiente:
```bash
brew link --force --overwrite php@7.4
```

### <a name="step-2-install-prerequisites"></a>Paso 2. Requisitos previos de instalación
Para instalar el controlador ODBC para macOS, siga las instrucciones del [artículo sobre instalación en macOS](../../connect/odbc/linux-mac/install-microsoft-odbc-driver-sql-server-macos.md). 

Además, puede que deba instalar las herramientas de creación de GNU:
```bash
brew install autoconf automake libtool
```

### <a name="step-3-install-the-php-drivers-for-microsoft-sql-server"></a>Paso 3. Instalación de los controladores de PHP para Microsoft SQL Server
```bash
sudo pecl install sqlsrv
sudo pecl install pdo_sqlsrv
```
### <a name="step-4-install-apache-and-configure-driver-loading"></a>Paso 4. Instalación de Apache y configuración de la carga de los controladores
```bash
brew install apache2
```
Para buscar el archivo de configuración de Apache, `httpd.conf`, para la instalación de Apache, ejecute 
```bash
/usr/local/bin/apachectl -V | grep SERVER_CONFIG_FILE
``` 
Los comandos siguientes anexan la configuración requerida a `httpd.conf`. Asegúrese de sustituir la ruta de acceso devuelta por el comando anterior en lugar de `/usr/local/etc/httpd/httpd.conf`:
```bash
echo "LoadModule php7_module /usr/local/opt/php@7.4/lib/httpd/modules/libphp7.so" >> /usr/local/etc/httpd/httpd.conf
(echo "<FilesMatch .php$>"; echo "SetHandler application/x-httpd-php"; echo "</FilesMatch>";) >> /usr/local/etc/httpd/httpd.conf
```
### <a name="step-5-restart-apache-and-test-the-sample-script"></a>Paso 5. Reinicio de Apache y prueba del script de ejemplo
```bash
sudo apachectl restart
```
Para probar la instalación, vea [Probar la instalación](#testing-your-installation) al final de este documento.

## <a name="testing-your-installation"></a>Probar la instalación

Para probar este script de ejemplo, cree un archivo llamado testsql.php en la raíz del documento del sistema. Se trata de `/var/www/html/` en Ubuntu, Debian y Redhat, de `/srv/www/htdocs` en SUSE, de `/var/www/localhost/htdocs` en Alpine o de `/usr/local/var/www` en macOS. Copie el script siguiente y reemplace el servidor, la base de datos, el nombre de usuario y la contraseña según proceda.
```php
<?php
$serverName = "yourServername";
$connectionOptions = array(
    "database" => "yourDatabase",
    "uid" => "yourUsername",
    "pwd" => "yourPassword"
);

function exception_handler($exception) {
    echo "<h1>Failure</h1>";
    echo "Uncaught exception: " , $exception->getMessage();
    echo "<h1>PHP Info for troubleshooting</h1>";
    phpinfo();
}

set_exception_handler('exception_handler');

// Establishes the connection
$conn = sqlsrv_connect($serverName, $connectionOptions);
if ($conn === false) {
    die(formatErrors(sqlsrv_errors()));
}

// Select Query
$tsql = "SELECT @@Version AS SQL_VERSION";

// Executes the query
$stmt = sqlsrv_query($conn, $tsql);

// Error handling
if ($stmt === false) {
    die(formatErrors(sqlsrv_errors()));
}
?>

<h1> Success Results : </h1>

<?php
while ($row = sqlsrv_fetch_array($stmt, SQLSRV_FETCH_ASSOC)) {
    echo $row['SQL_VERSION'] . PHP_EOL;
}

sqlsrv_free_stmt($stmt);
sqlsrv_close($conn);

function formatErrors($errors)
{
    // Display errors
    echo "<h1>SQL Error:</h1>";
    echo "Error information: <br/>";
    foreach ($errors as $error) {
        echo "SQLSTATE: ". $error['SQLSTATE'] . "<br/>";
        echo "Code: ". $error['code'] . "<br/>";
        echo "Message: ". $error['message'] . "<br/>";
    }
}
?>
```
Dirija el explorador a https://localhost/testsql.php (https://localhost:8080/testsql.php en macOS). Ahora podrá conectarse a la base de datos de SQL Server o Azure SQL. Si no ve un mensaje de confirmación en el que se muestre información sobre la versión de SQL, vea [Recursos de soporte](support-resources-for-the-php-sql-driver.md) para conocer los recursos que pueden serle de ayuda.

## <a name="see-also"></a>Consulte también  
[Introducción a los controladores de Microsoft para PHP para SQL Server](../../connect/php/getting-started-with-the-php-sql-driver.md)

[Carga de los controladores de Microsoft para PHP para SQL Server](../../connect/php/loading-the-php-sql-driver.md)

[Requisitos del sistema para los controladores de Microsoft para PHP para SQL Server](../../connect/php/system-requirements-for-the-php-sql-driver.md)
