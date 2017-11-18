---
title: "Sobre los ejemplos de código de la documentación | Documentos de Microsoft"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: php
ms.reviewer: 
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 3f035c37-0f2e-47d4-94e0-a10774402e82
caps.latest.revision: 31
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: d24d29aba9db9d3626a456f87f799e00da1b42cc
ms.contentlocale: es-es
ms.lasthandoff: 09/09/2017

---
# <a name="about-code-examples-in-the-documentation"></a>Sobre los ejemplos de código de la documentación
[!INCLUDE[Driver_PHP_Download](../../includes/driver_php_download.md)]

Hay que tener en cuenta varios puntos al ejecutar los ejemplos de código de la documentación de los [!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)] :  
  
-   En casi todos los ejemplos se da por hecho que SQL Server 2005 o posterior (SQL Server 2008 o posterior si utiliza la versión 3.1) y la base de datos de AdventureWorks están instalados en el equipo local.  
  
    Para obtener información sobre cómo descargar las ediciones gratuitas y de prueba de SQL Server, consulte [SQL Server](http://go.microsoft.com/fwlink/?LinkID=120193).  
  
    Para obtener información sobre cómo descargar la base de datos de AdventureWorks, visite la página [Microsoft SQL Server Samples and Community Projects](http://go.microsoft.com/fwlink/?LinkID=67739)(Proyectos de la comunidad y muestras de Microsoft SQL Server).  
  
    Para obtener información sobre cómo instalar la base de datos de AdventureWorks, consulte [Tutorial: Instalar la base de datos AdventureWorks](http://go.microsoft.com/fwlink/?LinkID=65819).  
  
-   Casi todos los ejemplos de código de esta documentación están diseñados para ejecutarse en la línea de comandos, que habilita las pruebas automatizadas de todos los ejemplos de código. Para obtener información sobre cómo ejecutar PHP en la línea de comandos, consulte [PHP desde la línea de comandos](http://php.net/manual/en/features.commandline.php).  
  
-   Aunque los ejemplos se han diseñado para ejecutarse en la línea de comandos, también puede hacerse desde un explorador sin realizar ningún cambio en el script. Para obtener un formato de salida, reemplace cada "\n" con "\<\/br >" en cada ejemplo antes de invocarlo desde un explorador.  
  
-   Con el fin de que todos los ejemplos sigan siendo específicos para cada caso, no se ha realizado el control de errores correcto. Se recomienda realizar la comprobación de la posible presencia de errores en todas las llamadas a una función de **sqlsrv** o método PDO y controlar tales errores del modo pertinente.  
  
    Se trata de una forma sencilla de obtener información de errores cuando no se sale correctamente de la secuencia de comandos con la siguiente línea de código:  
  
    ```  
    die( print_r( sqlsrv_errors(), true));  
    ```  
  
    Si utiliza PDO:  
  
    ```  
    print_r ($stmt->errorInfo());  
    die();  
    ```  
  
    Para obtener más información sobre el control de errores y advertencias, consulte [Controlar errores y advertencias](../../connect/php/handling-errors-and-warnings.md).  
  
## <a name="see-also"></a>Vea también  
[Información general sobre el controlador SQL para PHP](../../connect/php/overview-of-the-php-sql-driver.md)
  

