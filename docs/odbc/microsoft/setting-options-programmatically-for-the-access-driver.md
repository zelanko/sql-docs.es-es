---
title: "Establecer opciones mediante programación para el controlador de acceso | Documentos de Microsoft"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: microsoft
ms.reviewer: 
ms.suite: sql
ms.technology: drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- Access driver [ODBC], setting options programmatically
- ODBC desktop database drivers [ODBC], Access driver
- Jet-based ODBC drivers [ODBC], Access driver
- desktop database drivers [ODBC], Access driver
ms.assetid: 1690eb71-0cd3-4c00-9e15-f6a3ac5316dd
caps.latest.revision: "6"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: ed08d24f96b66b69bbff409cbc2c9e203526041b
ms.sourcegitcommit: 7f8aebc72e7d0c8cff3990865c9f1316996a67d5
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/20/2017
---
# <a name="setting-options-programmatically-for-the-access-driver"></a>Opciones de configuración mediante programación para el controlador de acceso
|Opción|Description|Método|  
|------------|-----------------|------------|  
|Tamaño del búfer|El tamaño del búfer interno en kilobytes, que es utilizado por Microsoft Access para transferir datos hacia y desde el disco. El tamaño de búfer predeterminado es 2048 KB (mostrada como 2048). Se puede especificar cualquier valor de entero divisible por 256.|Para establecer esta opción dinámicamente, utilice la palabra clave MAXBUFFERSIZE en una llamada a [SQLConfigDataSource](../../odbc/microsoft/sqlconfigdatasource-access-driver.md).|  
|Data Source Name|Un nombre que identifica el origen de datos, como nóminas o personal.|Para establecer esta opción de forma dinámica, utilice el **DSN** palabra clave en una llamada a [SQLConfigDataSource](../../odbc/microsoft/sqlconfigdatasource-access-driver.md).|  
|Base de datos|Un origen de datos de Microsoft Access se puede configurar sin seleccionar o crear una base de datos. Si no se proporciona ninguna base de datos en el programa de instalación, el usuario se le pedirá que elija un archivo de base de datos cuando se conecte al origen de datos.|Para establecer esta opción de forma dinámica, utilice el **DBQ** palabra clave en una llamada a [SQLConfigDataSource](../../odbc/microsoft/sqlconfigdatasource-access-driver.md).|  
|Description|Una descripción opcional de los datos en el origen de datos Por ejemplo, "Hire date, historial del sueldo y revisión actual de todos los empleados."|Para establecer esta opción de forma dinámica, utilice el **descripción** palabra clave en una llamada a [SQLConfigDataSource](../../odbc/microsoft/sqlconfigdatasource-access-driver.md).|  
|Exclusivo|Si el **exclusivo** está activada, la base de datos se abre en modo exclusivo y puede tener acceso a solo un usuario a la vez. Cuando se ejecuta en modo exclusivo, se mejora rendimiento.|Para establecer esta opción de forma dinámica, utilice el **exclusivo** palabra clave en una llamada a [SQLConfigDataSource](../../odbc/microsoft/sqlconfigdatasource-access-driver.md).|  
|ImplicitCommitSync|Determina cómo se escriben los cambios realizados fuera de una transacción en la base de datos. Este valor está establecido inicialmente en "Sí", lo que significa que el controlador de Microsoft Access esperará confirmaciones en una transacción interna o implícita se complete.|Esta opción se incluye en el **establecer opciones avanzadas** cuadro de diálogo para el controlador de Microsoft Access.|  
|Tiempo de espera de página|Especifica el período de tiempo, en milisegundos, que una página (si no se utiliza) permanece en el búfer antes de que se va a quitar. El controlador de Microsoft Access, el valor predeterminado es 500 milisegundos (0,5 segundos). Esta opción se aplica a todos los orígenes de datos que utilizan el controlador ODBC.<br /><br /> El tiempo de espera de página no puede ser 0 debido a un retraso inherente. El tiempo de espera de página no puede ser menor que el retraso inherente, incluso si se establece la opción de tiempo de espera de página por debajo del valor.|Para establecer esta opción de forma dinámica, utilice el **PAGETIMEOUT** palabra clave en una llamada a [SQLConfigDataSource](../../odbc/microsoft/sqlconfigdatasource-access-driver.md).|  
|Solo lectura|Designa la base de datos como de solo lectura.|Para establecer esta opción de forma dinámica, utilice el **READONLY** palabra clave en una llamada a [SQLConfigDataSource](../../odbc/microsoft/sqlconfigdatasource-access-driver.md).|  
|Base de datos del sistema|La ruta de acceso completa de la base de datos del sistema de Microsoft Access para su uso con la base de datos de Microsoft Access que desea tener acceso.<br /><br /> Haga clic en el **base de datos del sistema** para seleccionar la base de datos que se usará. El controlador ODBC de Microsoft Access pide al usuario un nombre y una contraseña. El nombre predeterminado es Admin y la contraseña predeterminada en Microsoft Access para el usuario Admin es una cadena vacía.<br /><br /> Para aumentar la seguridad de la base de datos de Microsoft Access, cree un nuevo usuario para reemplazar el usuario administrador y eliminar el usuario administrador o cambiar los objetos a los que el usuario administrador tiene acceso.|Para establecer esta opción de forma dinámica, utilice el **SYSTEMDB** palabra clave en una llamada a [SQLConfigDataSource](../../odbc/microsoft/sqlconfigdatasource-access-driver.md).|  
|Subprocesos|El número de subprocesos en segundo plano para el motor para usar. Para el controlador de Microsoft Access, este valor predeterminado es 3, pero puede cambiarse. El usuario puede querer aumentar el número de subprocesos si hay una gran cantidad de actividad en la base de datos.<br /><br /> Esta opción se incluye en el **establecer opciones avanzadas** cuadro de diálogo para el controlador de Microsoft Access.|Para establecer esta opción de forma dinámica, utilice el **subprocesos** palabra clave en una llamada a [SQLConfigDataSource](../../odbc/microsoft/sqlconfigdatasource-access-driver.md).|  
|UserCommitSync|Determina si el controlador de Microsoft Access llevará a cabo una transacciones explícitas definidas por el usuario de forma asincrónica. Este valor está establecido inicialmente en "Sí", lo que significa que el controlador de Microsoft Access esperará confirmaciones en una transacción definida por el usuario se complete.<br /><br /> Establecer esta opción en False puede tener consecuencias impredecibles en un entorno multiusuario.|Para establecer esta opción de forma dinámica, utilice el **USERCOMMITSYNC** palabra clave en una llamada a [SQLConfigDataSource](../../odbc/microsoft/sqlconfigdatasource-access-driver.md).|
