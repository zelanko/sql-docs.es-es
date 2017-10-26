---
title: "Tutorial de instalación de controladores de Mac y Linux PHP | Documentos de Microsoft"
ms.date: 07/13/2017
ms.prod: sql-non-specified
ms.technology:
- drivers
ms.topic: article
author: ulvii
ms.author: v-ulibra
manager: Hadis Fard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 6ca464b620a092a910d341c90b0fec364dadd89b
ms.contentlocale: es-es
ms.lasthandoff: 09/09/2017

---
# <a name="php-linux-and-mac-drivers-installation-tutorial"></a>Tutorial de instalación de controladores de Mac y Linux PHP
Las siguientes instrucciones se supone un entorno limpio y muestran cómo instalar PHP 7.x, Microsoft ODBC driver, Apache y Microsoft para PHP controladores en Ubuntu 15.10, 16.04, RedHat 7, 8 Debian y Mac OS X.
## <a name="installing-the-drivers-on-ubuntu-1510-for-php-70"></a>Instalar a los controladores en Ubuntu 15.10 para PHP 7.0
No hay ningún paquete de PHP 7.1 disponible para Ubuntu 15.10.
### <a name="step-1-install-php"></a>Paso 1. Instalar PHP
```
sudo su
sh -c 'echo "deb http://packages.dotdeb.org jessie all \ndeb-src http://packages.dotdeb.org jessie all" >> /etc/apt/sources.list'
apt-get update
apt-get install php7.0 php7.0-fpm php-pear php7.0-dev mcrypt php7.0-mcrypt php-mbstring php7.0-xml
```
### <a name="step-2-install-prerequisites"></a>Paso 2. Instalar los requisitos previos
```
sudo su 
curl https://packages.microsoft.com/keys/microsoft.asc | apt-key add -
curl https://packages.microsoft.com/config/ubuntu/15.10/prod.list > /etc/apt/sources.list.d/mssql-release.list
exit
sudo apt-get update
sudo ACCEPT_EULA=Y apt-get install msodbcsql mssql-tools
sudo apt-get install unixodbc-dev
echo 'export PATH="$PATH:/opt/mssql-tools/bin"' >> ~/.bash_profile
echo 'export PATH="$PATH:/opt/mssql-tools/bin"' >> ~/.bashrc
source ~/.bashrc
```
### <a name="step-3-install-the-php-drivers-for-microsoft-sql-server"></a>Paso 3. Instalar a los controladores PHP para Microsoft SQL Server
```
sudo pear config-set php_ini `php --ini | grep "Loaded Configuration" | sed -e "s|.*:\s*||"` system
sudo pecl install sqlsrv
sudo pecl install pdo_sqlsrv
```
### <a name="step-4-install-apache-and-configure-driver-loading"></a>Paso 4. Instalar a Apache y configurar la carga del controlador
```
sudo su
apt-get install libapache2-mod-php7.0 apache2
a2dismod mpm_event
a2enmod mpm_prefork
a2enmod php7.0
echo "extension=sqlsrv.so" >> /etc/php/7.0/apache2/php.ini
echo "extension=pdo_sqlsrv.so" >> /etc/php/7.0/apache2/php.ini
```
### <a name="step-5-restart-apache-and-test-the-sample-script"></a>Paso 5. Reinicie Apache y pruebe el script de ejemplo
```
sudo service apache2 restart
```
Para probar la instalación, consulte **comprobación de la instalación** al final de este documento.
 
