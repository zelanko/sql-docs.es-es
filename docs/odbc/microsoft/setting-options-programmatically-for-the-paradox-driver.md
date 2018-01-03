---
title: "Establecer opciones mediante programación para el controlador de Paradox | Documentos de Microsoft"
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
- ODBC desktop database drivers [ODBC], Paradox driver
- Paradox driver [ODBC], setting options programmatically
- desktop database drivers [ODBC], Paradox driver
- Jet-based ODBC drivers [ODBC], Paradox driver
ms.assetid: 7996d3f8-b5f5-4cac-8a66-fc96a42b603e
caps.latest.revision: "6"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: b7c881a428d279c4136d3d2422afc6cc79d9d502
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 12/21/2017
---
# <a name="setting-options-programmatically-for-the-paradox-driver"></a>Opciones de configuración mediante programación para el controlador de Paradox
|Opción|Description|Método|  
|------------|-----------------|------------|  
|Directorio|Establece el directorio de destino.|Para establecer esta opción de forma dinámica, utilice el **valor de esta opción** palabra clave en una llamada a [SQLConfigDataSource](../../odbc/microsoft/sqlconfigdatasource-paradox-driver.md).|  
|Secuencia de intercalación|La secuencia en la que se ordenan los campos.<br /><br /> La secuencia puede ser ASCII (valor predeterminado), internacional, sueco / finlandés o noruego danés.|Para establecer esta opción de forma dinámica, utilice el **COLLATINGSEQUENCE** palabra clave en una llamada a [SQLConfigDataSource](../../odbc/microsoft/sqlconfigdatasource-paradox-driver.md).|  
|Description|Una descripción opcional de los datos en el origen de datos Por ejemplo, "Hire date, historial del sueldo y revisión actual de todos los empleados."|Para establecer esta opción de forma dinámica, utilice el **descripción** palabra clave en una llamada a [SQLConfigDataSource](../../odbc/microsoft/sqlconfigdatasource-paradox-driver.md).|  
|Exclusivo|Si el **exclusivo** está activada, la base de datos se abre en modo exclusivo y puede tener acceso a solo un usuario a la vez. Cuando se ejecuta en modo exclusivo, se mejora rendimiento.|Para establecer esta opción de forma dinámica, utilice el **exclusivo** palabra clave en una llamada a [SQLConfigDataSource](../../odbc/microsoft/sqlconfigdatasource-paradox-driver.md).|  
|Estilo de red|El estilo de acceso de red que se utilizará al obtener acceso a datos Paradox: ya sea "3.*x*" para Paradox 3. *x* o "4. *x*"para Paradox 4. *x* ó 5. *x*. Se puede establecer en "3. *x*"o" 4. *x*"si la versión es Paradox 4. *x* ó 5. *x*; si la versión es Paradox 3. *x*, el estilo debe ser "3. *x*".|Para establecer esta opción de forma dinámica, utilice el **PARADOXNETSTYLE** palabra clave en una llamada a [SQLConfigDataSource](../../odbc/microsoft/sqlconfigdatasource-paradox-driver.md).|  
|Tiempo de espera de página|Especifica el período de tiempo, en décimas de segundo, que una página (si no se utiliza) permanece en el búfer antes de que se va a quitar. El valor predeterminado es 600 décimas de segundo (60 segundos). Esta opción se aplica a todos los orígenes de datos que utilizan el controlador ODBC.<br /><br /> El tiempo de espera de página no puede ser 0 debido a un retraso inherente. El tiempo de espera de página no puede ser menor que el retraso inherente, incluso si se establece la opción de tiempo de espera de página por debajo del valor.|Para establecer esta opción de forma dinámica, utilice el **PAGETIMEOUT** palabra clave en una llamada a [SQLConfigDataSource](../../odbc/microsoft/sqlconfigdatasource-paradox-driver.md).|  
|Solo lectura|Designa la base de datos como de solo lectura.|Para establecer esta opción de forma dinámica, utilice el **READONLY** palabra clave en una llamada a [SQLConfigDataSource](../../odbc/microsoft/sqlconfigdatasource-paradox-driver.md).|  
|Active Directory|Muestra un cuadro de diálogo donde puede seleccionar un directorio que contiene los archivos que desea obtener acceso.<br /><br /> Cuando la definición de un directorio de origen de datos especifica el directorio donde los archivos más utilizados se encuentran. El controlador ODBC utiliza este directorio como el directorio predeterminado. Copiar otros archivos en este directorio si se usan con frecuencia. Como alternativa, puede calificar nombres de archivo en una instrucción SELECT con el nombre del directorio:<br /><br /> SELECCIONE \* DE C:\MYDIR\EMP<br /><br /> O bien, puede especificar un nuevo directorio predeterminado mediante el **SQLSetConnectOption** función con la opción SQL_CURRENT_QUALIFIER.|Para establecer esta opción de forma dinámica, utilice el **valor de esta opción** palabra clave en una llamada a [SQLConfigDataSource](../../odbc/microsoft/sqlconfigdatasource-paradox-driver.md).|  
|Seleccione el directorio de red|La ruta de acceso completa del directorio que contiene una base de datos de bloqueo de Paradox, ya que contiene el archivo Pdoxusrs.net (en Paradox 4. *x*) o el archivo Paradox.net (en Paradox 5. *x*). Si el directorio no contiene uno de estos archivos, el controlador de Paradox creará uno. Para obtener información acerca de estos archivos, consulte la documentación de Paradox.<br /><br /> Para poder seleccionar un directorio de red, debe escribir su nombre de usuario Paradox en el **nombre de usuario** cuadro de texto. Haga clic en **seleccione directorio de red** para seleccionar un directorio de red.|Para establecer esta opción de forma dinámica, utilice el **PARADOXNETPATH** palabra clave en una llamada a [SQLConfigDataSource](../../odbc/microsoft/sqlconfigdatasource-paradox-driver.md).|  
|Nombre de usuario|El nombre de usuario Paradox. Este es el nombre que se muestra a otros usuarios de archivos Paradox cuando se encuentre un bloqueo.|Para establecer esta opción de forma dinámica, utilice el **PARADOXUSERNAME** palabra clave en una llamada a [SQLConfigDataSource](../../odbc/microsoft/sqlconfigdatasource-paradox-driver.md).|
