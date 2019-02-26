---
title: Linux y macOS Tutorial de instalación para los Drivers de Microsoft para PHP para SQL Server | Microsoft Docs
ms.date: 02/11/2019
ms.prod: sql
ms.prod_service: connectivity
ms.custom: ''
ms.technology: connectivity
ms.topic: conceptual
author: ulvii
ms.author: v-ulibra
manager: v-mabarw
ms.openlocfilehash: a31b17b8fbe2130b84b27be08d1a6218d697f9f2
ms.sourcegitcommit: 958cffe9288cfe281280544b763c542ca4025684
ms.translationtype: MTE75
ms.contentlocale: es-ES
ms.lasthandoff: 02/23/2019
ms.locfileid: "56744635"
---
# <a name="linux-and-macos-installation-tutorial-for-the-microsoft-drivers-for-php-for-sql-server"></a>Linux y macOS Tutorial de instalación para los Drivers de Microsoft para PHP para SQL Server
Las siguientes instrucciones se supone un entorno limpio y muestran cómo instalar PHP 7.x, el controlador ODBC de Microsoft, Apache y los Drivers de Microsoft para PHP para SQL Server en Ubuntu 16.04, 18.04 y 18.10, Red Hat 7, Debian 8 y 9, Suse 12 y 15 y macOS 10.12 , 10.13 y 10.14. Estas instrucciones aconseja instalar los controladores con PECL, pero también puede descargar los archivos binarios creados previamente desde la [Microsoft Drivers para PHP para SQL Server](https://github.com/Microsoft/msphpsql/releases) Github página project e instalarlos siguiendo las instrucciones de [ Carga de los controladores de Microsoft para PHP para SQL Server](../../connect/php/loading-the-php-sql-driver.md). Para obtener una explicación de la carga de la extensión y por qué no agregar las extensiones en php.ini, vea la sección sobre [carga de los controladores](../../connect/php/loading-the-php-sql-driver.md##loading-the-driver-at-php-startup).

Estas instrucciones instalan PHP 7.3 de forma predeterminada. Nota Algunos admiten predeterminado de las distribuciones de Linux para PHP 7.0 o versiones anteriores, que no se admite para los controladores PHP para SQL Server, vea las notas al principio de cada sección para instalar PHP 7.1 o 7.2 en su lugar.

## <a name="contents-of-this-page"></a>Contenido de esta página:

- [Instalar a los controladores en Ubuntu 16.04, 18.04 y 18.10](#installing-the-drivers-on-ubuntu-1604-1804-and-1810)
- [Instalar a los controladores en Red Hat 7](#installing-the-drivers-on-red-hat-7)
- [Instalar a los controladores en Debian 8 y 9](#installing-the-drivers-on-debian-8-and-9)
- [Instalar a los controladores en Suse 12 y 15](#installing-the-drivers-on-suse-12-and-15)
- [Instalar a los controladores en macOS Sierra, High Sierra y Mojave](#installing-the-drivers-on-macos-sierra-high-sierra-and-mojave)

## <a name="installing-the-drivers-on-ubuntu-1604-1804-and-1810"></a>Instalar a los controladores en Ubuntu 16.04, 18.04 y 18.10

> [!NOTE]
> Para instalar PHP 7.1 o 7.2, reemplace 7.3 7.1 o 7.2 en los siguientes comandos.

### <a name="step-1-install-php"></a>Paso 1. Instalación de PHP
```
sudo su
add-apt-repository ppa:ondrej/php -y
apt-get update
apt-get install php7.3 php7.3-dev php7.3-xml -y --allow-unauthenticated
```
### <a name="step-2-install-prerequisites"></a>Paso 2. Requisitos previos de instalación
Instalar el controlador ODBC para Ubuntu siguiendo las instrucciones de la [página instalación de Linux y macOS](../../connect/odbc/linux-mac/installing-the-microsoft-odbc-driver-for-sql-server.md).

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
a2enmod php7.3
echo "extension=pdo_sqlsrv.so" >> /etc/php/7.3/apache2/conf.d/30-pdo_sqlsrv.ini
echo "extension=sqlsrv.so" >> /etc/php/7.3/apache2/conf.d/20-sqlsrv.ini
exit
```
### <a name="step-5-restart-apache-and-test-the-sample-script"></a>Paso 5. Reinicie Apache y probar el script de ejemplo
```
sudo service apache2 restart
```
Para probar la instalación, consulte [comprobación de la instalación](#testing-your-installation) al final de este documento.

## <a name="installing-the-drivers-on-red-hat-7"></a>Instalar a los controladores en Red Hat 7

> [!NOTE]
> Para instalar PHP 7.1 o 7.2, reemplace remi php73 remi php71 o remi-php72 respectivamente en los siguientes comandos.

### <a name="step-1-install-php"></a>Paso 1. Instalación de PHP

```
sudo su
wget https://dl.fedoraproject.org/pub/epel/epel-release-latest-7.noarch.rpm
wget https://rpms.remirepo.net/enterprise/remi-release-7.rpm
rpm -Uvh remi-release-7.rpm epel-release-latest-7.noarch.rpm
subscription-manager repos --enable=rhel-7-server-optional-rpms
yum install yum-utils
yum-config-manager --enable remi-php73
yum update
yum install php php-pdo php-xml php-pear php-devel re2c gcc-c++ gcc
```
### <a name="step-2-install-prerequisites"></a>Paso 2. Requisitos previos de instalación
Instalar el controlador ODBC para Red Hat 7 siguiendo las instrucciones de la [página instalación de Linux y macOS](../../connect/odbc/linux-mac/installing-the-microsoft-odbc-driver-for-sql-server.md).

Compilar los controladores PHP con PECL con PHP 7.2 o 7.3 requiere un GCC más reciente que el valor predeterminado:
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
Un problema en PECL puede impedir la instalación correcta de la versión más reciente de los controladores incluso si ha actualizado GCC. Para instalar, descargue los paquetes y compile manualmente (pasos similares para pdo_sqlsrv):
```
pecl download sqlsrv
tar xvzf sqlsrv-5.6.0.tgz
cd sqlsrv-5.6.0/
phpize
./configure --with-php-config=/usr/bin/php-config
make
sudo make install
```
También puede descargar los archivos binarios creados previamente desde la [página de Github del proyecto](https://github.com/Microsoft/msphpsql/releases), o bien instalar desde el repositorio Remi:
```
sudo yum install php-sqlsrv
```
### <a name="step-4-install-apache"></a>Paso 4. Instalar Apache
```
sudo yum install httpd
```
SELinux se instala de forma predeterminada y se ejecuta en modo aplicar. Para permitir que Apache para conectarse a bases de datos a través de SELinux, ejecute el siguiente comando:
```
sudo setsebool -P httpd_can_network_connect_db 1
```
### <a name="step-5-restart-apache-and-test-the-sample-script"></a>Paso 5. Reinicie Apache y probar el script de ejemplo
```
sudo apachectl restart
```
Para probar la instalación, consulte [comprobación de la instalación](#testing-your-installation) al final de este documento.

## <a name="installing-the-drivers-on-debian-8-and-9"></a>Instalar a los controladores en Debian 8 y 9

> [!NOTE]
> Para instalar PHP 7.1 o 7.2, reemplace 7.3 en los siguientes comandos 7.1 o 7.2.

### <a name="step-1-install-php"></a>Paso 1. Instalación de PHP
```
sudo su
apt-get install curl apt-transport-https
wget -O /etc/apt/trusted.gpg.d/php.gpg https://packages.sury.org/php/apt.gpg
echo "deb https://packages.sury.org/php/ $(lsb_release -sc) main" > /etc/apt/sources.list.d/php.list
apt-get update
apt-get install -y php7.3 php7.3-dev php7.3-xml
```
### <a name="step-2-install-prerequisites"></a>Paso 2. Requisitos previos de instalación
Instalar el controlador ODBC para Debian siguiendo las instrucciones de la [página instalación de Linux y macOS](../../connect/odbc/linux-mac/installing-the-microsoft-odbc-driver-for-sql-server.md). 

También es posible que deba generar la configuración regional correcta para obtener un resultado PHP se muestre correctamente en un explorador. Por ejemplo, para la configuración regional UTF-8 de en_US, ejecute los siguientes comandos:
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
apt-get install libapache2-mod-php7.3 apache2
a2dismod mpm_event
a2enmod mpm_prefork
a2enmod php7.3
echo "extension=pdo_sqlsrv.so" >> /etc/php/7.3/apache2/conf.d/30-pdo_sqlsrv.ini
echo "extension=sqlsrv.so" >> /etc/php/7.3/apache2/conf.d/20-sqlsrv.ini
```
### <a name="step-5-restart-apache-and-test-the-sample-script"></a>Paso 5. Reinicie Apache y probar el script de ejemplo
```
sudo service apache2 restart
```
Para probar la instalación, consulte [comprobación de la instalación](#testing-your-installation) al final de este documento.

## <a name="installing-the-drivers-on-suse-12-and-15"></a>Instalar a los controladores en Suse 12 y 15

> [!NOTE]
> En las instrucciones siguientes, reemplace <SuseVersion> con su versión de Suse - si usa Suse Enterprise Linux 15, será SLE_15 o SLE_15_SP1 y del mismo modo para otras versiones. No todas las versiones de PHP están disponibles para todas las versiones de Suse Linux -, consulte `http://download.opensuse.org/repositories/devel:/languages:/php` para ver qué versiones de Suse tienen la versión predeterminada de PHP disponible, o a `http://download.opensuse.org/repositories/devel:/languages:/php:/` para ver qué otras versiones de PHP están disponibles para las versiones de Suse.

> [!NOTE]
> Los paquetes para PHP 7.3 no están disponibles para Suse 12. Para instalar PHP 7.1, reemplace la dirección URL del repositorio a continuación con la siguiente dirección URL: `https://download.opensuse.org/repositories/devel:/languages:/php:/php71/<SuseVersion>/devel:languages:php:php71.repo`.
> Para instalar PHP 7.2, reemplace la dirección URL del repositorio a continuación con la siguiente dirección URL: `https://download.opensuse.org/repositories/devel:/languages:/php:/php72/<SuseVersion>/devel:languages:php:php72.repo`.

### <a name="step-1-install-php"></a>Paso 1. Instalación de PHP
```
sudo su
zypper -n ar -f https://download.opensuse.org/repositories/devel:languages:php/<SuseVersion>/devel:languages:php.repo
zypper --gpg-auto-import-keys refresh
zypper -n install php7 php7-pear php7-devel php7-openssl
```
### <a name="step-2-install-prerequisites"></a>Paso 2. Requisitos previos de instalación
Instalar el controlador ODBC para Suse siguiendo las instrucciones de la [página instalación de Linux y macOS](../../connect/odbc/linux-mac/installing-the-microsoft-odbc-driver-for-sql-server.md).

### <a name="step-3-install-the-php-drivers-for-microsoft-sql-server"></a>Paso 3. Instalar a los controladores PHP para Microsoft SQL Server
> [!NOTE]
> Si se produce un error mensaje que dice que `Connection to 'pecl.php.net:443' failed: Unable to find the socket transport "ssl"`, edite el script pecl en /usr/bin/pecl y quite el `-n` cambie en la última línea. Este modificador evita que PECL carga archivos ini cuando se llama a PHP, lo que impide que se carga la extensión OpenSSL.

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
exit
```
### <a name="step-5-restart-apache-and-test-the-sample-script"></a>Paso 5. Reinicie Apache y probar el script de ejemplo
```
sudo systemctl restart apache2
```
Para probar la instalación, consulte [comprobación de la instalación](#testing-your-installation) al final de este documento.

## <a name="installing-the-drivers-on-macos-sierra-high-sierra-and-mojave"></a>Instalar a los controladores en macOS Sierra, High Sierra y Mojave

Si no lo tiene, instale brew como sigue:
```
/usr/bin/ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)"
```

> [!NOTE]
> Para instalar PHP 7.1 o 7.2, reemplace php@7.3 con php@7.1 o php@7.2 respectivamente en los siguientes comandos.

### <a name="step-1-install-php"></a>Paso 1. Instalación de PHP

```
brew tap
brew tap homebrew/core
brew install php@7.3
```
PHP debe estar ahora en la ruta de acceso--ejecutar `php -v` para comprobar que se está ejecutando la versión correcta de PHP. Si no es PHP en la ruta de acceso o no es la versión correcta, ejecute lo siguiente:
```
brew link --force --overwrite php@7.3
```

### <a name="step-2-install-prerequisites"></a>Paso 2. Requisitos previos de instalación
Instalar el controlador ODBC para macOS, siga las instrucciones de la [página instalación de Linux y macOS](../../connect/odbc/linux-mac/installing-the-microsoft-odbc-driver-for-sql-server.md). 

Además, deberá instalar las herramientas de creación de GNU:
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
Para buscar al Apache archivo de configuración para la instalación de Apache, ejecute 
```
apachectl -V | grep SERVER_CONFIG_FILE
``` 
y sustituya la ruta de acceso `httpd.conf` en los siguientes comandos:
```
echo "LoadModule php7_module /usr/local/opt/php@7.2/lib/httpd/modules/libphp7.so" >> /usr/local/etc/httpd/httpd.conf
(echo "<FilesMatch .php$>"; echo "SetHandler application/x-httpd-php"; echo "</FilesMatch>";) >> /usr/local/etc/httpd/httpd.conf
```
### <a name="step-5-restart-apache-and-test-the-sample-script"></a>Paso 5. Reinicie Apache y probar el script de ejemplo
```
sudo apachectl restart
```
Para probar la instalación, consulte [comprobación de la instalación](#testing-your-installation) al final de este documento.

## <a name="testing-your-installation"></a>Probar la instalación

Para probar esta secuencia de comandos de ejemplo, cree un archivo denominado testsql.php en la raíz del documento de su sistema. Se trata de `/var/www/html/` en Ubuntu, Debian y Redhat, `/srv/www/htdocs` en SUSE, o `/usr/local/var/www` en macOS. Copie el script siguiente, reemplazando el servidor, base de datos, nombre de usuario y contraseña según corresponda.
```
<?php
$serverName = "yourServername";
$connectionOptions = array(
    "database" => "yourDatabase",
    "uid" => "yourUsername",
    "pwd" => "yourPassword"
);

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

<h1> Results : </h1>

<?php
while ($row = sqlsrv_fetch_array($stmt, SQLSRV_FETCH_ASSOC)) {
    echo $row['SQL_VERSION'] . PHP_EOL;
}

sqlsrv_free_stmt($stmt);
sqlsrv_close($conn);

function formatErrors($errors)
{
    // Display errors
    echo "Error information: <br/>";
    foreach ($errors as $error) {
        echo "SQLSTATE: ". $error['SQLSTATE'] . "<br/>";
        echo "Code: ". $error['code'] . "<br/>";
        echo "Message: ". $error['message'] . "<br/>";
    }
}
?>
```
Dirija el explorador https://localhost/testsql.php (https://localhost:8080/testsql.php en macOS). Ahora podrá conectarse a la base de datos SQL de SQL Server o SQL Azure.

## <a name="see-also"></a>Consulte también  
[Introducción a los controladores de Microsoft para PHP para SQL Server](../../connect/php/getting-started-with-the-php-sql-driver.md)

[Carga de los controladores de Microsoft para PHP para SQL Server](../../connect/php/loading-the-php-sql-driver.md)

[Requisitos del sistema para los controladores de Microsoft para PHP para SQL Server](../../connect/php/system-requirements-for-the-php-sql-driver.md)