## <a name="installing-the-drivers-on-ubuntu-1604-for-php-70"></a>Instalar a los controladores en Ubuntu 16.04 para PHP 7.0
### <a name="step-1-install-php"></a>Paso 1. Instalar PHP 
```
sudo su
apt-get update
apt-get -y install php7.0 mcrypt php7.0-mcrypt php-mbstring php-pear php7.0-dev php7.0-xml 
```
### <a name="step-2-install-prerequisites"></a>Paso 2. Instalar los requisitos previos
```
sudo su 
curl https://packages.microsoft.com/keys/microsoft.asc | apt-key add -
curl https://packages.microsoft.com/config/ubuntu/16.04/prod.list > /etc/apt/sources.list.d/mssql-release.list
exit
sudo apt-get update
sudo ACCEPT_EULA=Y apt-get install msodbcsql mssql-tools 
sudo apt-get install unixodbc-dev
echo 'export PATH="$PATH:/opt/mssql-tools/bin"' >> ~/.bash_profile
echo 'export PATH="$PATH:/opt/mssql-tools/bin"' >> ~/.bashrc
source ~/.bashrc
```
### <a name="step-3-install-the-php-drivers-for-microsoft-sql-server"></a>Paso 3. Instalar a los controladores PHP para Microsoft SQL Server
```
sudo pear config-set php_ini `php --ini | grep "Loaded Configuration" | sed -e "s|.*:\s*||"` system
sudo pecl install sqlsrv
sudo pecl install pdo_sqlsrv
```
### <a name="step-4-install-apache-and-configure-driver-loading"></a>Paso 4. Instalar a Apache y configurar la carga del controlador
```
sudo su
apt-get install libapache2-mod-php7.0 apache2
a2dismod mpm_event
a2enmod mpm_prefork
a2enmod php7.0
echo "extension=sqlsrv.so" >> /etc/php/7.0/apache2/php.ini
echo "extension=pdo_sqlsrv.so" >> /etc/php/7.0/apache2/php.ini
```
### <a name="step-5-restart-apache-and-test-the-sample-script"></a>Paso 5. Reinicie Apache y pruebe el script de ejemplo
```
sudo service apache2 restart
```
Para probar la instalación, consulte **comprobación de la instalación** al final de este documento.
 
## <a name="installing-the-drivers-on-ubuntu-1604-for-php-71"></a>Instalar a los controladores en Ubuntu 16.04 para PHP 7.1
### <a name="step-1-install-php"></a>Paso 1. Instalar PHP 
```
sudo su
add-apt-repository ppa:ondrej/php
apt-get update
apt-get -y install php7.1 mcrypt php7.1-mcrypt php-mbstring php-pear php7.1-dev php7.1-xml
```
### <a name="step-2-install-prerequisites"></a>Paso 2. Instalar los requisitos previos
```
sudo su 
curl https://packages.microsoft.com/keys/microsoft.asc | apt-key add -
curl https://packages.microsoft.com/config/ubuntu/16.04/prod.list > /etc/apt/sources.list.d/mssql-release.list
exit
sudo apt-get update
sudo ACCEPT_EULA=Y apt-get install msodbcsql mssql-tools 
sudo apt-get install unixodbc-dev
echo 'export PATH="$PATH:/opt/mssql-tools/bin"' >> ~/.bash_profile
echo 'export PATH="$PATH:/opt/mssql-tools/bin"' >> ~/.bashrc
source ~/.bashrc
```
### <a name="step-3-install-the-php-drivers-for-microsoft-sql-server"></a>Paso 3. Instalar a los controladores PHP para Microsoft SQL Server
```
sudo pear config-set php_ini `php --ini | grep "Loaded Configuration" | sed -e "s|.*:\s*||"` system
sudo pecl install sqlsrv
sudo pecl install pdo_sqlsrv
```
### <a name="step-4-install-apache-and-configure-driver-loading"></a>Paso 4. Instalar a Apache y configurar la carga del controlador
```
sudo su
apt-get install libapache2-mod-php7.1 apache2
a2dismod mpm_event
a2enmod mpm_prefork
a2enmod php7.1
echo "extension=sqlsrv.so" >> /etc/php/7.1/apache2/php.ini
echo "extension=pdo_sqlsrv.so" >> /etc/php/7.1/apache2/php.ini
```
### <a name="step-5-restart-apache-and-test-the-sample-script"></a>Paso 5. Reinicie Apache y pruebe el script de ejemplo
```
sudo service apache2 restart
```
Para probar la instalación, consulte **comprobación de la instalación** al final de este documento.
 
