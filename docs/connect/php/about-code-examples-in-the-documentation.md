---
title: Acerca de los ejemplos de código de la documentación | Microsoft Docs
ms.custom: ''
ms.date: 03/26/2018
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 3f035c37-0f2e-47d4-94e0-a10774402e82
author: MightyPen
ms.author: genemi
ms.openlocfilehash: dc76cee723c11d49a4d6149a7c3a1df4cedbc256
ms.sourcegitcommit: b78f7ab9281f570b87f96991ebd9a095812cc546
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 01/31/2020
ms.locfileid: "68015169"
---
# <a name="about-code-examples-in-the-documentation"></a>Sobre los ejemplos de código de la documentación
[!INCLUDE[Driver_PHP_Download](../../includes/driver_php_download.md)]

## <a name="remarks-about-the-code-examples"></a>Comentarios sobre los ejemplos de código
Hay que tener en cuenta varios puntos al ejecutar los ejemplos de código de la documentación de los [!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)] :  
  
-   En casi todos los ejemplos se da por hecho que SQL Server 2008 o posterior y la base de datos AdventureWorks están instalados en el equipo local.  
  
    Para obtener información sobre cómo descargar las ediciones gratuitas y de prueba de SQL Server, consulte [SQL Server](https://go.microsoft.com/fwlink/?LinkID=120193).  
  
    Para información sobre cómo descargar e instalar la base de datos AdventureWorks, consulte la página [AdventureWorks en el repositorio de GitHub de ejemplos de SQL Server](https://github.com/Microsoft/sql-server-samples/tree/master/samples/databases/adventure-works).
  
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
  
    Para obtener más información sobre el control de errores y advertencias, consulte [Controlar errores y advertencias](../../connect/php/handling-errors-and-warnings.md).  
  
## <a name="see-also"></a>Consulte también  
[Información general de los controladores de Microsoft para PHP para SQL Server](../../connect/php/overview-of-the-php-sql-driver.md)
  
