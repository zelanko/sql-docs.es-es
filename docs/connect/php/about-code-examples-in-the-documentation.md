---
title: Sobre los ejemplos de código de la documentación
description: Hay que tener en cuenta varios puntos al ejecutar los ejemplos de código de la documentación sobre los controladores de Microsoft para PHP para SQL Server.
ms.custom: ''
ms.date: 03/26/2018
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 3f035c37-0f2e-47d4-94e0-a10774402e82
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: c90f2f1a420f1ab40f99a2fe83c928890e37e621
ms.sourcegitcommit: 8ffc23126609b1cbe2f6820f9a823c5850205372
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 04/17/2020
ms.locfileid: "81631896"
---
# <a name="about-code-examples-in-the-documentation"></a>Sobre los ejemplos de código de la documentación
[!INCLUDE[Driver_PHP_Download](../../includes/driver_php_download.md)]

## <a name="remarks-about-the-code-examples"></a>Comentarios sobre los ejemplos de código
Hay que tener en cuenta varios puntos al ejecutar los ejemplos de código de la documentación de los [!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)] :  
  
-   En casi todos los ejemplos se da por hecho que SQL Server 2008 o posterior y la base de datos AdventureWorks están instalados en el equipo local.  
  
    Para obtener información sobre cómo descargar las ediciones gratuitas y de prueba de SQL Server, consulte [SQL Server](https://go.microsoft.com/fwlink/?LinkID=120193).  
  
    Para información sobre cómo descargar e instalar la base de datos AdventureWorks, consulte la página [AdventureWorks en el repositorio de GitHub de ejemplos de SQL Server](https://github.com/Microsoft/sql-server-samples/tree/master/samples/databases/adventure-works).
  
-   Casi todos los ejemplos de código de esta documentación están diseñados para ejecutarse en la línea de comandos, que habilita las pruebas automatizadas de todos los ejemplos de código. Para obtener información sobre cómo ejecutar PHP en la línea de comandos, consulte [PHP desde la línea de comandos](https://php.net/manual/en/features.commandline.php).  
  
-   Aunque los ejemplos se han diseñado para ejecutarse en la línea de comandos, también puede hacerse desde un explorador sin realizar ningún cambio en el script. Para obtener un formato de salida correcto, reemplace cada "\n" por "\<\/br>" en cada ejemplo antes de invocarlo desde un explorador.  
  
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
  
    Para obtener más información sobre el control de errores y advertencias, consulte [Controlar errores y advertencias](handling-errors-and-warnings.md).  
  
## <a name="see-also"></a>Consulte también  
[Información general de los controladores de Microsoft para PHP para SQL Server](overview-of-the-php-sql-driver.md)
  