## <a name="installing-the-drivers-on-red-hat-7-for-php-70-and-71"></a>Instalar a los controladores en Red Hat 7 para PHP 7.0 y 7.1
### <a name="step-1-install-php"></a>Paso 1. Instalar PHP 
Para instalar PHP 7.1, reemplace remi php70 con remi php71 en los siguientes comandos: 
```
sudo su
wget https://dl.fedoraproject.org/pub/epel/epel-release-latest-7.noarch.rpm
wget http://rpms.remirepo.net/enterprise/remi-release-7.rpm
rpm -Uvh remi-release-7.rpm epel-release-latest-7.noarch.rpm
subscription-manager repos --enable=rhel-7-server-optional-rpms
yum-config-manager --enable remi-php70 
yum update
yum install php php-pdo php-xml php-pear php-devel re2c gcc-c++ gcc
```
### <a name="step-2-install-prerequisites"></a>Paso 2. Instalar los requisitos previos
```
sudo su
curl https://packages.microsoft.com/config/rhel/7/prod.repo > /etc/yum.repos.d/mssql-release.repo
exit
sudo yum update
sudo yum remove unixODBC-utf16-devel
sudo ACCEPT_EULA=Y yum install msodbcsql mssql-tools 
sudo yum install unixODBC-devel
echo 'export PATH="$PATH:/opt/mssql-tools/bin"' >> ~/.bash_profile
echo 'export PATH="$PATH:/opt/mssql-tools/bin"' >> ~/.bashrc
source ~/.bashrc
```
### <a name="step-3-install-the-php-drivers-for-microsoft-sql-server"></a>Paso 3. Instalar a los controladores PHP para Microsoft SQL Server
```
sudo pecl install sqlsrv
sudo pecl install pdo_sqlsrv
```
### <a name="step-4-install-apache-and-configure-driver-loading"></a>Paso 4. Instalar a Apache y configurar la carga del controlador
```
sudo su
yum install httpd
echo "extension=sqlsrv.so" > /etc/php.d/sqlsrv.ini
echo "extension=pdo_sqlsrv.so" > /etc/php.d/pdo_sqlsrv.ini
```
SELinux se instala de forma predeterminada y se ejecuta en modo aplicar. Para permitir que Apache para conectarse a bases de datos a través de SELinux, ejecute el siguiente comando:
```
sudo setsebool -P httpd_can_network_connect_db 1
```
### <a name="step-5-restart-apache-and-test-the-sample-script"></a>Paso 5. Reinicie Apache y pruebe el script de ejemplo
```
sudo apachectl restart
```
Para probar la instalación, consulte **comprobación de la instalación** al final de este documento.
 
## <a name="installing-the-drivers-on-debian-8-for-php-70"></a>Instalar a los controladores en 8 Debian para PHP 7.0
### <a name="step-1-install-php"></a>Paso 1. Instalar PHP 
```
sudo su
apt-get install curl apt-transport-https
curl https://www.dotdeb.org/dotdeb.gpg | apt-key add -
echo "deb http://packages.dotdeb.org jessie all" >> /etc/apt/sources.list
echo "deb-src http://packages.dotdeb.org jessie all" >> /etc/apt/sources.list
apt-get update
apt-get install –y php7.0 php-pear php7.0-dev php7.0-xml
```
### <a name="step-2-install-prerequisites"></a>Paso 2. Instalar los requisitos previos
```
sudo su 
curl https://packages.microsoft.com/keys/microsoft.asc | apt-key add -
curl https://packages.microsoft.com/config/debian/8/prod.list > /etc/apt/sources.list.d/mssql-release.list
apt-get install -y locales
echo "en_US.UTF-8 UTF-8" > /etc/locale.gen 
locale-gen
exit
sudo apt-get update
sudo ACCEPT_EULA=Y apt-get install msodbcsql
sudo apt-get install unixodbc-dev
```
### <a name="step-3-install-the-php-drivers-for-microsoft-sql-server"></a>Paso 3. Instalar a los controladores PHP para Microsoft SQL Server
```
sudo pear config-set php_ini `php --ini | grep "Loaded Configuration" | sed -e "s|.*:\s*||"` system
sudo pecl install sqlsrv
sudo pecl install pdo_sqlsrv
```
### <a name="step-4-install-apache-and-configure-driver-loading"></a>Paso 4. Instalar a Apache y configurar la carga del controlador
```
sudo su
apt-get install libapache2-mod-php7.0 apache2
a2dismod mpm_event
a2enmod mpm_prefork
a2enmod php7.0
echo "extension=sqlsrv.so" >> /etc/php/7.0/apache2/php.ini
echo "extension=pdo_sqlsrv.so" >> /etc/php/7.0/apache2/php.ini
```
### <a name="step-5-restart-apache-and-test-the-sample-script"></a>Paso 5. Reinicie Apache y pruebe el script de ejemplo
```
sudo service apache2 restart
```
Para probar la instalación, consulte **comprobación de la instalación** al final de este documento.
 
