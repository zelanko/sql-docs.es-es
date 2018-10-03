---
title: Opciones de configuración mediante programación para el controlador de Access | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- Access driver [ODBC], setting options programmatically
- ODBC desktop database drivers [ODBC], Access driver
- Jet-based ODBC drivers [ODBC], Access driver
- desktop database drivers [ODBC], Access driver
ms.assetid: 1690eb71-0cd3-4c00-9e15-f6a3ac5316dd
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 5227985c56d5e2fd4730c86fe9182c8b16b2cb02
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/01/2018
ms.locfileid: "47804463"
---
# <a name="setting-options-programmatically-for-the-access-driver"></a>Opciones de configuración mediante programación para el controlador de acceso
|Opción|Descripción|Método|  
|------------|-----------------|------------|  
|Tamaño del búfer|El tamaño del búfer interno, en kilobytes, que es utilizado por Microsoft Access para transferir datos hacia y desde el disco. El tamaño de búfer predeterminado es 2048 KB (se muestra como 2048). Se puede especificar cualquier valor de entero divisible por 256.|Para establecer esta opción dinámicamente, use la palabra clave MAXBUFFERSIZE en una llamada a [SQLConfigDataSource](../../odbc/microsoft/sqlconfigdatasource-access-driver.md).|  
|Data Source Name|Un nombre que identifica el origen de datos, como nóminas o personal.|Para establecer esta opción de forma dinámica, utilice el **DSN** palabra clave en una llamada a [SQLConfigDataSource](../../odbc/microsoft/sqlconfigdatasource-access-driver.md).|  
|Base de datos|Puede configurarse un origen de datos de Microsoft Access sin seleccionar o crear una base de datos. Si no se proporciona ninguna base de datos tras la instalación, se pedirá al usuario elegir un archivo de base de datos al conectarse al origen de datos.|Para establecer esta opción de forma dinámica, utilice el **DBQ** palabra clave en una llamada a [SQLConfigDataSource](../../odbc/microsoft/sqlconfigdatasource-access-driver.md).|  
|Descripción|Una descripción opcional de los datos en el origen de datos Por ejemplo, "Hire date, historial del sueldo y la revisión actual de todos los empleados."|Para establecer esta opción de forma dinámica, utilice el **descripción** palabra clave en una llamada a [SQLConfigDataSource](../../odbc/microsoft/sqlconfigdatasource-access-driver.md).|  
|Exclusivo|Si el **exclusivo** está activada, la base de datos se abrirá en modo exclusivo y puede tener acceso a solo un usuario a la vez. Se mejora el rendimiento cuando se ejecuta en modo exclusivo.|Para establecer esta opción de forma dinámica, utilice el **exclusivo** palabra clave en una llamada a [SQLConfigDataSource](../../odbc/microsoft/sqlconfigdatasource-access-driver.md).|  
|ImplicitCommitSync|Determina cómo se escriben los cambios realizados fuera de una transacción en la base de datos. Inicialmente, este valor se establece en "Sí", lo que significa que esperará el controlador de Microsoft Access para las confirmaciones en una transacción interna y implícita se complete.|Esta opción se incluye en el **establecer opciones avanzadas** cuadro de diálogo para el controlador de Microsoft Access.|  
|Tiempo de espera de página|Especifica el período de tiempo, en milisegundos, que permanece una página (si no usa) en el búfer antes de eliminarse. Para el controlador de Microsoft Access, el valor predeterminado es 500 milisegundos (0,5 segundos). Esta opción se aplica a todos los orígenes de datos que usan el controlador ODBC.<br /><br /> El tiempo de espera de la página no puede ser 0 debido a un retraso inherente. El tiempo de espera de la página no puede ser menor que el retraso inherente, incluso si se establece la opción de tiempo de espera de la página por debajo de ese valor.|Para establecer esta opción de forma dinámica, utilice el **PAGETIMEOUT** palabra clave en una llamada a [SQLConfigDataSource](../../odbc/microsoft/sqlconfigdatasource-access-driver.md).|  
|Solo lectura|La base de datos se designa como de solo lectura.|Para establecer esta opción de forma dinámica, utilice el **READONLY** palabra clave en una llamada a [SQLConfigDataSource](../../odbc/microsoft/sqlconfigdatasource-access-driver.md).|  
|Base de datos del sistema|La ruta de acceso completa de la base de datos del sistema de Microsoft Access para su uso con la base de datos de Microsoft Access que desea tener acceso.<br /><br /> Haga clic en el **base de datos del sistema** para seleccionar la base de datos del sistema que se usará. El controlador ODBC de Microsoft Access solicita al usuario un nombre y una contraseña. El nombre predeterminado es Admin y la contraseña predeterminada de Microsoft Access para el usuario administrador es una cadena vacía.<br /><br /> Para aumentar la seguridad de la base de datos de Microsoft Access, cree un nuevo usuario para reemplazar el usuario administrador y eliminar el usuario administrador o cambiar los objetos a los que el usuario administrador tiene acceso.|Para establecer esta opción de forma dinámica, utilice el **SYSTEMDB** palabra clave en una llamada a [SQLConfigDataSource](../../odbc/microsoft/sqlconfigdatasource-access-driver.md).|  
|Subprocesos|El número de subprocesos en segundo plano para el motor para usar. Para el controlador de Microsoft Access, este valor predeterminado es 3, pero puede cambiarse. El usuario es posible que desee aumentar el número de subprocesos si hay una gran cantidad de actividad en la base de datos.<br /><br /> Esta opción se incluye en el **establecer opciones avanzadas** cuadro de diálogo para el controlador de Microsoft Access.|Para establecer esta opción de forma dinámica, utilice el **subprocesos** palabra clave en una llamada a [SQLConfigDataSource](../../odbc/microsoft/sqlconfigdatasource-access-driver.md).|  
|UserCommitSync|Determina si el controlador de Microsoft Access llevará a cabo una transacciones explícitas definidas por el usuario de forma asincrónica. Inicialmente, este valor se establece en "Sí", lo que significa que esperará el controlador de Microsoft Access para las confirmaciones en una transacción definida por el usuario se complete.<br /><br /> Al establecer esta opción en False, puede tener consecuencias impredecibles en un entorno multiusuario.|Para establecer esta opción de forma dinámica, utilice el **USERCOMMITSYNC** palabra clave en una llamada a [SQLConfigDataSource](../../odbc/microsoft/sqlconfigdatasource-access-driver.md).|
