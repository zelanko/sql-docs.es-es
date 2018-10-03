---
title: Carga de los controladores de Microsoft para PHP para SQL Server | Microsoft Docs
ms.custom: ''
ms.date: 03/26/2018
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
manager: craigg
ms.openlocfilehash: eec1a271e10e85c9a22bfa45c75c8ac5efbbf7d6
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MTE75
ms.contentlocale: es-ES
ms.lasthandoff: 10/01/2018
ms.locfileid: "47785624"
---
# <a name="loading-the-microsoft-drivers-for-php-for-sql-server"></a>Carga de los controladores de Microsoft para PHP para SQL Server
[!INCLUDE[Driver_PHP_Download](../../includes/driver_php_download.md)]

En esta página se proporcionan instrucciones para cargar los [!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)] en el espacio del proceso PHP.  
  
Puede descargar los controladores creados previamente para su plataforma desde el [Microsoft Drivers para PHP para SQL Server](https://github.com/Microsoft/msphpsql/releases) página de Github del proyecto. Cada paquete de instalación contiene archivos de controlador PDO_SQLSRV SQLSRV en subprocesos y un subproceso que no son variantes. En Windows, también están disponibles en las variantes de 32 bits y 64 bits. Consulte [requisitos del sistema para el Drivers de Microsoft para PHP para SQL Server](../../connect/php/system-requirements-for-the-php-sql-driver.md) para obtener una lista de los archivos de controlador que se encuentran en cada paquete. El archivo del controlador debe coincidir con la versión PHP, arquitectura y threadedness de su entorno de PHP.

En Linux y macOS, los controladores también se pueden instalar mediante PECL, que se encuentra en la [tutorial de instalación](../../connect/php/installation-tutorial-linux-mac.md).
  
## <a name="moving-the-driver-file-into-your-extension-directory"></a>Traslado del archivo del controlador al directorio de extensión  
El archivo del controlador debe encontrarse en un directorio donde puede encontrar el tiempo de ejecución PHP. Es más fácil colocar el archivo de controlador en el directorio de extensión PHP predeterminado - para encontrar el directorio predeterminado, ejecute `php -i | sls extension_dir` en Windows o `php -i | grep extension_dir` en Linux y macOS. Si no utiliza el directorio de extensión predeterminado, especifique un directorio en el archivo de configuración de PHP (php.ini) mediante el **extension_dir** opción. Por ejemplo, en Windows, si ha colocado el archivo del controlador su `c:\php\ext` directory, agregue la siguiente línea a php.ini:
  
```  
extension_dir = "c:\PHP\ext"  
```

## <a name="loading-the-driver-at-php-startup"></a>Carga del controlador al iniciar PHP  
Para cargar el controlador de SQLSRV cuando se inicie PHP, mueva primero un archivo del controlador al directorio de extensión. A continuación, siga estos pasos:  
  
1.  Para habilitar el **SQLSRV** modificar controlador, **php.ini** agregando la siguiente línea a la sección de extensión, cambiar el nombre de archivo según corresponda:  
  
    En Windows: 
    ```  
    extension=php_sqlsrv_72_ts.dll  
    ```  
    En Linux, si ha descargado los archivos binarios creados previamente para su distribución: 
    ```  
    extension=php_sqlsrv_72_nts.so  
    ```
    Si ha compilado el SQLSRV binario de origen o con PECL, en su lugar, se denominada sqlsrv.so:
    ```
    extension=sqlsrv.so
    ```
  
2.  Para habilitar el **PDO_SQLSRV** controlador, la extensión de los objetos de datos PHP (PDO) debe ser disponible, como una extensión integrada, o como una extensión cargada dinámicamente.

    En Windows, los archivos binarios creados previamente de PHP vienen con PDO integrada, por lo que no hay ninguna necesidad de modificar php.ini para cargarla. Si, sin embargo, ha compilado PHP desde el origen y especifica una extensión PDO independiente que se crea, se denominará `php_pdo.dll`, y debe copiarlo en el directorio de extensión y agregue la siguiente línea a php.ini:  
    ```
    extension=php_pdo.dll  
    ```
    En Linux, si ha instalado PHP mediante Administrador de paquetes de su sistema PDO probablemente se instala como una extensión cargada dinámicamente denominada pdo.so. La extensión PDO debe cargarse antes de la extensión PDO_SQLSRV o se producirá un error de carga. Normalmente se cargan las extensiones mediante los archivos .ini individuales, y estos archivos se leen después php.ini. Por lo tanto, si se carga pdo.so a través de su propio archivo. ini, se requiere un archivo independiente al cargar el controlador PDO_SQLSRV después PDO. 

    Para averiguar qué directorio se encuentran los archivos .ini específica de la extensión, ejecute `php --ini` y tenga en cuenta el directorio enumerado en `Scan for additional .ini files in:`. Busque el archivo que se carga pdo.so, es probable que viene precedida por un número, como 10 pdo.ini. El prefijo numérico indica el orden de carga de los archivos. ini, mientras que los archivos que no tienen un prefijo numérico se cargan por orden alfabético. Cree un archivo para cargar el archivo del controlador PDO_SQLSRV denominado 30-pdo_sqlsrv.ini (cualquier número mayor que la que se antepone a works pdo.ini) o pdo_sqlsrv.ini (si pdo.ini no viene precedida por un número) y agregue la siguiente línea, cambiar el nombre de archivo como adecuado:  
    ```
    extension=php_pdo_sqlsrv_72_nts.so
    ```
    Como con SQLSRV, si ha compilado el binario PDO_SQLSRV desde el origen o con PECL, en su lugar se denominará pdo_sqlsrv.so:
    ```
    extension=pdo_sqlsrv.so
    ```
    Copie este archivo en el directorio que contiene los demás archivos. ini. 

    Si ha compilado PHP de código fuente con compatibilidad integrada con PDO, no necesita un archivo .ini independiente y puede agregar la línea adecuada anteriormente a php.ini.
  
3.  Reinicie el servidor web.  
  
> [!NOTE]  
> Para determinar si el controlador se ha cargado correctamente, ejecute un script que llame a [phpinfo()](http://php.net/manual/en/function.phpinfo.php).  
  
Para obtener más información sobre las directivas de **php.ini**, vea el artículo [Descripción de las directivas del núcleo de php.ini](http://php.net/manual/en/ini.core.php).  
  
## <a name="see-also"></a>Ver también  
[Introducción a los controladores de Microsoft para PHP para SQL Server](../../connect/php/getting-started-with-the-php-sql-driver.md)

[Requisitos del sistema para los controladores de Microsoft para PHP para SQL Server](../../connect/php/system-requirements-for-the-php-sql-driver.md)

[Programación de guía para los controladores de Microsoft para PHP para SQL Server](../../connect/php/programming-guide-for-php-sql-driver.md)

[Referencia de API del controlador SQLSRV](../../connect/php/sqlsrv-driver-api-reference.md)

[Referencia de la API del controlador PDO_SQLSRV](../../connect/php/pdo-sqlsrv-driver-reference.md)  
  
