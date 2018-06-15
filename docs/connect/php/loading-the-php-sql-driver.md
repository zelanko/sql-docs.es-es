---
title: Carga los controladores de Microsoft para PHP para SQL Server | Documentos de Microsoft
ms.custom: ''
ms.date: 03/26/2018
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- loading the driver
ms.assetid: e5c114c5-8204-49c2-94eb-62ca63f5d3ec
caps.latest.revision: 42
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 8f257439fe011948ac264ac7aea33975abcf06dd
ms.sourcegitcommit: f16003fd1ca28b5e06d5700e730f681720006816
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/11/2018
ms.locfileid: "35308044"
---
# <a name="loading-the-microsoft-drivers-for-php-for-sql-server"></a>Carga de los controladores de Microsoft para PHP para SQL Server
[!INCLUDE[Driver_PHP_Download](../../includes/driver_php_download.md)]

Esta página proporciona instrucciones para cargar el [!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)] en el archivo PHP espacio del proceso.  
  
Puede descargar los controladores creada previamente para su plataforma de la [Microsoft Drivers for PHP para SQL Server](https://github.com/Microsoft/msphpsql/releases) página de Github del proyecto. Cada paquete de instalación contiene los archivos de controlador SQLSRV y PDO_SQLSRV en variantes uniproceso y no un subproceso. En Windows, también están disponibles en las variantes de 32 bits y 64 bits. Vea [requisitos del sistema para Drivers de Microsoft para PHP para SQL Server](../../connect/php/system-requirements-for-the-php-sql-driver.md) para obtener una lista de los archivos de controlador que se encuentran en cada paquete. El archivo del controlador debe coincidir con la versión PHP, la arquitectura y la threadedness de su entorno de PHP.

En Linux y Mac OS, los controladores o bien se pueden instalar mediante PECL, como se encuentra en la [tutorial de instalación](../../connect/php/installation-tutorial-linux-mac.md).
  
## <a name="moving-the-driver-file-into-your-extension-directory"></a>Traslado del archivo del controlador al directorio de extensión  
El archivo del controlador debe encontrarse en un directorio donde encuentre el runtime PHP. Es más fácil para el archivo del controlador se coloca en el directorio de extensión PHP predeterminado - para buscar el directorio predeterminado, ejecute `php -i | sls extension_dir` en Windows o `php -i | grep extension_dir` en Linux/macOS. Si no se usa el directorio de extensión de manera predeterminada, especifique un directorio en el archivo de configuración de PHP (php.ini) mediante la **extension_dir** opción. Por ejemplo, en Windows, si ha colocado el archivo del controlador en su `c:\php\ext` directory, agregue la siguiente línea a php.ini:
  
```  
extension_dir = "c:\PHP\ext"  
```

## <a name="loading-the-driver-at-php-startup"></a>Carga del controlador al iniciar PHP  
Para cargar el controlador SQLSRV cuando se inicia PHP, mueva primero un archivo de controlador al directorio de extensión. A continuación, siga estos pasos:  
  
1.  Para habilitar la **SQLSRV** controlador, modificar **php.ini** agregando la siguiente línea a la sección de extensión, cambiar el nombre de archivo según corresponda:  
  
    En Windows: 
    ```  
    extension=php_sqlsrv_72_ts.dll  
    ```  
    En Linux, si ha descargado los archivos binarios creada previamente para su distribución: 
    ```  
    extension=php_sqlsrv_72_nts.so  
    ```
    Si ha compilado el SQLSRV binario de origen o con PECL, en su lugar, se denomina sqlsrv.so:
    ```
    extension=sqlsrv.so
    ```
  
2.  Para habilitar la **PDO_SQLSRV** controlador, la extensión de los objetos de datos de PHP (PDO) debe estar disponible como extensión integrada o como una extensión cargada dinámicamente.

    En Windows, los binarios PHP predeterminados incluyen PDO integrado, por lo que no es necesario modificar php.ini para cargarla. Si, sin embargo, se compila PHP de origen y especifica una extensión PDO independiente que se crea, se denominará `php_pdo.dll`, y debe copiarlo en el directorio de extensión y agregue la siguiente línea a php.ini:  
    ```
    extension=php_pdo.dll  
    ```
    En Linux, si ha instalado PHP mediante Administrador de paquetes de su sistema, PDO probablemente se instala como una extensión cargada dinámicamente denominada pdo.so. La extensión PDO debe cargarse antes de la extensión PDO_SQLSRV o se producirá un error de carga. Las extensiones se cargan normalmente utilizando los archivos .ini individuales y se leen estos archivos después de php.ini. Por lo tanto, si pdo.so se carga a través de su propio archivo. ini, se requiere un archivo independiente que carga el controlador PDO_SQLSRV después PDO. 

    Para averiguar qué directorio se encuentran los archivos .ini específica de la extensión, ejecute `php --ini` y tenga en cuenta el directorio que aparece en `Scan for additional .ini files in:`. Busque el archivo que carga pdo.so, es probable que viene precedida por un número, como 10 pdo.ini. El prefijo numérico indica el orden de carga de los archivos .ini, mientras se cargan archivos que no tienen un prefijo numérico por orden alfabético. Cree un archivo para cargar el archivo del controlador PDO_SQLSRV llamado a 30-pdo_sqlsrv.ini (cualquier número mayor que la que se antepone a works pdo.ini) o pdo_sqlsrv.ini (si pdo.ini no viene precedida por un número) y agregue la siguiente línea, cambiar el nombre de archivo como apropiados:  
    ```
    extension=php_pdo_sqlsrv_72_nts.so
    ```
    Como con SQLSRV, si ha compilado el PDO_SQLSRV binario de origen o con PECL, en su lugar, se denominará pdo_sqlsrv.so:
    ```
    extension=pdo_sqlsrv.so
    ```
    Copie este archivo en el directorio que contiene los demás archivos ini. 

    Si ha compilado PHP de origen con la compatibilidad integrada de PDO, no necesita un archivo .ini independiente, y puede agregar la línea adecuada anteriormente a php.ini.
  
3.  Reinicie el servidor web.  
  
> [!NOTE]  
> Para determinar si el controlador se ha cargado correctamente, ejecute un script que llame [phpinfo()](http://php.net/manual/en/function.phpinfo.php).  
  
Para obtener más información acerca de **php.ini** directivas, consulte [descripción de las directivas de php.ini core](http://php.net/manual/en/ini.core.php).  
  
## <a name="see-also"></a>Vea también  
[Introducción a los controladores de Microsoft para PHP para SQL Server](../../connect/php/getting-started-with-the-php-sql-driver.md)

[Requisitos del sistema para los controladores de Microsoft para PHP para SQL Server](../../connect/php/system-requirements-for-the-php-sql-driver.md)

[Programación de guía para los controladores de Microsoft para PHP para SQL Server](../../connect/php/programming-guide-for-php-sql-driver.md)

[Referencia de API del controlador SQLSRV](../../connect/php/sqlsrv-driver-api-reference.md)

[Referencia de API del controlador PDO_SQLSRV](../../connect/php/pdo-sqlsrv-driver-reference.md)  
  
