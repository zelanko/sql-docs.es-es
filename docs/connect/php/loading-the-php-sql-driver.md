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
author: MightyPen
ms.author: genemi
ms.openlocfilehash: e3c6614425cf8796bd7ec462a62f9410b9ca5857
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MTE75
ms.contentlocale: es-ES
ms.lasthandoff: 07/15/2019
ms.locfileid: "67936382"
---
# <a name="loading-the-microsoft-drivers-for-php-for-sql-server"></a>Carga de los controladores de Microsoft para PHP para SQL Server
[!INCLUDE[Driver_PHP_Download](../../includes/driver_php_download.md)]

En esta página se proporcionan instrucciones para cargar los [!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)] en el espacio del proceso PHP.  
  
Puede descargar los controladores pregenerados para su plataforma en la página de proyecto [controladores de Microsoft para PHP para SQL Server](https://github.com/Microsoft/msphpsql/releases) github. Cada paquete de instalación contiene archivos de controlador SQLSRV y PDO_SQLSRV en variantes de subproceso y no de subproceso. En Windows, también están disponibles en variantes de 32 y 64 bits. Consulte [requisitos del sistema para los controladores de Microsoft para PHP para obtener SQL Server](../../connect/php/system-requirements-for-the-php-sql-driver.md) para obtener una lista de los archivos de controlador contenidos en cada paquete. El archivo del controlador debe coincidir con la versión, la arquitectura y el subproceso de PHP del entorno PHP.

En Linux y macOS, los controladores se pueden instalar alternativamente mediante PECL, tal y como se encuentra en el [tutorial de instalación](../../connect/php/installation-tutorial-linux-mac.md).

También puede compilar los controladores desde el origen al compilar PHP `phpize`o mediante. Si decide compilar los controladores desde el origen, tiene la opción de compilarlos estáticamente en php en lugar de compilarlos como extensiones compartidas agregando `--enable-sqlsrv=static --with-pdo_sqlsrv=static` (en Linux y MacOS) o `--enable-sqlsrv=static --with-pdo-sqlsrv=static` ( `./configure` en Windows) al comando cuando compilando PHP. Para obtener más información sobre el sistema de compilación `phpize`de PHP y, vea la [documentación de php](http://php.net/manual/install.php).
  
## <a name="moving-the-driver-file-into-your-extension-directory"></a>Traslado del archivo del controlador al directorio de extensión  
El archivo del controlador debe encontrarse en un directorio en el que el tiempo de ejecución de PHP pueda encontrarlo. Es más fácil colocar el archivo del controlador en el directorio de extensión PHP predeterminado: para encontrar el directorio predeterminado, `php -i | sls extension_dir` ejecute en Windows `php -i | grep extension_dir` o en Linux/MacOS. Si no usa el directorio de extensión predeterminado, especifique un directorio en el archivo de configuración de PHP (php. ini) mediante la opción **extension_dir** . Por ejemplo, en Windows, si ha colocado el archivo del controlador en el `c:\php\ext` directorio, agregue la siguiente línea a php. ini:
  
```  
extension_dir = "c:\PHP\ext"  
```

## <a name="loading-the-driver-at-php-startup"></a>Carga del controlador al iniciar PHP  
Para cargar el controlador de SQLSRV cuando se inicie PHP, mueva primero un archivo del controlador al directorio de extensión. A continuación, siga estos pasos:  
  
1.  Para habilitar el controlador **SQLSRV** , modifique **php. ini** agregando la siguiente línea a la sección de extensión, cambiando el nombre de archivo según corresponda:  
  
    En Windows: 
    ```  
    extension=php_sqlsrv_72_ts.dll  
    ```  
    En Linux, si ha descargado los archivos binarios pregenerados para la distribución: 
    ```  
    extension=php_sqlsrv_72_nts.so  
    ```
    Si ha compilado el archivo binario SQLSRV desde el origen o con PECL, en su lugar se denominará sqlsrv.so:
    ```
    extension=sqlsrv.so
    ```
  
2.  Para habilitar el controlador **PDO_SQLSRV** , la extensión de objetos de datos php (PDO) debe estar disponible, ya sea como extensión integrada, o como extensión cargada dinámicamente.

    En Windows, los archivos binarios de PHP prediseñados incorporan PDO, por lo que no es necesario modificar php. ini para cargarlo. Sin embargo, si ha compilado php desde el origen y ha especificado una extensión PDO independiente que se va a compilar `php_pdo.dll`, se denominará, y debe copiarlo en el directorio de extensión y agregar la siguiente línea a php. ini:  
    ```
    extension=php_pdo.dll  
    ```
    En Linux, si ha instalado PHP con el administrador de paquetes del sistema, PDO probablemente se instala como una extensión cargada dinámicamente denominada pdo.so. La extensión PDO debe cargarse antes que la extensión PDO_SQLSRV, o bien se producirá un error de carga. Normalmente, las extensiones se cargan mediante archivos. ini individuales, y estos archivos se leen después de php. ini. Por lo tanto, si pdo.so se carga a través de su propio archivo. ini, se requiere un archivo independiente que cargue el controlador PDO_SQLSRV después de PDO. 

    Para averiguar en qué directorio se encuentran los archivos. ini específicos de la extensión, `php --ini` ejecute y anote el directorio que `Scan for additional .ini files in:`se muestra en. Busque el archivo que carga pdo.so. es probable que tenga como prefijo un número, como 10-PDO. ini. El prefijo numérico indica el orden de carga de los archivos. ini, mientras que los archivos que no tienen un prefijo numérico se cargan alfabéticamente. Cree un archivo para cargar el archivo del controlador PDO_SQLSRV denominado 30-pdo_sqlsrv. ini (cualquier número mayor que el que Prefije a PDO. ini) o PDO_SQLSRV. ini (si PDO. ini no tiene un número como prefijo) y agregue la siguiente línea al mismo, cambiando el nombre de archivo como responda  
    ```
    extension=php_pdo_sqlsrv_72_nts.so
    ```
    Al igual que con SQLSRV, si ha compilado el archivo binario PDO_SQLSRV desde el origen o con PECL, se le denominará PDO_SQLSRV. por lo tanto:
    ```
    extension=pdo_sqlsrv.so
    ```
    Copie este archivo en el directorio que contiene los demás archivos. ini. 

    Si ha compilado PHP desde el código fuente con compatibilidad con PDO integrada, no necesita un archivo. ini independiente y puede Agregar la línea adecuada anterior a php. ini.
  
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
  
