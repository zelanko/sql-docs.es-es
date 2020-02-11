---
title: Establecer opciones mediante programación para el controlador de Excel | Microsoft Docs
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
ms.openlocfilehash: 47181fca07aff7b2a0d418b8852cfce47cf9e501
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/08/2020
ms.locfileid: "68063526"
---
# <a name="setting-options-programmatically-for-the-excel-driver"></a>Opciones de configuración mediante programación para el controlador de Excel

|Opción|Descripción|Método|  
|------------|-----------------|------------|  
|Data Source Name|Nombre que identifica el origen de datos, como por ejemplo, nómina o personal.|Para establecer esta opción de forma dinámica, utilice la palabra clave **DSN** en una llamada a [SQLConfigDataSource](../../odbc/microsoft/odbc-jet-sqlconfigdatasource-excel-driver.md).|  
|Base de datos|Se puede configurar un origen de datos de Microsoft Access sin necesidad de seleccionar o crear una base de datos. Si no se proporciona ninguna base de datos al realizar la instalación, se le pedirá al usuario que elija un archivo de base de datos al conectarse al origen de datos.|Para establecer esta opción de forma dinámica, utilice la palabra clave **DBQ** en una llamada a [SQLConfigDataSource](../../odbc/microsoft/odbc-jet-sqlconfigdatasource-excel-driver.md).|  
|Descripción|Una descripción opcional de los datos del origen de datos; por ejemplo, "fecha de contratación, historial de salario y revisión actual de todos los empleados".|Para establecer esta opción de forma dinámica, utilice la palabra clave **Description** en una llamada a [SQLConfigDataSource](../../odbc/microsoft/odbc-jet-sqlconfigdatasource-excel-driver.md).|  
|Directory|Muestra el directorio seleccionado actualmente.<br /><br /> En el caso de los archivos de Microsoft Excel 3.0/4.0, la visualización de la ruta de acceso tiene la etiqueta "directorio", mientras que para los archivos de Microsoft Excel 5,0, 7,0 o 97, la presentación de la ruta de acceso tiene la etiqueta "libro".|Para establecer esta opción de forma dinámica, utilice la palabra clave **DEFAULTDIR** en una llamada a [SQLConfigDataSource](../../odbc/microsoft/odbc-jet-sqlconfigdatasource-excel-driver.md).|  
|Solo lectura|Designa la base de datos como de solo lectura.|Para establecer esta opción de forma dinámica, utilice la palabra clave **ReadOnly** en una llamada a [SQLConfigDataSource](../../odbc/microsoft/odbc-jet-sqlconfigdatasource-excel-driver.md).|  
|Filas que se van a examinar|Número de filas que se van a examinar para determinar el tipo de datos de cada columna. El tipo de datos determina el número máximo de tipos de datos encontrados. Si se encuentran datos que no coinciden con el tipo de datos adivinado para la columna, el tipo de datos se devolverá como un valor NULL.<br /><br /> En el caso del controlador de Microsoft Excel, puede escribir un número de 1 a 16 para las filas que se van a examinar. El valor predeterminado es 8; Si se establece en 0, se examinan todas las filas. (Un número fuera del límite devolverá un error).|Para establecer esta opción de forma dinámica, utilice la palabra clave **MAXSCANROWS** en una llamada a [SQLConfigDataSource](../../odbc/microsoft/odbc-jet-sqlconfigdatasource-excel-driver.md).|  
|Seleccionar directorio|Muestra un cuadro de diálogo en el que puede seleccionar un directorio que contenga los archivos a los que desea obtener acceso.<br /><br /> Al definir un directorio de origen de datos (para todos los controladores excepto Microsoft Access), especifique el directorio donde se encuentran los archivos que se usan con más frecuencia. El controlador ODBC utiliza este directorio como directorio predeterminado. Copie otros archivos en este directorio si se usan con frecuencia. Como alternativa, puede calificar nombres de archivo en una instrucción SELECT con el nombre de directorio:<br /><br /> SELECT \* from C:\MYDIR\EMP<br /><br /> O bien, puede especificar un nuevo directorio predeterminado mediante la función **SQLSetConnectOption** con la opción SQL_CURRENT_QUALIFIER.<br /><br /> En el caso de los archivos de Microsoft Excel 3,0 o 4,0, la visualización de la ruta de acceso está etiquetada como "directorio" y el botón de selección de trazado tiene la etiqueta "seleccionar directorio". En el caso de los archivos de Microsoft Excel 5,0, 7,0 o 97, la visualización de la ruta de acceso está etiquetada como "libro" y el botón de selección de trazado tiene la etiqueta "seleccionar libro". Al definir un directorio de origen de datos, especifique el directorio donde se encuentran los archivos de Microsoft Excel más usados para Microsoft Excel 3.0/4.0, o el directorio donde se encuentra el archivo de libro para Microsoft Excel 5,0, 7,0 o 97. **Usar directorio actual** está deshabilitado para Microsoft Excel 5,0, 7,0 y 97.|Para establecer esta opción de forma dinámica, utilice la palabra clave **DEFAULTDIR** en una llamada a [SQLConfigDataSource](../../odbc/microsoft/odbc-jet-sqlconfigdatasource-excel-driver.md).|
