---
title: Linux y macOS Tutorial de instalación de Drivers de Microsoft para PHP para SQL Server | Documentos de Microsoft
ms.date: 05/08/2018
ms.prod: sql
ms.prod_service: connectivity
ms.component: php
ms.suite: sql
ms.custom: ''
ms.technology: connectivity
ms.topic: conceptual
author: ulvii
ms.author: v-ulibra
manager: v-mabarw
ms.openlocfilehash: c1115eaf304fa360cf446b67fe98157d324c2347
ms.sourcegitcommit: 38f8824abb6760a9dc6953f10a6c91f97fa48432
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/10/2018
---
# <a name="linux-and-macos-installation-tutorial-for-the-microsoft-drivers-for-php-for-sql-server"></a>Linux y macOS Tutorial de instalación de Drivers de Microsoft para PHP para SQL Server
Las siguientes instrucciones supone un entorno limpio y muestran cómo instalar PHP 7.x, el controlador ODBC de Microsoft, Apache y Microsoft Drivers para PHP para SQL Server en Ubuntu 16.04 y 17.10, RedHat 7, 12 de Suse 8 y 9, Debian y macOS X 10.11 y 10.12. Estas instrucciones aconseja instalar los controladores con PECL, pero también puede descargar los archivos binarios creada previamente desde la [Microsoft Drivers for PHP para SQL Server](https://github.com/Microsoft/msphpsql/releases) Github página de proyecto e instalarlos siguiendo las instrucciones de [ Carga los controladores de Microsoft para PHP para SQL Server](../../connect/php/loading-the-php-sql-driver.md). Para obtener una explicación de la carga de extensión y por qué no agregar las extensiones en php.ini, vea la sección sobre [carga de los controladores](../../connect/php/loading-the-php-sql-driver.md##loading-the-driver-at-php-startup).

Estos instalación instrucción 7.2 PHP de forma predeterminada, vea las notas al principio de cada sección para instalar PHP 7.0 ó 7.1.

## <a name="contents-of-this-page"></a>Contenido de esta página:

- [Instalar a los controladores en Ubuntu 16.04 y 17.10](#installing-the-drivers-on-ubuntu-1604-and-1710)
- [Instalar a los controladores de Red Hat 7](#installing-the-drivers-on-red-hat-7)
- [Instalar a los controladores en Debian 8 y 9](#installing-the-drivers-on-debian-8-and-9)
- [Instalar a los controladores en Suse 12](#installing-the-drivers-on-suse-12)
- [Instalar a los controladores en macOS El capitán y Sierra](#installing-the-drivers-on-macos-el-capitan-and-sierra)

## <a name="installing-the-drivers-on-ubuntu-1604-and-1710"></a>Instalar a los controladores en Ubuntu 16.04 y 17.10

> [!NOTE]
> Para instalar PHP 7.0 ó 7.1, reemplace 7.2 con 7.0 ó 7.1 en los siguientes comandos.

### <a name="step-1-install-php"></a>Paso 1. Instalar PHP
```
sudo su
add-apt-repository ppa:ondrej/php -y
apt-get update
apt-get install php7.2 php7.2-dev php7.2-xml -y --allow-unauthenticated
```
### <a name="step-2-install-prerequisites"></a>Paso 2. Instalar los requisitos previos
Instalar el controlador ODBC para Ubuntu siguiendo las instrucciones de la [página de instalación de Linux y Mac OS](../../connect/odbc/linux-mac/installing-the-microsoft-odbc-driver-for-sql-server.md).

### <a name="step-3-install-the-php-drivers-for-microsoft-sql-server"></a>Paso 3. Instalar a los controladores PHP para Microsoft SQL Server
```
sudo pecl install sqlsrv
sudo pecl install pdo_sqlsrv
sudo su
echo extension=pdo_sqlsrv.so >> `php --ini | grep "Scan for additional .ini files" | sed -e "s|.*:\s*||"`/30-pdo_sqlsrv.ini
echo extension=sqlsrv.so >> `php --ini | grep "Scan for additional .ini files" | sed -e "s|.*:\s*||"`/20-sqlsrv.ini
exit
```
### <a name="step-4-install-apache-and-configure-driver-loading"></a>Paso 4. Instalar a Apache y configurar la carga del controlador
```
sudo su
apt-get install libapache2-mod-php7.2 apache2
a2dismod mpm_event
a2enmod mpm_prefork
a2enmod php7.2
echo "extension=pdo_sqlsrv.so" >> /etc/php/7.2/apache2/conf.d/30-pdo_sqlsrv.ini
echo "extension=sqlsrv.so" >> /etc/php/7.2/apache2/conf.d/20-sqlsrv.ini
exit
```
### <a name="step-5-restart-apache-and-test-the-sample-script"></a>Paso 5. Reinicie Apache y pruebe el script de ejemplo
```
sudo service apache2 restart
```
Para probar la instalación, consulte [comprobación de la instalación](#testing-your-installation) al final de este documento.

## <a name="installing-the-drivers-on-red-hat-7"></a>Instalar a los controladores de Red Hat 7

> [!NOTE]
> Para instalar PHP 7.0 ó 7.1, reemplace remi php72 con remi php70 o remi php71 respectivamente en los siguientes comandos.

### <a name="step-1-install-php"></a>Paso 1. Instalar PHP

```
sudo su
wget https://dl.fedoraproject.org/pub/epel/epel-release-latest-7.noarch.rpm
wget http://rpms.remirepo.net/enterprise/remi-release-7.rpm
rpm -Uvh remi-release-7.rpm epel-release-latest-7.noarch.rpm
subscription-manager repos --enable=rhel-7-server-optional-rpms
yum-config-manager --enable remi-php72
yum update
yum install php php-pdo php-xml php-pear php-devel re2c gcc-c++ gcc
```
### <a name="step-2-install-prerequisites"></a>Paso 2. Instalar los requisitos previos
Instalar el controlador ODBC para Red Hat 7 siguiendo las instrucciones de la [página de instalación de Linux y Mac OS](../../connect/odbc/linux-mac/installing-the-microsoft-odbc-driver-for-sql-server.md).

Compilar los controladores PHP con PECL con PHP 7.2 necesita un GCC más reciente que el valor predeterminado:
```
sudo yum-config-manager --enable rhel-server-rhscl-7-rpms
sudo yum install devtoolset-7
scl enable devtoolset-7 bash
```
### <a name="step-3-install-the-php-drivers-for-microsoft-sql-server"></a>Paso 3. Instalar a los controladores PHP para Microsoft SQL Server
```
sudo pecl install sqlsrv
sudo pecl install pdo_sqlsrv
sudo su
echo extension=pdo_sqlsrv.so >> `php --ini | grep "Scan for additional .ini files" | sed -e "s|.*:\s*||"`/30-pdo_sqlsrv.ini
echo extension=sqlsrv.so >> `php --ini | grep "Scan for additional .ini files" | sed -e "s|.*:\s*||"`/20-sqlsrv.ini
exit
```
Un problema en PECL puede impedir la correcta instalación de la versión más reciente de los controladores incluso si ha actualizado GCC. Para instalar, descargue los paquetes y compile manualmente:
```
pecl download sqlsrv
tar xvzf sqlsrv-5.2.0.tgz
cd sqlsrv-5.2.0/
phpize
./configure --with-php-config=/usr/bin/php-config
make
sudo make install
```
O bien puede descargar los archivos binarios creada previamente desde la [página de proyecto de Github](https://github.com/Microsoft/msphpsql/releases), o bien instalar desde el repositorio de Remi:
```
sudo yum install php-sqlsrv php-pdo_sqlsrv
```
### <a name="step-4-install-apache"></a>Paso 4. Instalar Apache
```
sudo yum install httpd
```
SELinux se instala de forma predeterminada y se ejecuta en modo aplicar. Para permitir que Apache para conectarse a bases de datos a través de SELinux, ejecute el siguiente comando:
```
sudo setsebool -P httpd_can_network_connect_db 1
```
### <a name="step-5-restart-apache-and-test-the-sample-script"></a>Paso 5. Reinicie Apache y pruebe el script de ejemplo
```
sudo apachectl restart
```
Para probar la instalación, consulte [comprobación de la instalación](#testing-your-installation) al final de este documento.

## <a name="installing-the-drivers-on-debian-8-and-9"></a>Instalar a los controladores en Debian 8 y 9

> [!NOTE]
> Para instalar PHP 7.0 ó 7.1, reemplace 7.2 en los siguientes comandos con 7.0 ó 7.1.

### <a name="step-1-install-php"></a>Paso 1. Instalar PHP
```
sudo su
apt-get install curl apt-transport-https
wget -O /etc/apt/trusted.gpg.d/php.gpg https://packages.sury.org/php/apt.gpg
echo "deb https://packages.sury.org/php/ $(lsb_release -sc) main" > /etc/apt/sources.list.d/php.list
apt-get update
apt-get install -y php7.2 php7.2-dev php7.2-xml
```
### <a name="step-2-install-prerequisites"></a>Paso 2. Instalar los requisitos previos
Instalar el controlador ODBC para Debian siguiendo las instrucciones de la [página de instalación de Linux y Mac OS](../../connect/odbc/linux-mac/installing-the-microsoft-odbc-driver-for-sql-server.md). 

También debe generar la configuración regional correcta para obtener una salida PHP se muestre correctamente en un explorador. Por ejemplo, para la configuración regional UTF-8 de en_US, ejecute los siguientes comandos:
```
sudo su
sed -i 's/# en_US.UTF-8 UTF-8/en_US.UTF-8 UTF-8/g' /etc/locale.gen
locale-gen
```

### <a name="step-3-install-the-php-drivers-for-microsoft-sql-server"></a>Paso 3. Instalar a los controladores PHP para Microsoft SQL Server
```
sudo pecl install sqlsrv
sudo pecl install pdo_sqlsrv
sudo su
echo extension=pdo_sqlsrv.so >> `php --ini | grep "Scan for additional .ini files" | sed -e "s|.*:\s*||"`/30-pdo_sqlsrv.ini
echo extension=sqlsrv.so >> `php --ini | grep "Scan for additional .ini files" | sed -e "s|.*:\s*||"`/20-sqlsrv.ini
exit
```
### <a name="step-4-install-apache-and-configure-driver-loading"></a>Paso 4. Instalar a Apache y configurar la carga del controlador
```
sudo su
apt-get install libapache2-mod-php7.2 apache2
a2dismod mpm_event
a2enmod mpm_prefork
a2enmod php7.2
echo "extension=pdo_sqlsrv.so" >> /etc/php/7.2/apache2/conf.d/30-pdo_sqlsrv.ini
echo "extension=sqlsrv.so" >> /etc/php/7.2/apache2/conf.d/20-sqlsrv.ini
```
### <a name="step-5-restart-apache-and-test-the-sample-script"></a>Paso 5. Reinicie Apache y pruebe el script de ejemplo
```
sudo service apache2 restart
```
Para probar la instalación, consulte [comprobación de la instalación](#testing-your-installation) al final de este documento.

## <a name="installing-the-drivers-on-suse-12"></a>Instalar a los controladores en Suse 12

> [!NOTE]
> Para instalar PHP 7.0, omita el siguiente comando agrega el repositorio - 7.0 es el predeterminado PHP en suse 12.
> Para instalar PHP 7.1, reemplace la dirección URL de repositorio a continuación con la dirección URL siguiente: `http://download.opensuse.org/repositories/devel:/languages:/php:/php71/SLE_12/devel:languages:php:php71.repo`

### <a name="step-1-install-php"></a>Paso 1. Instalar PHP
```
sudo su
zypper -n ar -f http://download.opensuse.org/repositories/devel:languages:php/SLE_12/devel:languages:php.repo
zypper --gpg-auto-import-keys refresh
zypper -n install php7 php7-pear php7-devel
```
### <a name="step-2-install-prerequisites"></a>Paso 2. Instalar los requisitos previos
Instalar el controlador ODBC para Suse 12 siguiendo las instrucciones de la [página de instalación de Linux y Mac OS](../../connect/odbc/linux-mac/installing-the-microsoft-odbc-driver-for-sql-server.md).

### <a name="step-3-install-the-php-drivers-for-microsoft-sql-server"></a>Paso 3. Instalar a los controladores PHP para Microsoft SQL Server
```
sudo pecl install sqlsrv
sudo pecl install pdo_sqlsrv
sudo su
echo extension=pdo_sqlsrv.so >> `php --ini | grep "Scan for additional .ini files" | sed -e "s|.*:\s*||"`/pdo_sqlsrv.ini
echo extension=sqlsrv.so >> `php --ini | grep "Scan for additional .ini files" | sed -e "s|.*:\s*||"`/sqlsrv.ini
exit
```
### <a name="step-4-install-apache-and-configure-driver-loading"></a>Paso 4. Instalar a Apache y configurar la carga del controlador
```
sudo su
zypper install apache2 apache2-mod_php7
a2enmod php7
echo "extension=sqlsrv.so" >> /etc/php7/apache2/php.ini
echo "extension=pdo_sqlsrv.so" >> /etc/php7/apache2/php.ini
```
### <a name="step-5-restart-apache-and-test-the-sample-script"></a>Paso 5. Reinicie Apache y pruebe el script de ejemplo
```
sudo systemctl restart apache2
```
Para probar la instalación, consulte [comprobación de la instalación](#testing-your-installation) al final de este documento.

## <a name="installing-the-drivers-on-macos-el-capitan-and-sierra"></a>Instalar a los controladores en macOS El capitán y Sierra

Si no lo tiene, instale cerveza como sigue:
```
/usr/bin/ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)"
```

> [!NOTE]
> Para instalar PHP 7.0 ó 7.1, reemplace php@7.2 con php@7.0 o php@7.1 respectivamente en los siguientes comandos.

### <a name="step-1-install-php"></a>Paso 1. Instalar PHP

```
brew tap
brew tap homebrew/core
brew install php@7.2
```
PHP debe estar en la ruta de acceso--ejecutar `php -v` para comprobar que está ejecutando la versión correcta de PHP. Si PHP no está en la ruta de acceso o no es la versión correcta, ejecute lo siguiente:
```
brew link --force --overwrite php@7.2
```

### <a name="step-2-install-prerequisites"></a>Paso 2. Instalar los requisitos previos
Instalar el controlador ODBC para macOS siguiendo las instrucciones de la [página de instalación de Linux y Mac OS](../../connect/odbc/linux-mac/installing-the-microsoft-odbc-driver-for-sql-server.md). 

Además, debe instalar las herramientas de creación de GNU:
```
brew install autoconf automake libtool
```

### <a name="step-3-install-the-php-drivers-for-microsoft-sql-server"></a>Paso 3. Instalar a los controladores PHP para Microsoft SQL Server
```
sudo pecl install sqlsrv
sudo pecl install pdo_sqlsrv
```
### <a name="step-4-install-apache-and-configure-driver-loading"></a>Paso 4. Instalar a Apache y configurar la carga del controlador
```
brew install apache2
```
Para averiguar al Apache archivo de configuración para la instalación de Apache, ejecute 
```
apachectl -V | grep SERVER_CONFIG_FILE
``` 
sustituyendo la ruta de acceso `httpd.conf` en los siguientes comandos:
```
echo "LoadModule php7_module /usr/local/opt/php@7.2/lib/httpd/modules/libphp7.so" >> /usr/local/etc/httpd/httpd.conf
(echo "<FilesMatch .php$>"; echo "SetHandler application/x-httpd-php"; echo "</FilesMatch>";) >> /usr/local/etc/httpd/httpd.conf
```
### <a name="step-5-restart-apache-and-test-the-sample-script"></a>Paso 5. Reinicie Apache y pruebe el script de ejemplo
```
sudo apachectl restart
```
Para probar la instalación, consulte [comprobación de la instalación](#testing-your-installation) al final de este documento.

## <a name="testing-your-installation"></a>Comprobación de la instalación

Para probar esta secuencia de comandos de ejemplo, cree un archivo denominado testsql.php en la raíz del documento de su sistema. Se trata de `/var/www/html/` en Ubuntu, Debian y Redhat, `/srv/www/htdocs` en SUSE, o `/usr/local/var/www` en macOS. Copie el script siguiente, reemplazando el servidor, la base de datos, el nombre de usuario y la contraseña según corresponda.
```
<?php
$serverName = "yourServername";
$connectionOptions = array(
    "Database" => "yourDatabase",
    "Uid" => "yourUsername",
    "PWD" => "yourPassword"
);

//Establishes the connection
$conn = sqlsrv_connect($serverName, $connectionOptions);
if( $conn === false ) {
    die( FormatErrors( sqlsrv_errors()));
}

//Select Query
$tsql= "SELECT @@Version as SQL_VERSION";

//Executes the query
$getResults= sqlsrv_query($conn, $tsql);

//Error handling
if ($getResults == FALSE)
    die(FormatErrors(sqlsrv_errors()));
?>

<h1> Results : </h1>

<?php
while ($row = sqlsrv_fetch_array($getResults, SQLSRV_FETCH_ASSOC)) {
    echo ($row['SQL_VERSION']);
    echo ("<br/>");
}

sqlsrv_free_stmt($getResults);

function FormatErrors( $errors )
{
    /* Display errors. */
    echo "Error information: <br/>";
    foreach ( $errors as $error )
    {
        echo "SQLSTATE: ".$error['SQLSTATE']."<br/>";
        echo "Code: ".$error['code']."<br/>";
        echo "Message: ".$error['message']."<br/>";
    }
}
?>
```
El explorador a http://localhost/testsql.php (http://localhost:8080/testsql.php en Mac OS). Ahora debe ser capaz de conectarse a la base de datos SQL de SQL Server o SQL Azure.

## <a name="see-also"></a>Vea también  
[Introducción a los controladores de Microsoft para PHP para SQL Server](../../connect/php/getting-started-with-the-php-sql-driver.md)

[Carga los controladores de Microsoft para PHP para SQL Server](../../connect/php/loading-the-php-sql-driver.md)

[Requisitos del sistema para los controladores de Microsoft para PHP para SQL Server](../../connect/php/system-requirements-for-the-php-sql-driver.md)