## <a name="installing-the-drivers-on-debian-8-for-php-71"></a>Instalar a los controladores en 8 Debian para PHP 7.1
### <a name="step-1-install-php"></a>Paso 1. Instalar PHP 
```
sudo su
apt-get install curl apt-transport-https 
wget -O /etc/apt/trusted.gpg.d/php.gpg https://packages.sury.org/php/apt.gpg
echo "deb https://packages.sury.org/php/ $(lsb_release -sc) main" > /etc/apt/sources.list.d/php.list
apt-get update
apt-get install –y php7.1 php-pear php7.1-dev php7.1-xml
```
### <a name="step-2-install-prerequisites"></a>Paso 2. Instalar los requisitos previos
```
sudo su 
curl https://packages.microsoft.com/keys/microsoft.asc | apt-key add -
curl https://packages.microsoft.com/config/debian/8/prod.list > /etc/apt/sources.list.d/mssql-release.list
apt-get install -y locales
echo "en_US.UTF-8 UTF-8" > /etc/locale.gen 
locale-gen
exit
sudo apt-get update
sudo ACCEPT_EULA=Y apt-get install msodbcsql
sudo apt-get install unixodbc-dev
```
### <a name="step-3-install-the-php-drivers-for-microsoft-sql-server"></a>Paso 3. Instalar a los controladores PHP para Microsoft SQL Server
```
sudo pear config-set php_ini `php --ini | grep "Loaded Configuration" | sed -e "s|.*:\s*||"` system
sudo pecl install sqlsrv
sudo pecl install pdo_sqlsrv
```
### <a name="step-4-install-apache-and-configure-driver-loading"></a>Paso 4. Instalar a Apache y configurar la carga del controlador
```
sudo su
apt-get install libapache2-mod-php7.1 apache2
a2dismod mpm_event
a2enmod mpm_prefork
a2enmod php7.1
echo "extension=sqlsrv.so" >> /etc/php/7.1/apache2/php.ini
echo "extension=pdo_sqlsrv.so" >> /etc/php/7.1/apache2/php.ini
```
### <a name="step-5-restart-apache-and-test-the-sample-script"></a>Paso 5. Reinicie Apache y pruebe el script de ejemplo
```
sudo service apache2 restart
```
Para probar la instalación, consulte **comprobación de la instalación** al final de este documento.
 
## <a name="installing-the-drivers-on-macos-el-capitan-and-sierra"></a>Instalar a los controladores en MacOS El capitán y Sierra
### <a name="step-1-install-php"></a>Paso 1. Instalar PHP 
Para instalar PHP 7.1, reemplace php70 por php71 en los siguientes comandos:
```
/usr/bin/ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)"
brew tap 
brew tap homebrew/dupes
brew tap homebrew/versions
brew tap homebrew/homebrew-php
brew install php70 --with-pear --with-httpd24 --with-cgi
echo 'export PATH="/usr/local/sbin:$PATH"' >> ~/.bash_profile
echo 'export PATH="/usr/local/bin:$PATH"' >> ~/.bash_profile
source ~/.bash_profile
```
### <a name="step-2-install-prerequisites"></a>Paso 2. Instalar los requisitos previos
```
brew tap microsoft/msodbcsql https://github.com/Microsoft/homebrew-mssql-release
brew update
brew install msodbcsql
brew install mssql-tools
brew install autoconf
```
### <a name="step-3-install-the-php-drivers-for-microsoft-sql-server"></a>Paso 3. Instalar a los controladores PHP para Microsoft SQL Server
```
sudo pecl install sqlsrv
sudo pecl install pdo_sqlsrv
```
### <a name="step-4-install-apache-and-configure-driver-loading"></a>Paso 4. Instalar a Apache y configurar la carga del controlador
```
(echo "<FilesMatch .php$>"; echo "SetHandler application/x-httpd-php"; echo "</FilesMatch>";) >> /usr/local/etc/apache2/2.4/httpd.conf
```
### <a name="step-5-restart-apache-and-test-the-sample-script"></a>Paso 5. Reinicie Apache y pruebe el script de ejemplo
```
sudo apachectl restart
```
Para probar la instalación, consulte **comprobación de la instalación** al final de este documento.
 
## <a name="testing-your-installation"></a>Comprobación de la instalación
Para probar esta secuencia de comandos de ejemplo, cree un archivo denominado testsql.php en/var/www/html / (/ usr/local/var/www/htdocs en Mac OS) y copie el script siguiente, reemplazando el servidor, la base de datos, el nombre de usuario y la contraseña según corresponda. 
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
Seleccione el explorador http://localhost/testsql.php (http://localhost:8080/testsql.php en Mac OS). Ahora debe ser capaz de conectarse a la base de datos SQL de SQL Server o SQL Azure.


