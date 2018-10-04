---
title: Establecer opciones mediante programación para el controlador dBASE | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- Jet-based ODBC drivers [ODBC], DBasedriver
- desktop database drivers [ODBC], DBasedriver
- DBase driver [ODBC], setting options programmatically
- ODBC desktop database drivers [ODBC], DBasedriver
ms.assetid: 336d0fd4-5448-4d8c-b7d9-49e857228e36
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: dd5ebd223c3b4a15193f6ce5f9f8aa8bf03170f8
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/01/2018
ms.locfileid: "47745893"
---
# <a name="setting-options-programmatically-for-the-dbase-driver"></a>Establecer opciones mediante programación para el controlador dBASE
|Opción|Descripción|Método|  
|------------|-----------------|------------|  
|Recuento de filas aproximado|Determina si se aproximan las estadísticas de tamaño de tabla. Esta opción se aplica a todos los orígenes de datos que usan el controlador ODBC.|Para establecer esta opción de forma dinámica, utilice el **estadísticas** palabra clave en una llamada a [SQLConfigDataSource](../../odbc/microsoft/sqlconfigdatasource-dbase-driver.md).|  
|Secuencia de intercalación|La secuencia en la que se ordenan los campos.<br /><br /> La secuencia puede ser: ASCII (valor predeterminado) o internacional.|Para establecer esta opción de forma dinámica, utilice el **COLLATINGSEQUENCE** palabra clave en una llamada a [SQLConfigDataSource](../../odbc/microsoft/sqlconfigdatasource-dbase-driver.md).|  
|Data Source Name|Un nombre que identifica el origen de datos, como nóminas o personal.|Para establecer esta opción de forma dinámica, utilice el **DSN** palabra clave en una llamada a [SQLConfigDataSource](../../odbc/microsoft/sqlconfigdatasource-dbase-driver.md).|  
|Base de datos|Puede configurarse un origen de datos de Microsoft Access sin seleccionar o crear una base de datos. Si no se proporciona ninguna base de datos tras la instalación, se solicitará a los usuarios seleccionar un archivo de base de datos cuando se conectan al origen de datos.|Para establecer esta opción de forma dinámica, utilice el **DBQ** palabra clave en una llamada a [SQLConfigDataSource](../../odbc/microsoft/sqlconfigdatasource-dbase-driver.md).|  
|Descripción|Una descripción opcional de los datos en el origen de datos Por ejemplo, "Hire date, historial del sueldo y la revisión actual de todos los empleados."|Para establecer esta opción de forma dinámica, utilice el **descripción** palabra clave en una llamada a [SQLConfigDataSource](../../odbc/microsoft/sqlconfigdatasource-dbase-driver.md).|  
|Exclusivo|Si el **exclusivo** está activada, la base de datos se abrirá en modo exclusivo y puede tener acceso a solo un usuario a la vez. Se mejora el rendimiento cuando se ejecuta en modo exclusivo.|Para establecer esta opción de forma dinámica, utilice el **exclusivo** palabra clave en una llamada a [SQLConfigDataSource](../../odbc/microsoft/sqlconfigdatasource-dbase-driver.md).|  
|Tiempo de espera de página|Especifica el período de tiempo, en décimas de segundo, que permanece una página (si no usa) en el búfer antes de quitarlo. El valor predeterminado es 600 décimas de segundo (60 segundos). Esta opción se aplica a todos los orígenes de datos que usan el controlador ODBC.<br /><br /> El tiempo de espera de la página no puede ser 0 debido a un retraso inherente. El tiempo de espera de la página no puede ser menor que el retraso inherente, incluso si se establece la opción de tiempo de espera de la página por debajo de ese valor.|Para establecer esta opción de forma dinámica, utilice el **PAGETIMEOUT** palabra clave en una llamada a [SQLConfigDataSource](../../odbc/microsoft/sqlconfigdatasource-dbase-driver.md).|  
|Solo lectura|La base de datos se designa como de solo lectura.|Para establecer esta opción de forma dinámica, utilice el **READONLY** palabra clave en una llamada a [SQLConfigDataSource](../../odbc/microsoft/sqlconfigdatasource-dbase-driver.md).|  
|Seleccionar directorio|Muestra un cuadro de diálogo donde puede seleccionar un directorio que contiene los archivos que desea tener acceso.<br /><br /> Al definir un directorio de origen de datos, especifique el directorio donde se encuentran los archivos que se usan con más frecuencia. El controlador ODBC utiliza este directorio como directorio predeterminado. Copie los otros archivos en este directorio si se usan con frecuencia. Como alternativa, puede calificar nombres de archivo en una instrucción SELECT con el nombre del directorio:<br /><br /> SELECCIONE \* DESDE C:\MYDIR\EMP<br /><br /> O bien, puede especificar un nuevo directorio predeterminado mediante el **SQLSetConnectOption** función con la opción SQL_CURRENT_QUALIFIER.|Para establecer esta opción de forma dinámica, utilice el **valor de esta opción** palabra clave en una llamada a [SQLConfigDataSource](../../odbc/microsoft/sqlconfigdatasource-dbase-driver.md).|  
|Mostrar las filas eliminadas|Especifica si se pueden recuperar o colocadas en las filas que se han marcado como eliminado. Si está desactivada, no se muestran las filas eliminadas; Si se selecciona, las filas eliminadas se tratan igual que las filas no eliminados. El valor predeterminado es desactivada.|Para establecer esta opción de forma dinámica, utilice el **DELETED** palabra clave en una llamada a [SQLConfigDataSource](../../odbc/microsoft/sqlconfigdatasource-dbase-driver.md).|
