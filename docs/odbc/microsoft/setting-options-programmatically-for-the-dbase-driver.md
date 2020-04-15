---
title: Configuración de opciones mediante programación para el controlador dBASE ? Microsoft Docs
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 75889d9ff3ccfe01f9b8d5141df7774205522815
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/14/2020
ms.locfileid: "81300785"
---
# <a name="setting-options-programmatically-for-the-dbase-driver"></a>Establecer opciones mediante programación para el controlador dBASE

|Opción|Descripción|Método|  
|------------|-----------------|------------|  
|Recuento aproximado de filas|Determina si las estadísticas de tamaño de tabla son aproximadas. Esta opción se aplica a todos los orígenes de datos que usan el controlador ODBC.|Para establecer esta opción dinámicamente, utilice la palabra clave **STATISTICS** en una llamada a [SQLConfigDataSource](../../odbc/microsoft/sqlconfigdatasource-dbase-driver.md).|  
|Secuencia de intercalación|La secuencia en la que se ordenan los campos.<br /><br /> La secuencia puede ser: ASCII (valor predeterminado) o Internacional.|Para establecer esta opción dinámicamente, utilice la palabra clave **COLLATINGSEQUENCE** en una llamada a [SQLConfigDataSource](../../odbc/microsoft/sqlconfigdatasource-dbase-driver.md).|  
|Data Source Name|Nombre que identifica el origen de datos, como Cálculo de nómina o Personal.|Para establecer esta opción dinámicamente, utilice la palabra clave **DSN** en una llamada a [SQLConfigDataSource](../../odbc/microsoft/sqlconfigdatasource-dbase-driver.md).|  
|Base de datos|Un origen de datos de Microsoft Access se puede configurar sin seleccionar ni crear una base de datos. Si no se proporciona ninguna base de datos durante la instalación, se pedirá a los usuarios que seleccionen un archivo de base de datos cuando se conecten al origen de datos.|Para establecer esta opción dinámicamente, utilice la palabra clave **DBQ** en una llamada a [SQLConfigDataSource](../../odbc/microsoft/sqlconfigdatasource-dbase-driver.md).|  
|Descripción|Una descripción opcional de los datos en el origen de datos; por ejemplo, "Fecha de contratación, historial salarial y revisión actual de todos los empleados".|Para establecer esta opción dinámicamente, utilice la palabra clave **DESCRIPTION** en una llamada a [SQLConfigDataSource](../../odbc/microsoft/sqlconfigdatasource-dbase-driver.md).|  
|Exclusivo|Si se selecciona el cuadro **Exclusivo,** la base de datos se abrirá en modo Exclusivo y solo un usuario podrá acceder a ella. El rendimiento se mejora cuando se ejecuta en modo exclusivo.|Para establecer esta opción dinámicamente, utilice la palabra clave **EXCLUSIVE** en una llamada a [SQLConfigDataSource](../../odbc/microsoft/sqlconfigdatasource-dbase-driver.md).|  
|Tiempo de espera de página|Especifica el período de tiempo, en décimas de segundo, que una página (si no se utiliza) permanece en el búfer antes de quitarla. El valor predeterminado es 600 décimas de segundo (60 segundos). Esta opción se aplica a todos los orígenes de datos que usan el controlador ODBC.<br /><br /> El tiempo de espera de página no puede ser 0 debido a un retraso inherente. El tiempo de espera de página no puede ser menor que el retardo inherente, incluso si la opción de tiempo de espera de página se establece por debajo de ese valor.|Para establecer esta opción dinámicamente, utilice la palabra clave **PAGETIMEOUT** en una llamada a [SQLConfigDataSource](../../odbc/microsoft/sqlconfigdatasource-dbase-driver.md).|  
|Solo lectura|Designa la base de datos como de solo lectura.|Para establecer esta opción dinámicamente, utilice la palabra clave **READONLY** en una llamada a [SQLConfigDataSource](../../odbc/microsoft/sqlconfigdatasource-dbase-driver.md).|  
|Seleccione Directorio|Muestra un cuadro de diálogo en el que puede seleccionar un directorio que contenga los archivos a los que desea acceder.<br /><br /> Al definir un directorio de origen de datos, especifique el directorio donde se encuentran los archivos utilizados con más frecuencia. El controlador ODBC utiliza este directorio como directorio predeterminado. Copie otros archivos en este directorio si se utilizan con frecuencia. Como alternativa, puede calificar los nombres de archivo en una instrucción SELECT con el nombre del directorio:<br /><br /> SELECCIONE \* DE C:-MYDIR-EMP<br /><br /> O bien, puede especificar un nuevo directorio predeterminado mediante la función **SQLSetConnectOption** con la opción SQL_CURRENT_QUALIFIER.|Para establecer esta opción dinámicamente, utilice la palabra clave **DEFAULTDIR** en una llamada a [SQLConfigDataSource](../../odbc/microsoft/sqlconfigdatasource-dbase-driver.md).|  
|Mostrar filas eliminadas|Especifica si las filas que se han marcado como eliminadas se pueden recuperar o colocar en. Si está desactivada, no se muestran las filas eliminadas; si se seleccionan, las filas eliminadas se tratan igual que las filas no eliminadas. El valor predeterminado es desactivada.|Para establecer esta opción dinámicamente, utilice la palabra clave **DELETED** en una llamada a [SQLConfigDataSource](../../odbc/microsoft/sqlconfigdatasource-dbase-driver.md).|
