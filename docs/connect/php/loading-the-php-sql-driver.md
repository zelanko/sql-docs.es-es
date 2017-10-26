---
title: Carga del controlador SQL para PHP | Documentos de Microsoft
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- loading the driver
ms.assetid: e5c114c5-8204-49c2-94eb-62ca63f5d3ec
caps.latest.revision: 42
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Active
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: cb2200b2c5d151981e9dcdf8322dd7c43b91c6ee
ms.contentlocale: es-es
ms.lasthandoff: 09/09/2017

---
# <a name="loading-the-php-sql-driver"></a>Carga del controlador SQL para PHP
[!INCLUDE[Driver_PHP_Download](../../includes/driver_php_download.md)]

En este tema se proporcionan instrucciones para cargar los [!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)] en el espacio del proceso PHP.  
  
Hay dos opciones para cargar un controlador: cuando se inicia PHP o en el runtime del script PHP.  
  
## <a name="moving-the-driver-file-into-your-extension-directory"></a>Traslado del archivo del controlador al directorio de extensión  
Con independencia del procedimiento que se use, el primer paso será colocar el archivo del controlador en un directorio donde se encuentre el runtime PHP. Por lo tanto, coloque el archivo del controlador en el directorio de extensión PHP. Vea [Requisitos del sistema para el controlador SQL para PHP](../../connect/php/system-requirements-for-the-php-sql-driver.md) para obtener una lista de los archivos de controladores que se instalan con los [!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)].  
  
Si es necesario, especifique la ubicación del directorio del archivo del controlador en el archivo de configuración de PHP (php.ini) mediante la **extension_dir** opción. Por ejemplo, si el archivo del controlador se coloca en el directorio c:\php\ext, utilice esta opción:  
  
```  
extension_dir = "c:\PHP\ext"  
```  
  
## <a name="loading-the-driver-at-php-startup"></a>Carga del controlador al iniciar PHP  
Para cargar los [!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)] cuando se inicie PHP, mueva primero un archivo del controlador al directorio de extensión. A continuación, siga estos pasos:  
  
1.  Para habilitar la **SQLSRV** controlador, modificar **php.ini** agregando la línea siguiente a la sección de extensión o modificando la línea que ya existe:  
  
    En Windows (este ejemplo utiliza la versión 4.0 del controlador seguro para subprocesos para PHP 7): 
    ```  
    extension=php_sqlsrv_7_ts.dll  
    ```  
    En Linux (este ejemplo utiliza la versión como instalados por PECL): 
    ```  
    extension=sqlsrv.so  
    ```  
    Para habilitar la **PDO_SQLSRV** controlador, modificar **php.ini** agregando la línea siguiente a la sección de extensión o modificando la línea que ya existe:  
  
    En Windows (este ejemplo utiliza la versión 4.0 del controlador seguro para subprocesos para PHP 7):
    ```  
    extension=php_pdo_sqlsrv_7_ts.dll  
    ```  
    En Linux (este ejemplo utiliza la versión como instalados por PECL):
    ```  
    extension=pdo_sqlsrv.so  
    ```  
  
2.  Si desea utilizar el **PDO_SQLSRV** controlador, la extensión de los objetos de datos de PHP (PDO) debe estar disponible como extensión integrada o como una extensión cargada dinámicamente. Si tiene que cargar el controlador PDO_SQLSRV dinámicamente, el archivo php_pdo.dll (o pdo.so en Linux) debe estar presente en el directorio de extensión y la siguiente línea debe estar en el archivo php.ini:

    En Windows:  
    ```
    extension=php_pdo.dll  
    ```  
    En Linux:  
    ```
    extension=pdo.so  
    ```  
  
3.  Reinicie el servidor web.  
  
> [!NOTE]  
> Para determinar si el controlador se ha cargado correctamente, ejecute un script que llame [phpinfo()](http://go.microsoft.com/fwlink/?LinkId=108678).  
  
Para obtener más información sobre las directivas de **php.ini** , consulte el artículo [Descripción de las directivas del núcleo de php.ini](http://go.microsoft.com/fwlink/?LinkId=105817).  
  
## <a name="loading-the-driver-at-php-script-runtime"></a>Carga del controlador en el runtime del script PHP  
Para cargar los [!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)] en el runtime del script, mueva primero un archivo del controlador al directorio de extensión. A continuación, incluya la línea siguiente al principio del script PHP que coincida con el nombre de archivo del controlador:  
  
```  
dl('php_pdo_sqlsrv_7_ts.dll');  
```  
  
Para obtener más información sobre las funciones PHP relacionadas con la carga dinámica de extensiones, vea [dl](http://go.microsoft.com/fwlink/?LinkId=105818) y [extension_loaded.](http://go.microsoft.com/fwlink/?LinkId=105819)  
  
## <a name="see-also"></a>Vea también  
[Introducción al controlador SQL para PHP](../../connect/php/getting-started-with-the-php-sql-driver.md)
[Requisitos del sistema para el controlador SQL para PHP](../../connect/php/system-requirements-for-the-php-sql-driver.md)
[Guía de programación para el controlador SQL para PHP](../../connect/php/programming-guide-for-php-sql-driver.md)
[Referencia de API del controlador SQLSRV](../../connect/php/sqlsrv-driver-api-reference.md)  
  

