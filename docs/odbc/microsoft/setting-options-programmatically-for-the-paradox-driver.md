---
title: Configuración de opciones mediante programación para el controlador de Paradox ? Microsoft Docs
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: d04de1f0de4baca5b3f474ef9fbcf3f886e6906f
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/14/2020
ms.locfileid: "81300765"
---
# <a name="setting-options-programmatically-for-the-paradox-driver"></a>Opciones de configuración mediante programación para el controlador de Paradox

|Opción|Descripción|Método|  
|------------|-----------------|------------|  
|Directorio|Establece el directorio de destino.|Para establecer esta opción dinámicamente, utilice la palabra clave **DEFAULTDIR** en una llamada a [SQLConfigDataSource](../../odbc/microsoft/sqlconfigdatasource-paradox-driver.md).|  
|Secuencia de intercalación|La secuencia en la que se ordenan los campos.<br /><br /> La secuencia puede ser ASCII (valor predeterminado), Internacional, sueco-finlandés o noruego-danés.|Para establecer esta opción dinámicamente, utilice la palabra clave **COLLATINGSEQUENCE** en una llamada a [SQLConfigDataSource](../../odbc/microsoft/sqlconfigdatasource-paradox-driver.md).|  
|Descripción|Una descripción opcional de los datos en el origen de datos; por ejemplo, "Fecha de contratación, historial salarial y revisión actual de todos los empleados".|Para establecer esta opción dinámicamente, utilice la palabra clave **DESCRIPTION** en una llamada a [SQLConfigDataSource](../../odbc/microsoft/sqlconfigdatasource-paradox-driver.md).|  
|Exclusivo|Si se selecciona el cuadro **Exclusivo,** la base de datos se abrirá en modo Exclusivo y solo un usuario podrá acceder a ella. El rendimiento se mejora cuando se ejecuta en modo exclusivo.|Para establecer esta opción dinámicamente, utilice la palabra clave **EXCLUSIVE** en una llamada a [SQLConfigDataSource](../../odbc/microsoft/sqlconfigdatasource-paradox-driver.md).|  
|Estilo Net|El estilo de acceso a la red que se utilizará al acceder a los datos de Paradox: "3.*x"* para Paradox 3. *x* o "4. *x*" para Paradox 4. *x* o 5. *x*. Se puede establecer en "3. *x"* o "4. *x*" si la versión es Paradox 4. *x* o 5. *x*; si la versión es Paradox 3. *x*, el estilo debe ser "3. *x*".|Para establecer esta opción dinámicamente, utilice la palabra clave **PARADOXNETSTYLE** en una llamada a [SQLConfigDataSource](../../odbc/microsoft/sqlconfigdatasource-paradox-driver.md).|  
|Tiempo de espera de página|Especifica el período de tiempo, en décimas de segundo, que una página (si no se utiliza) permanece en el búfer antes de quitarse. El valor predeterminado es 600 décimas de segundo (60 segundos). Esta opción se aplica a todos los orígenes de datos que usan el controlador ODBC.<br /><br /> El tiempo de espera de página no puede ser 0 debido a un retraso inherente. El tiempo de espera de página no puede ser menor que el retardo inherente, incluso si la opción de tiempo de espera de página se establece por debajo de ese valor.|Para establecer esta opción dinámicamente, utilice la palabra clave **PAGETIMEOUT** en una llamada a [SQLConfigDataSource](../../odbc/microsoft/sqlconfigdatasource-paradox-driver.md).|  
|Solo lectura|Designa la base de datos como de solo lectura.|Para establecer esta opción dinámicamente, utilice la palabra clave **READONLY** en una llamada a [SQLConfigDataSource](../../odbc/microsoft/sqlconfigdatasource-paradox-driver.md).|  
|Seleccione Directorio|Muestra un cuadro de diálogo en el que puede seleccionar un directorio que contenga los archivos a los que desea acceder.<br /><br /> Al definir un directorio de origen de datos, especifique el directorio donde se encuentran los archivos más utilizados. El controlador ODBC utiliza este directorio como directorio predeterminado. Copie otros archivos en este directorio si se utilizan con frecuencia. Como alternativa, puede calificar los nombres de archivo en una instrucción SELECT con el nombre del directorio:<br /><br /> SELECCIONE \* DE C:-MYDIR-EMP<br /><br /> O bien, puede especificar un nuevo directorio predeterminado mediante la función **SQLSetConnectOption** con la opción SQL_CURRENT_QUALIFIER.|Para establecer esta opción dinámicamente, utilice la palabra clave **DEFAULTDIR** en una llamada a [SQLConfigDataSource](../../odbc/microsoft/sqlconfigdatasource-paradox-driver.md).|  
|Seleccione Directorio de red|La ruta de acceso completa del directorio que contiene una base de datos de bloqueo de Paradox, porque contiene el archivo Pdoxusrs.net (en Paradox 4.* x*) o el archivo Paradox.net (en Paradox 5.* x*). Si el directorio no contiene uno de estos archivos, el controlador Paradox crea uno. Para obtener información acerca de estos archivos, consulte la documentación de Paradox.<br /><br /> Para poder seleccionar un directorio de red, debe introducir su nombre de usuario de Paradox en el cuadro de texto Nombre de **usuario.** Haga clic en **Seleccionar directorio** de red para seleccionar un directorio de red.|Para establecer esta opción dinámicamente, utilice la palabra clave **PARADOXNETPATH** en una llamada a [SQLConfigDataSource](../../odbc/microsoft/sqlconfigdatasource-paradox-driver.md).|  
|Nombre de usuario|El nombre de usuario de Paradox. Este es el nombre que se muestra a otros usuarios de archivos Paradox cuando se encuentra un bloqueo.|Para establecer esta opción dinámicamente, utilice la palabra clave **PARADOXUSERNAME** en una llamada a [SQLConfigDataSource](../../odbc/microsoft/sqlconfigdatasource-paradox-driver.md).|
