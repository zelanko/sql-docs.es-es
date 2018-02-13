---
title: "Establecer opciones mediante programación para el controlador de archivo de texto | Documentos de Microsoft"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: odbc
ms.reviewer: 
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- text file driver [ODBC], setting options programmatically
- ODBC desktop database drivers [ODBC], text file driver
- desktop database drivers [ODBC], text file driver
- Jet-based ODBC drivers [ODBC], text file driver
ms.assetid: cbde2ca1-5d4e-4444-a371-a72f3ac4d92a
caps.latest.revision: 
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: d1a7f971a0ac5d07c451b9a786bdcc563108e3f7
ms.sourcegitcommit: f02598eb8665a9c2dc01991c36f27943701fdd2d
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/13/2018
---
# <a name="setting-options-programmatically-for-the-text-file-driver"></a>Establecer opciones mediante programación para el controlador de archivo de texto
|Opción|Description|Método|  
|------------|-----------------|------------|  
|Data Source Name|Un nombre que identifica el origen de datos, como nóminas o personal.|Para establecer esta opción de forma dinámica, utilice el **DSN** palabra clave en una llamada a [SQLConfigDataSource](../../odbc/microsoft/sqlconfigdatasource-text-file-driver.md).|  
|Definir formato|Muestra el **Definir formato de texto** cuadro de diálogo y le permite especificar el esquema para las tablas individuales en el directorio de origen de datos.|Esta opción no se puede establecer dinámicamente mediante una llamada a [SQLConfigDataSource](../../odbc/microsoft/sqlconfigdatasource-text-file-driver.md).|  
|Description|Una descripción opcional de los datos en el origen de datos Por ejemplo, "Hire date, historial del sueldo y revisión actual de todos los empleados."|Para establecer esta opción de forma dinámica, utilice el **descripción** palabra clave en una llamada a [SQLConfigDataSource](../../odbc/microsoft/sqlconfigdatasource-text-file-driver.md).|  
|Directorio|Selecciona el directorio de destino.|Para establecer esta opción de forma dinámica, utilice el **valor de esta opción** palabra clave en una llamada a [SQLConfigDataSource](../../odbc/microsoft/sqlconfigdatasource-text-file-driver.md).|  
|Lista de extensiones|Enumera las extensiones de nombre de archivo de los archivos de texto en el origen de datos. Cuando se utiliza el controlador de texto, se crea un archivo sin extensión cuando se ejecuta la instrucción CREATE TABLE con un nombre que no tiene ninguna extensión. Otros controladores de crean un archivo con una extensión predeterminada cuando no se proporciona ninguna extensión. Para crear un archivo con una extensión. txt, la extensión debe incluirse en el nombre. Para mostrar archivos sin extensión en el **Definir formato de texto** cuadro de diálogo, "*." deben agregarse a la lista de extensiones.|Para establecer esta opción de forma dinámica, utilice el **extensiones** palabra clave en una llamada a [SQLConfigDataSource](../../odbc/microsoft/sqlconfigdatasource-text-file-driver.md).|  
|Solo lectura|Designa la base de datos como de solo lectura.|Para establecer esta opción de forma dinámica, utilice el **READONLY** palabra clave en una llamada a [SQLConfigDataSource](../../odbc/microsoft/sqlconfigdatasource-text-file-driver.md).|  
|Filas para explorar|El número de filas que se va a examinar para determinar el tipo de datos de cada columna. Se determina el tipo de datos dado el número máximo de tipos de datos que se encuentran. Si se encuentran datos que no coincide con el tipo de datos estimado para la columna, el tipo de datos se devolverán como un valor NULL.<br /><br /> Para el controlador de texto, se puede especificar un número entre 1 y 32767 para el número de filas para buscar; Sin embargo, el valor siempre predeterminado será 25. (Un número que está fuera del límite devolverá un error.)|Para establecer esta opción de forma dinámica, utilice el **MAXSCANROWS** palabra clave en una llamada a [SQLConfigDataSource](../../odbc/microsoft/sqlconfigdatasource-text-file-driver.md).|  
|Active Directory|Muestra un cuadro de diálogo donde puede seleccionar un directorio que contiene los archivos que desea obtener acceso.<br /><br /> Cuando la definición de un directorio de origen de datos especifica el directorio donde los archivos más utilizados se encuentran. El controlador ODBC utiliza este directorio como el directorio predeterminado. Copiar otros archivos en este directorio si se usan con frecuencia. Como alternativa, puede calificar nombres de archivo en una instrucción SELECT con el nombre del directorio: `SELECT * FROM C:\MYDIR\EMP`<br /><br /> O bien, puede especificar un nuevo directorio predeterminado mediante el **SQLSetConnectOption** función con la opción SQL_CURRENT_QUALIFIER.|Para establecer esta opción de forma dinámica, utilice el **valor de esta opción** palabra clave en una llamada a [SQLConfigDataSource](../../odbc/microsoft/sqlconfigdatasource-text-file-driver.md).|
