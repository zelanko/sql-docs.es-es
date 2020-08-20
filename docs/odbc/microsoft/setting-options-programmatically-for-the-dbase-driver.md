---
description: Establecer opciones mediante programación para el controlador dBASE
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 7c4b86b8284ca9a47e3ad40b1680a362035a3f13
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/17/2020
ms.locfileid: "88471587"
---
# <a name="setting-options-programmatically-for-the-dbase-driver"></a>Establecer opciones mediante programación para el controlador dBASE

|Opción|Descripción|Método|  
|------------|-----------------|------------|  
|Recuento de filas aproximado|Determina si las estadísticas de tamaño de tabla se aproximan. Esta opción se aplica a todos los orígenes de datos que utilizan el controlador ODBC.|Para establecer esta opción de forma dinámica, utilice la palabra clave **Statistics** en una llamada a [SQLConfigDataSource](../../odbc/microsoft/sqlconfigdatasource-dbase-driver.md).|  
|Secuencia de intercalación|Secuencia en la que se ordenan los campos.<br /><br /> La secuencia puede ser: ASCII (valor predeterminado) o internacional.|Para establecer esta opción de forma dinámica, utilice la palabra clave **COLLATINGSEQUENCE** en una llamada a [SQLConfigDataSource](../../odbc/microsoft/sqlconfigdatasource-dbase-driver.md).|  
|Data Source Name|Nombre que identifica el origen de datos, como por ejemplo, nómina o personal.|Para establecer esta opción de forma dinámica, utilice la palabra clave **DSN** en una llamada a [SQLConfigDataSource](../../odbc/microsoft/sqlconfigdatasource-dbase-driver.md).|  
|Base de datos|Se puede configurar un origen de datos de Microsoft Access sin necesidad de seleccionar o crear una base de datos. Si no se proporciona ninguna base de datos al realizar la instalación, se pedirá a los usuarios que seleccionen un archivo de base de datos cuando se conecten al origen de datos.|Para establecer esta opción de forma dinámica, utilice la palabra clave **DBQ** en una llamada a [SQLConfigDataSource](../../odbc/microsoft/sqlconfigdatasource-dbase-driver.md).|  
|Descripción|Una descripción opcional de los datos del origen de datos; por ejemplo, "fecha de contratación, historial de salario y revisión actual de todos los empleados".|Para establecer esta opción de forma dinámica, utilice la palabra clave **Description** en una llamada a [SQLConfigDataSource](../../odbc/microsoft/sqlconfigdatasource-dbase-driver.md).|  
|Exclusivo|Si se selecciona el cuadro **exclusivo** , la base de datos se abrirá en modo exclusivo y solo un usuario podrá acceder a ella a la vez. El rendimiento se mejora cuando se ejecuta en modo exclusivo.|Para establecer esta opción de forma dinámica, utilice la palabra clave **Exclusive** en una llamada a [SQLConfigDataSource](../../odbc/microsoft/sqlconfigdatasource-dbase-driver.md).|  
|Tiempo de espera de página|Especifica el período de tiempo, en décimas de segundo, que una página (si no se usa) permanece en el búfer antes de que se quite. El valor predeterminado es 600 décimas de segundo (60 segundos). Esta opción se aplica a todos los orígenes de datos que utilizan el controlador ODBC.<br /><br /> El tiempo de espera de la página no puede ser 0 debido a un retraso inherente. El tiempo de espera de la página no puede ser menor que el retraso inherente, aunque la opción de tiempo de espera de la página esté establecida por debajo de ese valor.|Para establecer esta opción de forma dinámica, utilice la palabra clave **PAGETIMEOUT** en una llamada a [SQLConfigDataSource](../../odbc/microsoft/sqlconfigdatasource-dbase-driver.md).|  
|Solo lectura|Designa la base de datos como de solo lectura.|Para establecer esta opción de forma dinámica, utilice la palabra clave **ReadOnly** en una llamada a [SQLConfigDataSource](../../odbc/microsoft/sqlconfigdatasource-dbase-driver.md).|  
|Seleccionar directorio|Muestra un cuadro de diálogo en el que puede seleccionar un directorio que contenga los archivos a los que desea obtener acceso.<br /><br /> Al definir un directorio de origen de datos, especifique el directorio donde se encuentran los archivos que se usan con más frecuencia. El controlador ODBC utiliza este directorio como directorio predeterminado. Copie otros archivos en este directorio si se usan con frecuencia. Como alternativa, puede calificar nombres de archivo en una instrucción SELECT con el nombre de directorio:<br /><br /> SELECT \* from C:\MYDIR\EMP<br /><br /> O bien, puede especificar un nuevo directorio predeterminado mediante la función **SQLSetConnectOption** con la opción SQL_CURRENT_QUALIFIER.|Para establecer esta opción de forma dinámica, utilice la palabra clave **DEFAULTDIR** en una llamada a [SQLConfigDataSource](../../odbc/microsoft/sqlconfigdatasource-dbase-driver.md).|  
|Mostrar filas eliminadas|Especifica si las filas que se han marcado como eliminadas se pueden recuperar o colocar en. Si está desactivada, no se muestran las filas eliminadas; Si se selecciona, las filas eliminadas se tratan igual que las filas no eliminadas. El valor predeterminado es desactivada.|Para establecer esta opción de forma dinámica, utilice la palabra clave **Deleted** en una llamada a [SQLConfigDataSource](../../odbc/microsoft/sqlconfigdatasource-dbase-driver.md).|
