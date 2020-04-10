---
title: Carga de los controladores de Microsoft para PHP para SQL Server | Microsoft Docs
ms.custom: ''
ms.date: 02/11/2019
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- loading the driver
ms.assetid: e5c114c5-8204-49c2-94eb-62ca63f5d3ec
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 5ce26b4800250cab25a6db6f5b3ed7ebf0b1d9bd
ms.sourcegitcommit: fe5c45a492e19a320a1a36b037704bf132dffd51
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 04/08/2020
ms.locfileid: "80922870"
---
# <a name="loading-the-microsoft-drivers-for-php-for-sql-server"></a>Carga de los controladores de Microsoft para PHP para SQL Server
[!INCLUDE[Driver_PHP_Download](../../includes/driver_php_download.md)]

En esta página se proporcionan instrucciones para cargar los [!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)] en el espacio del proceso PHP.  
  
Puede descargar los controladores pregenerados para su plataforma desde la página del proyecto de Github [Controladores de Microsoft para PHP para SQL Server](https://github.com/Microsoft/msphpsql/releases). Cada paquete de instalación contiene los archivos de los controladores SQLSRV y PDO_SQLSRV en las variantes de subprocesos y de no subproceso. En Windows, también están disponibles en variantes de 32 bits y de 64 bits. Consulte [Requisitos del sistema para los controladores de Microsoft para PHP para SQL Server](../../connect/php/system-requirements-for-the-php-sql-driver.md) para obtener una lista de los archivos de controlador contenidos en cada paquete. El archivo de controlador debe coincidir con la versión, la arquitectura y los subprocesos de PHP del entorno PHP.

En Linux y macOS, los controladores se pueden instalar alternativamente mediante PECL, tal y como se encuentra en el [tutorial de instalación](../../connect/php/installation-tutorial-linux-mac.md).

También puede crear los controladores desde el código fuente al crear PHP o mediante `phpize`. Si opta por crear los controladores desde el código fuente, tiene la opción de crearlos estáticamente en PHP en lugar de crearlos como extensiones compartidas agregando `--enable-sqlsrv=static --with-pdo_sqlsrv=static` (en Linux y macOS) o `--enable-sqlsrv=static --with-pdo-sqlsrv=static` (en Windows) al comando `./configure` al crear PHP. Para más información sobre el sistema de creación de PHP y `phpize`, consulte la [documentación de PHP](http://php.net/manual/install.php).
  
## <a name="moving-the-driver-file-into-your-extension-directory"></a>Traslado del archivo del controlador al directorio de extensión  
El archivo del controlador debe estar ubicado en un directorio donde el entorno de ejecución de PHP pueda encontrarlo. Es más fácil colocar el archivo del controlador en el directorio de extensión de PHP predeterminado (para encontrar el directorio predeterminado, ejecute `php -i | sls extension_dir` en Windows o `php -i | grep extension_dir` en Linux o macOS). Si no está utilizando el directorio de extensión predeterminado, especifique un directorio en el archivo de configuración de PHP (php.ini), utilizando la opción **extension_dir**. Por ejemplo, en Windows, si ha colocado el archivo del controlador en el directorio `c:\php\ext`, agregue la siguiente línea al archivo php.ini:
  
```  
extension_dir = "c:\PHP\ext"  
```

## <a name="loading-the-driver-at-php-startup"></a>Carga del controlador al iniciar PHP  
Para cargar el controlador de SQLSRV cuando se inicie PHP, mueva primero un archivo del controlador al directorio de extensión. A continuación, siga estos pasos:  
  
1.  Para habilitar el controlador **SQLSRV**, modifique el archivo **php.ini** agregando la siguiente línea a la sección de extensión, cambiando el nombre del archivo según corresponda:  
  
    En Windows: 
    ```  
    extension=php_sqlsrv_72_ts.dll  
    ```  
    En Linux, si ha descargado los binarios precompilados para la distribución: 
    ```  
    extension=php_sqlsrv_72_nts.so  
    ```
    Si ha compilado el binario de SQLSRV desde el código fuente o con PECL, pasará a denominarse sqlsrv.so:
    ```
    extension=sqlsrv.so
    ```
  
2.  Para habilitar el controlador **PDO_SQLSRV**, la extensión de objetos de datos de PHP (PDO) debe estar disponible como extensión integrada o extensión cargada dinámicamente.

    En Windows, los binarios de PHP precompilados incorporan PDO, por lo que no es necesario modificar el archivo php.ini para cargarlo. Sin embargo, si ha compilado PHP desde el código fuente y ha especificado una extensión PDO independiente que se va a compilar, se le llamará `php_pdo.dll`, y se debe copiar en el directorio de la extensión y agregar la siguiente línea al archivo php.ini:  
    ```
    extension=php_pdo.dll  
    ```
    En Linux, si ha instalado PHP con el administrador de paquetes del sistema, PDO probablemente se instala como una extensión cargada dinámicamente denominada pdo.so. La extensión PDO debe cargarse antes que la extensión PDO_SQLSRV; de lo contrario, se producirá un error de carga. Normalmente, las extensiones se cargan mediante archivos .ini individuales, y estos archivos se leen después del archivo php.ini. Por lo tanto, si pdo.so se carga a través de su propio archivo .ini, se requiere una carga de archivos independiente en el controlador PDO_SQLSRV después de PDO. 

    Para averiguar en qué directorio se encuentran los archivos .ini específicos de la extensión, ejecute `php --ini` y anote el directorio que aparece en `Scan for additional .ini files in:`. Busque el archivo que carga pdo.so; es probable que tenga como prefijo un número, como 10-pdo.ini. El prefijo numérico indica el orden de carga de los archivos .ini, mientras que los archivos que no tienen un prefijo numérico se cargan alfabéticamente. Cree un archivo para cargar el archivo del controlador PDO_SQLSRV llamado 30-pdo_sqlsrv. ini (cualquier número mayor que el que se utilice como prefijo para PDO.ini funciona) o pdo_sqlsrv. ini (si el archivo pdo.ini no tiene un número como prefijo) y agréguele la línea siguiente, cambiando el nombre de archivo según corresponda:  
    ```
    extension=php_pdo_sqlsrv_72_nts.so
    ```
    Al igual que con SQLSRV, si ha compilado el binario de PDO_SQLSRV desde el código fuente o con PECL, pasará a denominarse pdo_sqlsrv.so:
    ```
    extension=pdo_sqlsrv.so
    ```
    Copie este archivo en el directorio que contiene los demás archivos .ini. 

    Si ha compilado PHP desde el código fuente con compatibilidad con PDO integrada, no necesita un archivo .ini independiente y puede agregar la línea adecuada anterior al archivo php.ini.
  
3.  Reinicie el servidor web.  
  
> [!NOTE]  
> Para determinar si el controlador se ha cargado correctamente, ejecute un script que llame a [phpinfo()](https://php.net/manual/en/function.phpinfo.php).  
  
Para obtener más información sobre las directivas de **php.ini**, vea el artículo [Descripción de las directivas del núcleo de php.ini](https://php.net/manual/en/ini.core.php).  
  
## <a name="see-also"></a>Consulte también  
[Introducción a los controladores de Microsoft para PHP para SQL Server](../../connect/php/getting-started-with-the-php-sql-driver.md)

[Requisitos del sistema para los controladores de Microsoft para PHP para SQL Server](../../connect/php/system-requirements-for-the-php-sql-driver.md)

[Guía de programación para los controladores de Microsoft para PHP para SQL Server](../../connect/php/programming-guide-for-php-sql-driver.md)

[Referencia de API del controlador SQLSRV](../../connect/php/sqlsrv-driver-api-reference.md)

[Referencia de la API del controlador PDO_SQLSRV](../../connect/php/pdo-sqlsrv-driver-reference.md)  
  
