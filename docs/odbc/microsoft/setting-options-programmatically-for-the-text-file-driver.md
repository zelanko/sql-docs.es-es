---
title: Opciones de configuración mediante programación para el controlador de archivo de texto | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- text file driver [ODBC], setting options programmatically
- ODBC desktop database drivers [ODBC], text file driver
- desktop database drivers [ODBC], text file driver
- Jet-based ODBC drivers [ODBC], text file driver
ms.assetid: cbde2ca1-5d4e-4444-a371-a72f3ac4d92a
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 04bd9a37d87c91fe3f42cbb1fdf464660ba5a299
ms.sourcegitcommit: 1e28f923cda9436a4395a405ebda5149202f8204
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 01/25/2019
ms.locfileid: "55044422"
---
# <a name="setting-options-programmatically-for-the-text-file-driver"></a>Establecer opciones mediante programación para el controlador de archivo de texto

|Opción|Descripción|Método|  
|------------|-----------------|------------|  
|Data Source Name|Un nombre que identifica el origen de datos, como nóminas o personal.|Para establecer esta opción de forma dinámica, utilice el **DSN** palabra clave en una llamada a [SQLConfigDataSource](../../odbc/microsoft/sqlconfigdatasource-text-file-driver.md).|  
|Definir el formato|Muestra el **Definir formato de texto** cuadro de diálogo y le permite especificar el esquema para las tablas individuales en el directorio de origen de datos.|Esta opción no se puede establecer dinámicamente mediante una llamada a [SQLConfigDataSource](../../odbc/microsoft/sqlconfigdatasource-text-file-driver.md).|  
|Descripción|Una descripción opcional de los datos en el origen de datos Por ejemplo, "Hire date, historial del sueldo y la revisión actual de todos los empleados."|Para establecer esta opción de forma dinámica, utilice el **descripción** palabra clave en una llamada a [SQLConfigDataSource](../../odbc/microsoft/sqlconfigdatasource-text-file-driver.md).|  
|Directorio|Selecciona el directorio de destino.|Para establecer esta opción de forma dinámica, utilice el **valor de esta opción** palabra clave en una llamada a [SQLConfigDataSource](../../odbc/microsoft/sqlconfigdatasource-text-file-driver.md).|  
|Lista de extensiones|Enumera las extensiones de nombre de archivo de los archivos de texto en el origen de datos. Cuando se usa el controlador de texto, se crea un archivo sin extensión cuando se ejecuta la instrucción CREATE TABLE con un nombre que no tiene extensión. Otros controladores crean un archivo con una extensión predeterminada cuando no se proporciona ninguna extensión. Para crear un archivo con una extensión .txt, la extensión debe incluirse en el nombre. Para mostrar los archivos sin extensión en el **Definir formato de texto** cuadro de diálogo, "*." debe agregarse a la lista de extensiones.|Para establecer esta opción de forma dinámica, utilice el **extensiones** palabra clave en una llamada a [SQLConfigDataSource](../../odbc/microsoft/sqlconfigdatasource-text-file-driver.md).|  
|Solo lectura|La base de datos se designa como de solo lectura.|Para establecer esta opción de forma dinámica, utilice el **READONLY** palabra clave en una llamada a [SQLConfigDataSource](../../odbc/microsoft/sqlconfigdatasource-text-file-driver.md).|  
|Filas para explorar|El número de filas que se va a examinar para determinar el tipo de datos de cada columna. El tipo de datos se determina según el número máximo de tipos de datos que se encuentran. Si se encuentran datos que no coincide con el tipo de datos estimado para la columna, se devolverá el tipo de datos como un valor NULL.<br /><br /> Para el controlador de texto, se puede especificar un número comprendido entre 1 y 32767 para el número de filas para buscar; Sin embargo, el valor siempre será 25. (Un número fuera del límite devolverá un error).|Para establecer esta opción de forma dinámica, utilice el **MAXSCANROWS** palabra clave en una llamada a [SQLConfigDataSource](../../odbc/microsoft/sqlconfigdatasource-text-file-driver.md).|  
|Seleccionar directorio|Muestra un cuadro de diálogo donde puede seleccionar un directorio que contiene los archivos que desea tener acceso.<br /><br /> Cuando la definición de un directorio de origen de datos especifica el directorio donde los archivos más utilizados se encuentran. El controlador ODBC utiliza este directorio como directorio predeterminado. Copie los otros archivos en este directorio si se usan con frecuencia. Como alternativa, puede calificar nombres de archivo en una instrucción SELECT con el nombre del directorio: `SELECT * FROM C:\MYDIR\EMP`<br /><br /> O bien, puede especificar un nuevo directorio predeterminado mediante el **SQLSetConnectOption** función con la opción SQL_CURRENT_QUALIFIER.|Para establecer esta opción de forma dinámica, utilice el **valor de esta opción** palabra clave en una llamada a [SQLConfigDataSource](../../odbc/microsoft/sqlconfigdatasource-text-file-driver.md).|
