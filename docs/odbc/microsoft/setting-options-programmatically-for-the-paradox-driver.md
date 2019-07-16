---
title: Opciones de configuración mediante programación para el controlador de Paradox | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- ODBC desktop database drivers [ODBC], Paradox driver
- Paradox driver [ODBC], setting options programmatically
- desktop database drivers [ODBC], Paradox driver
- Jet-based ODBC drivers [ODBC], Paradox driver
ms.assetid: 7996d3f8-b5f5-4cac-8a66-fc96a42b603e
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 658d03469e2733b0c25513a4d4a89c6ab88b9852
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/15/2019
ms.locfileid: "68063511"
---
# <a name="setting-options-programmatically-for-the-paradox-driver"></a>Opciones de configuración mediante programación para el controlador de Paradox

|Opción|Descripción|Método|  
|------------|-----------------|------------|  
|Directorio|Establece el directorio de destino.|Para establecer esta opción de forma dinámica, utilice el **valor de esta opción** palabra clave en una llamada a [SQLConfigDataSource](../../odbc/microsoft/sqlconfigdatasource-paradox-driver.md).|  
|Secuencia de intercalación|La secuencia en la que se ordenan los campos.<br /><br /> La secuencia puede ser ASCII (valor predeterminado), internacional, sueco / finlandés o noruego danés.|Para establecer esta opción de forma dinámica, utilice el **COLLATINGSEQUENCE** palabra clave en una llamada a [SQLConfigDataSource](../../odbc/microsoft/sqlconfigdatasource-paradox-driver.md).|  
|Descripción|Una descripción opcional de los datos en el origen de datos Por ejemplo, "Hire date, historial del sueldo y la revisión actual de todos los empleados."|Para establecer esta opción de forma dinámica, utilice el **descripción** palabra clave en una llamada a [SQLConfigDataSource](../../odbc/microsoft/sqlconfigdatasource-paradox-driver.md).|  
|Exclusivo|Si el **exclusivo** está activada, la base de datos se abrirá en modo exclusivo y puede tener acceso a solo un usuario a la vez. Se mejora el rendimiento cuando se ejecuta en modo exclusivo.|Para establecer esta opción de forma dinámica, utilice el **exclusivo** palabra clave en una llamada a [SQLConfigDataSource](../../odbc/microsoft/sqlconfigdatasource-paradox-driver.md).|  
|Estilo de red|El estilo de acceso de red que se utilizará al obtener acceso a datos de Paradox: ya sea "3.*x*" para Paradox 3. *x* o "4. *x*"para Paradox 4. *x* o 5. *x*. Se puede establecer en "3. *x*"o" 4. *x*"si la versión es Paradox 4. *x* o 5. *x*; si la versión 3 de Paradox. *x*, el estilo debe ser "3. *x*".|Para establecer esta opción de forma dinámica, utilice el **PARADOXNETSTYLE** palabra clave en una llamada a [SQLConfigDataSource](../../odbc/microsoft/sqlconfigdatasource-paradox-driver.md).|  
|Tiempo de espera de página|Especifica el período de tiempo, en décimas de segundo, que permanece una página (si no usa) en el búfer antes de eliminarse. El valor predeterminado es 600 décimas de segundo (60 segundos). Esta opción se aplica a todos los orígenes de datos que usan el controlador ODBC.<br /><br /> El tiempo de espera de la página no puede ser 0 debido a un retraso inherente. El tiempo de espera de la página no puede ser menor que el retraso inherente, incluso si se establece la opción de tiempo de espera de la página por debajo de ese valor.|Para establecer esta opción de forma dinámica, utilice el **PAGETIMEOUT** palabra clave en una llamada a [SQLConfigDataSource](../../odbc/microsoft/sqlconfigdatasource-paradox-driver.md).|  
|Solo lectura|La base de datos se designa como de solo lectura.|Para establecer esta opción de forma dinámica, utilice el **READONLY** palabra clave en una llamada a [SQLConfigDataSource](../../odbc/microsoft/sqlconfigdatasource-paradox-driver.md).|  
|Seleccionar directorio|Muestra un cuadro de diálogo donde puede seleccionar un directorio que contiene los archivos que desea tener acceso.<br /><br /> Cuando la definición de un directorio de origen de datos especifica el directorio donde los archivos más utilizados se encuentran. El controlador ODBC utiliza este directorio como directorio predeterminado. Copie los otros archivos en este directorio si se usan con frecuencia. Como alternativa, puede calificar nombres de archivo en una instrucción SELECT con el nombre del directorio:<br /><br /> SELECCIONE \* DESDE C:\MYDIR\EMP<br /><br /> O bien, puede especificar un nuevo directorio predeterminado mediante el **SQLSetConnectOption** función con la opción SQL_CURRENT_QUALIFIER.|Para establecer esta opción de forma dinámica, utilice el **valor de esta opción** palabra clave en una llamada a [SQLConfigDataSource](../../odbc/microsoft/sqlconfigdatasource-paradox-driver.md).|  
|Seleccione el directorio de red|La ruta de acceso completa del directorio que contiene una base de datos de bloqueo de Paradox, ya que contiene el archivo Pdoxusrs.net (en 4 Paradox. *x*) o Paradox.NET (en Paradox 5. *x*). Si el directorio no contiene uno de estos archivos, el controlador de Paradox creará uno. Para obtener información acerca de estos archivos, consulte la documentación de Paradox.<br /><br /> Para poder seleccionar un directorio de red, debe escribir su nombre de usuario Paradox en el **nombre de usuario** cuadro de texto. Haga clic en **Seleccionar directorio de red** para seleccionar un directorio de red.|Para establecer esta opción de forma dinámica, utilice el **PARADOXNETPATH** palabra clave en una llamada a [SQLConfigDataSource](../../odbc/microsoft/sqlconfigdatasource-paradox-driver.md).|  
|Nombre de usuario|El nombre de usuario Paradox. Éste es el nombre que se muestra a otros usuarios de archivos Paradox cuando se encuentre un bloqueo.|Para establecer esta opción de forma dinámica, utilice el **PARADOXUSERNAME** palabra clave en una llamada a [SQLConfigDataSource](../../odbc/microsoft/sqlconfigdatasource-paradox-driver.md).|
