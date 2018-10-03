---
title: Opciones de configuración mediante programación para el controlador de Excel | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- Jet-based ODBC drivers [ODBC], Excel driver
- desktop database drivers [ODBC], Excel driver
- ODBC desktop database drivers [ODBC], Excel driver
- Excel driver [ODBC], setting options programmatically
ms.assetid: b5ee3636-4591-427a-a65a-a2d5926fcc1a
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: c62503611e88435b139a00b180d3e087769b7fda
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/01/2018
ms.locfileid: "47786593"
---
# <a name="setting-options-programmatically-for-the-excel-driver"></a>Opciones de configuración mediante programación para el controlador de Excel
|Opción|Descripción|Método|  
|------------|-----------------|------------|  
|Data Source Name|Un nombre que identifica el origen de datos, como nóminas o personal.|Para establecer esta opción de forma dinámica, utilice el **DSN** palabra clave en una llamada a [SQLConfigDataSource](../../odbc/microsoft/odbc-jet-sqlconfigdatasource-excel-driver.md).|  
|Base de datos|Puede configurarse un origen de datos de Microsoft Access sin seleccionar o crear una base de datos. Si no se proporciona ninguna base de datos tras la instalación, se pedirá al usuario elegir un archivo de base de datos al conectarse al origen de datos.|Para establecer esta opción de forma dinámica, utilice el **DBQ** palabra clave en una llamada a [SQLConfigDataSource](../../odbc/microsoft/odbc-jet-sqlconfigdatasource-excel-driver.md).|  
|Descripción|Una descripción opcional de los datos en el origen de datos Por ejemplo, "Hire date, historial del sueldo y la revisión actual de todos los empleados."|Para establecer esta opción de forma dinámica, utilice el **descripción** palabra clave en una llamada a [SQLConfigDataSource](../../odbc/microsoft/odbc-jet-sqlconfigdatasource-excel-driver.md).|  
|Directorio|Muestra el directorio seleccionado actualmente.<br /><br /> Para los archivos de Excel de Microsoft 3.0 y 4.0, la presentación de la ruta de acceso tiene la etiqueta "Directory", mientras que para Microsoft Excel 5.0, 7.0 o 97 archivos, la presentación de la ruta de acceso con la etiqueta "Libro".|Para establecer esta opción de forma dinámica, utilice el **valor de esta opción** palabra clave en una llamada a [SQLConfigDataSource](../../odbc/microsoft/odbc-jet-sqlconfigdatasource-excel-driver.md).|  
|Solo lectura|La base de datos se designa como de solo lectura.|Para establecer esta opción de forma dinámica, utilice el **READONLY** palabra clave en una llamada a [SQLConfigDataSource](../../odbc/microsoft/odbc-jet-sqlconfigdatasource-excel-driver.md).|  
|Filas para explorar|El número de filas que se va a examinar para determinar el tipo de datos de cada columna. El tipo de datos se determina según el número máximo de tipos de datos que se encuentran. Si se encuentran datos que no coincide con el tipo de datos estimado para la columna, se devolverá el tipo de datos como un valor NULL.<br /><br /> Para el controlador de Microsoft Excel, puede escribir un número de 1 a 16 para las filas que se va a analizar. El valor predeterminado es 8; Si se establece en 0, se examinan todas las filas. (Un número fuera del límite devolverá un error).|Para establecer esta opción de forma dinámica, utilice el **MAXSCANROWS** palabra clave en una llamada a [SQLConfigDataSource](../../odbc/microsoft/odbc-jet-sqlconfigdatasource-excel-driver.md).|  
|Seleccionar directorio|Muestra un cuadro de diálogo donde puede seleccionar un directorio que contiene los archivos que desea tener acceso.<br /><br /> Al definir un directorio de origen de datos (para todos los controladores, excepto Microsoft Access), especifique el directorio donde se encuentran los archivos más usados. El controlador ODBC utiliza este directorio como directorio predeterminado. Copie los otros archivos en este directorio si se usan con frecuencia. Como alternativa, puede calificar nombres de archivo en una instrucción SELECT con el nombre del directorio:<br /><br /> SELECCIONE \* DESDE C:\MYDIR\EMP<br /><br /> O bien, puede especificar un nuevo directorio predeterminado mediante el **SQLSetConnectOption** función con la opción SQL_CURRENT_QUALIFIER.<br /><br /> Para Microsoft Excel 3.0 o 4.0 archivos, tiene la etiqueta "Active" la presentación de la ruta de acceso y el botón de selección de la ruta de acceso está etiquetado "Active Directory". Archivos de Microsoft Excel 5.0, 7.0 ó 97, tiene la etiqueta "Libro" la presentación de la ruta de acceso y el botón de selección de la ruta de acceso tiene la etiqueta "Seleccionar libro". Al definir un directorio de origen de datos, especifique el directorio donde los archivos de Excel de Microsoft más usados se encuentran para Microsoft Excel 3.0 o 4.0 o el directorio donde el archivo de libro se encuentra para Microsoft Excel 97, 7.0 o 5.0. **Usar el directorio actual** está deshabilitado para Microsoft Excel 97, 7.0 y 5.0.|Para establecer esta opción de forma dinámica, utilice el **valor de esta opción** palabra clave en una llamada a [SQLConfigDataSource](../../odbc/microsoft/odbc-jet-sqlconfigdatasource-excel-driver.md).|
