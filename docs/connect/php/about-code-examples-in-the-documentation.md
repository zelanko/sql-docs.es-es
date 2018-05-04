---
title: Sobre los ejemplos de código de la documentación | Documentos de Microsoft
ms.custom: ''
ms.date: 03/26/2018
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: php
ms.reviewer: ''
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: 3f035c37-0f2e-47d4-94e0-a10774402e82
caps.latest.revision: 31
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 331e9e1467eec99368a27402b05e921b087bce1a
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 05/03/2018
---
# <a name="about-code-examples-in-the-documentation"></a>Sobre los ejemplos de código de la documentación
[!INCLUDE[Driver_PHP_Download](../../includes/driver_php_download.md)]

## <a name="remarks-about-the-code-examples"></a>Comentarios acerca de los ejemplos de código
Hay que tener en cuenta varios puntos al ejecutar los ejemplos de código de la documentación de los [!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)] :  
  
-   Casi todos los ejemplos se supone que SQL Server 2008 o posterior y la base de datos de AdventureWorks están instalados en el equipo local.  
  
    Para obtener información sobre cómo descargar las ediciones gratuitas y de prueba de SQL Server, consulte [SQL Server](http://go.microsoft.com/fwlink/?LinkID=120193).  
  
    Para obtener información acerca de cómo descargar e instalar la base de datos de AdventureWorks, vea el [página de AdventureWorks en el repositorio de Github de ejemplos de SQL Server](https://github.com/Microsoft/sql-server-samples/tree/master/samples/databases/adventure-works).
  
-   Casi todos los ejemplos de código de esta documentación están diseñados para ejecutarse en la línea de comandos, que habilita las pruebas automatizadas de todos los ejemplos de código. Para obtener información sobre cómo ejecutar PHP en la línea de comandos, consulte [PHP desde la línea de comandos](http://php.net/manual/en/features.commandline.php).  
  
-   Aunque los ejemplos están diseñados para ejecutarse desde la línea de comandos, cada ejemplo se puede ejecutar mediante la invocación de un explorador sin realizar ningún cambio en la secuencia de comandos. Para aplicar formato al resultado correctamente, reemplace cada "\n" por "\<\/br >" en cada ejemplo antes de invocarlo desde un explorador.  
  
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
[Información general sobre controladores de Microsoft para PHP para SQL Server](../../connect/php/overview-of-the-php-sql-driver.md)
  
