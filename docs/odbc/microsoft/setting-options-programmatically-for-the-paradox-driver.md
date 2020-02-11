---
title: Establecer opciones mediante programación para el controlador de Paradox | Microsoft Docs
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
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/08/2020
ms.locfileid: "68063511"
---
# <a name="setting-options-programmatically-for-the-paradox-driver"></a>Opciones de configuración mediante programación para el controlador de Paradox

|Opción|Descripción|Método|  
|------------|-----------------|------------|  
|Directory|Establece el directorio de destino.|Para establecer esta opción de forma dinámica, utilice la palabra clave **DEFAULTDIR** en una llamada a [SQLConfigDataSource](../../odbc/microsoft/sqlconfigdatasource-paradox-driver.md).|  
|Secuencia de intercalación|Secuencia en la que se ordenan los campos.<br /><br /> La secuencia puede ser ASCII (valor predeterminado), internacional, Sueco-Finés o noruego-danés.|Para establecer esta opción de forma dinámica, utilice la palabra clave **COLLATINGSEQUENCE** en una llamada a [SQLConfigDataSource](../../odbc/microsoft/sqlconfigdatasource-paradox-driver.md).|  
|Descripción|Una descripción opcional de los datos del origen de datos; por ejemplo, "fecha de contratación, historial de salario y revisión actual de todos los empleados".|Para establecer esta opción de forma dinámica, utilice la palabra clave **Description** en una llamada a [SQLConfigDataSource](../../odbc/microsoft/sqlconfigdatasource-paradox-driver.md).|  
|Exclusivo|Si se selecciona el cuadro **exclusivo** , la base de datos se abrirá en modo exclusivo y solo un usuario podrá acceder a ella a la vez. El rendimiento se mejora cuando se ejecuta en modo exclusivo.|Para establecer esta opción de forma dinámica, utilice la palabra clave **Exclusive** en una llamada a [SQLConfigDataSource](../../odbc/microsoft/sqlconfigdatasource-paradox-driver.md).|  
|Estilo neto|El estilo de acceso a la red que se va a usar al obtener acceso a los datos de Paradox: "3.*x*" para Paradox 3. *x* o "4. *x*"para Paradox 4. *x* o 5. *x*. Se puede establecer en "3. *x*"o" 4. *x*"si la versión es Paradox 4. *x* o 5. *x*; Si la versión es Paradox 3. *x*, el estilo debe ser "3. *x*".|Para establecer esta opción de forma dinámica, utilice la palabra clave **PARADOXNETSTYLE** en una llamada a [SQLConfigDataSource](../../odbc/microsoft/sqlconfigdatasource-paradox-driver.md).|  
|Tiempo de espera de página|Especifica el período de tiempo, en décimas de segundo, que una página (si no se usa) permanece en el búfer antes de quitarse. El valor predeterminado es 600 décimas de segundo (60 segundos). Esta opción se aplica a todos los orígenes de datos que utilizan el controlador ODBC.<br /><br /> El tiempo de espera de la página no puede ser 0 debido a un retraso inherente. El tiempo de espera de la página no puede ser menor que el retraso inherente, aunque la opción de tiempo de espera de la página esté establecida por debajo de ese valor.|Para establecer esta opción de forma dinámica, utilice la palabra clave **PAGETIMEOUT** en una llamada a [SQLConfigDataSource](../../odbc/microsoft/sqlconfigdatasource-paradox-driver.md).|  
|Solo lectura|Designa la base de datos como de solo lectura.|Para establecer esta opción de forma dinámica, utilice la palabra clave **ReadOnly** en una llamada a [SQLConfigDataSource](../../odbc/microsoft/sqlconfigdatasource-paradox-driver.md).|  
|Seleccionar directorio|Muestra un cuadro de diálogo en el que puede seleccionar un directorio que contenga los archivos a los que desea obtener acceso.<br /><br /> Al definir un directorio de origen de datos, especifique el directorio donde se encuentran los archivos que se usan con más frecuencia. El controlador ODBC utiliza este directorio como directorio predeterminado. Copie otros archivos en este directorio si se usan con frecuencia. Como alternativa, puede calificar nombres de archivo en una instrucción SELECT con el nombre de directorio:<br /><br /> SELECT \* from C:\MYDIR\EMP<br /><br /> O bien, puede especificar un nuevo directorio predeterminado mediante la función **SQLSetConnectOption** con la opción SQL_CURRENT_QUALIFIER.|Para establecer esta opción de forma dinámica, utilice la palabra clave **DEFAULTDIR** en una llamada a [SQLConfigDataSource](../../odbc/microsoft/sqlconfigdatasource-paradox-driver.md).|  
|Seleccionar directorio de red|La ruta de acceso completa del directorio que contiene una base de datos de bloqueo de Paradox, ya que contiene el archivo Pdoxusrs.net (en Paradox 4.* x*) o el archivo Paradox.net (en Paradox 5.* x*). Si el directorio no contiene uno de estos archivos, el controlador de Paradox crea uno. Para obtener información acerca de estos archivos, vea la documentación de Paradox.<br /><br /> Para poder seleccionar un directorio de red, debe escribir el nombre de usuario de Paradox en el cuadro de texto **nombre de usuario** . Haga clic en **seleccionar directorio de red** para seleccionar un directorio de red.|Para establecer esta opción de forma dinámica, utilice la palabra clave **PARADOXNETPATH** en una llamada a [SQLConfigDataSource](../../odbc/microsoft/sqlconfigdatasource-paradox-driver.md).|  
|User Name|El nombre de usuario de Paradox. Este es el nombre que se muestra a otros usuarios de archivos de Paradox cuando se encuentra un bloqueo.|Para establecer esta opción de forma dinámica, utilice la palabra clave **PARADOXUSERNAME** en una llamada a [SQLConfigDataSource](../../odbc/microsoft/sqlconfigdatasource-paradox-driver.md).|
