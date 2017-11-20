---
title: "Establecer opciones mediante programación para el controlador de Excel | Documentos de Microsoft"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: microsoft
ms.reviewer: 
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- Jet-based ODBC drivers [ODBC], Excel driver
- desktop database drivers [ODBC], Excel driver
- ODBC desktop database drivers [ODBC], Excel driver
- Excel driver [ODBC], setting options programmatically
ms.assetid: b5ee3636-4591-427a-a65a-a2d5926fcc1a
caps.latest.revision: 6
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: da1f2ed6bbca3709c8223713f4841ed34288f5a3
ms.contentlocale: es-es
ms.lasthandoff: 09/09/2017

---
# <a name="setting-options-programmatically-for-the-excel-driver"></a>Opciones de configuración mediante programación para el controlador de Excel
|Opción|Description|Método|  
|------------|-----------------|------------|  
|Data Source Name|Un nombre que identifica el origen de datos, como nóminas o personal.|Para establecer esta opción de forma dinámica, utilice el **DSN** palabra clave en una llamada a [SQLConfigDataSource](../../odbc/microsoft/odbc-jet-sqlconfigdatasource-excel-driver.md).|  
|Base de datos|Un origen de datos de Microsoft Access se puede configurar sin seleccionar o crear una base de datos. Si no se proporciona ninguna base de datos en el programa de instalación, el usuario se le pedirá que elija un archivo de base de datos cuando se conecte al origen de datos.|Para establecer esta opción de forma dinámica, utilice el **DBQ** palabra clave en una llamada a [SQLConfigDataSource](../../odbc/microsoft/odbc-jet-sqlconfigdatasource-excel-driver.md).|  
|Description|Una descripción opcional de los datos en el origen de datos Por ejemplo, "Hire date, historial del sueldo y revisión actual de todos los empleados."|Para establecer esta opción de forma dinámica, utilice el **descripción** palabra clave en una llamada a [SQLConfigDataSource](../../odbc/microsoft/odbc-jet-sqlconfigdatasource-excel-driver.md).|  
|Directorio|Muestra el directorio seleccionado actualmente.<br /><br /> Para los archivos de Microsoft Excel 3.0 o 4.0, la presentación de la ruta de acceso con la etiqueta "Directory", mientras que para Microsoft Excel 5.0, 7.0 o 97 archivos, la presentación de la ruta de acceso con la etiqueta "Libro".|Para establecer esta opción de forma dinámica, utilice el **valor de esta opción** palabra clave en una llamada a [SQLConfigDataSource](../../odbc/microsoft/odbc-jet-sqlconfigdatasource-excel-driver.md).|  
|Solo lectura|Designa la base de datos como de solo lectura.|Para establecer esta opción de forma dinámica, utilice el **READONLY** palabra clave en una llamada a [SQLConfigDataSource](../../odbc/microsoft/odbc-jet-sqlconfigdatasource-excel-driver.md).|  
|Filas para explorar|El número de filas que se va a examinar para determinar el tipo de datos de cada columna. Se determina el tipo de datos dado el número máximo de tipos de datos que se encuentran. Si se encuentran datos que no coincide con el tipo de datos estimado para la columna, el tipo de datos se devolverán como un valor NULL.<br /><br /> Para el controlador de Microsoft Excel, puede escribir un número de 1 a 16 para las filas que se va a buscar. El valor predeterminado es 8; Si se establece en 0, se examinan todas las filas. (Un número que está fuera del límite devolverá un error.)|Para establecer esta opción de forma dinámica, utilice el **MAXSCANROWS** palabra clave en una llamada a [SQLConfigDataSource](../../odbc/microsoft/odbc-jet-sqlconfigdatasource-excel-driver.md).|  
|Active Directory|Muestra un cuadro de diálogo donde puede seleccionar un directorio que contiene los archivos que desea obtener acceso.<br /><br /> Al definir un directorio de origen de datos (para todos los controladores excepto Microsoft Access), especifique el directorio donde se encuentran los archivos de usados más frecuente. El controlador ODBC utiliza este directorio como el directorio predeterminado. Copiar otros archivos en este directorio si se usan con frecuencia. Como alternativa, puede calificar nombres de archivo en una instrucción SELECT con el nombre del directorio:<br /><br /> SELECCIONE \* DE C:\MYDIR\EMP<br /><br /> O bien, puede especificar un nuevo directorio predeterminado mediante el **SQLSetConnectOption** función con la opción SQL_CURRENT_QUALIFIER.<br /><br /> Para Microsoft Excel 3.0 o 4.0 archivos, la presentación de la ruta de acceso con la etiqueta "Directory" y el botón de selección de la ruta de acceso tiene la etiqueta "Active Directory". Para los archivos de Microsoft Excel 5.0, 7.0 ó 97, la presentación de la ruta de acceso con la etiqueta "Libro" y el botón de selección de la ruta de acceso tiene la etiqueta "Seleccionar libro". Al definir un directorio de origen de datos, especifique el directorio donde se encuentran para Microsoft Excel 3.0 o 4.0 los archivos más usados de Microsoft Excel o el directorio donde se encuentra para Microsoft Excel 5.0, 7.0 ó 97 el archivo de libro. **Usar el directorio actual** está deshabilitado para Microsoft Excel 5.0, 7.0 y 97.|Para establecer esta opción de forma dinámica, utilice el **valor de esta opción** palabra clave en una llamada a [SQLConfigDataSource](../../odbc/microsoft/odbc-jet-sqlconfigdatasource-excel-driver.md).|

