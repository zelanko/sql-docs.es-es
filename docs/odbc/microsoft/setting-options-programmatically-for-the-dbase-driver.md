---
title: "Establecer opciones mediante programación para el controlador dBASE | Documentos de Microsoft"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: odbc
ms.reviewer: 
ms.suite: sql
ms.technology: drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- Jet-based ODBC drivers [ODBC], DBasedriver
- desktop database drivers [ODBC], DBasedriver
- DBase driver [ODBC], setting options programmatically
- ODBC desktop database drivers [ODBC], DBasedriver
ms.assetid: 336d0fd4-5448-4d8c-b7d9-49e857228e36
caps.latest.revision: "7"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 79bf64c2f577935b26dcb64b93e7f3567924291b
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 12/21/2017
---
# <a name="setting-options-programmatically-for-the-dbase-driver"></a>Establecer opciones mediante programación para el controlador dBASE
|Opción|Description|Método|  
|------------|-----------------|------------|  
|Recuento de filas aproximado|Determina si las estadísticas de tamaño de tabla son aproximadas. Esta opción se aplica a todos los orígenes de datos que utilizan el controlador ODBC.|Para establecer esta opción de forma dinámica, utilice el **estadísticas** palabra clave en una llamada a [SQLConfigDataSource](../../odbc/microsoft/sqlconfigdatasource-dbase-driver.md).|  
|Secuencia de intercalación|La secuencia en la que se ordenan los campos.<br /><br /> La secuencia puede ser: ASCII (valor predeterminado) o internacional.|Para establecer esta opción de forma dinámica, utilice el **COLLATINGSEQUENCE** palabra clave en una llamada a [SQLConfigDataSource](../../odbc/microsoft/sqlconfigdatasource-dbase-driver.md).|  
|Data Source Name|Un nombre que identifica el origen de datos, como nóminas o personal.|Para establecer esta opción de forma dinámica, utilice el **DSN** palabra clave en una llamada a [SQLConfigDataSource](../../odbc/microsoft/sqlconfigdatasource-dbase-driver.md).|  
|Base de datos|Un origen de datos de Microsoft Access se puede configurar sin seleccionar o crear una base de datos. Si no se proporciona ninguna base de datos en el programa de instalación, los usuarios se le pedirá que seleccione un archivo de base de datos cuando se conectan al origen de datos.|Para establecer esta opción de forma dinámica, utilice el **DBQ** palabra clave en una llamada a [SQLConfigDataSource](../../odbc/microsoft/sqlconfigdatasource-dbase-driver.md).|  
|Description|Una descripción opcional de los datos en el origen de datos Por ejemplo, "Hire date, historial del sueldo y revisión actual de todos los empleados."|Para establecer esta opción de forma dinámica, utilice el **descripción** palabra clave en una llamada a [SQLConfigDataSource](../../odbc/microsoft/sqlconfigdatasource-dbase-driver.md).|  
|Exclusivo|Si el **exclusivo** está activada, la base de datos se abre en modo exclusivo y puede tener acceso a solo un usuario a la vez. Cuando se ejecuta en modo exclusivo, se mejora rendimiento.|Para establecer esta opción de forma dinámica, utilice el **exclusivo** palabra clave en una llamada a [SQLConfigDataSource](../../odbc/microsoft/sqlconfigdatasource-dbase-driver.md).|  
|Tiempo de espera de página|Especifica el período de tiempo, en décimas de segundo, que una página (si no se utiliza) permanece en el búfer antes de que se quite. El valor predeterminado es 600 décimas de segundo (60 segundos). Esta opción se aplica a todos los orígenes de datos que utilizan el controlador ODBC.<br /><br /> El tiempo de espera de página no puede ser 0 debido a un retraso inherente. El tiempo de espera de página no puede ser menor que el retraso inherente, incluso si se establece la opción de tiempo de espera de página por debajo del valor.|Para establecer esta opción de forma dinámica, utilice el **PAGETIMEOUT** palabra clave en una llamada a [SQLConfigDataSource](../../odbc/microsoft/sqlconfigdatasource-dbase-driver.md).|  
|Solo lectura|Designa la base de datos como de solo lectura.|Para establecer esta opción de forma dinámica, utilice el **READONLY** palabra clave en una llamada a [SQLConfigDataSource](../../odbc/microsoft/sqlconfigdatasource-dbase-driver.md).|  
|Active Directory|Muestra un cuadro de diálogo donde puede seleccionar un directorio que contiene los archivos que desea obtener acceso.<br /><br /> Al definir un directorio de origen de datos, especifique el directorio donde se encuentran los archivos usados con más frecuencia. El controlador ODBC utiliza este directorio como el directorio predeterminado. Copiar otros archivos en este directorio si se usan con frecuencia. Como alternativa, puede calificar nombres de archivo en una instrucción SELECT con el nombre del directorio:<br /><br /> SELECCIONE \* DE C:\MYDIR\EMP<br /><br /> O bien, puede especificar un nuevo directorio predeterminado mediante el **SQLSetConnectOption** función con la opción SQL_CURRENT_QUALIFIER.|Para establecer esta opción de forma dinámica, utilice el **valor de esta opción** palabra clave en una llamada a [SQLConfigDataSource](../../odbc/microsoft/sqlconfigdatasource-dbase-driver.md).|  
|Mostrar filas eliminadas|Especifica si se pueden recuperar o colocados en filas que se han marcado como eliminada. Si está desactivada, no se muestran las filas eliminadas; Si se selecciona, las filas eliminadas se tratan igual que las filas no se han eliminado. El valor predeterminado es desactivada.|Para establecer esta opción de forma dinámica, utilice el **DELETED** palabra clave en una llamada a [SQLConfigDataSource](../../odbc/microsoft/sqlconfigdatasource-dbase-driver.md).|
