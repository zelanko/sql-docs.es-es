---
title: Establecer opciones mediante programación para el controlador de archivo de texto | Microsoft Docs
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
ms.openlocfilehash: e1a28e5c7ccf3c701e5f97440cd97ed843ab53dd
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/08/2020
ms.locfileid: "68063505"
---
# <a name="setting-options-programmatically-for-the-text-file-driver"></a>Establecer opciones mediante programación para el controlador de archivo de texto

|Opción|Descripción|Método|  
|------------|-----------------|------------|  
|Data Source Name|Nombre que identifica el origen de datos, como por ejemplo, nómina o personal.|Para establecer esta opción de forma dinámica, utilice la palabra clave **DSN** en una llamada a [SQLConfigDataSource](../../odbc/microsoft/sqlconfigdatasource-text-file-driver.md).|  
|Definir formato|Muestra el cuadro de diálogo **definir formato de texto** y permite especificar el esquema de las tablas individuales en el directorio de origen de datos.|Esta opción no se puede establecer dinámicamente mediante una llamada a [SQLConfigDataSource](../../odbc/microsoft/sqlconfigdatasource-text-file-driver.md).|  
|Descripción|Una descripción opcional de los datos del origen de datos; por ejemplo, "fecha de contratación, historial de salario y revisión actual de todos los empleados".|Para establecer esta opción de forma dinámica, utilice la palabra clave **Description** en una llamada a [SQLConfigDataSource](../../odbc/microsoft/sqlconfigdatasource-text-file-driver.md).|  
|Directory|Selecciona el directorio de destino.|Para establecer esta opción de forma dinámica, utilice la palabra clave **DEFAULTDIR** en una llamada a [SQLConfigDataSource](../../odbc/microsoft/sqlconfigdatasource-text-file-driver.md).|  
|Lista de extensiones|Enumera las extensiones de nombre de archivo de los archivos de texto en el origen de datos. Cuando se usa el controlador de texto, se crea un archivo sin extensión cuando se ejecuta la instrucción CREATE TABLE con un nombre que no tiene ninguna extensión. Otros controladores crean un archivo con una extensión predeterminada cuando no se proporciona ninguna extensión. Para crear un archivo con la extensión. txt, la extensión debe incluirse en el nombre. Para mostrar archivos sin extensiones en el cuadro de diálogo **definir formato de texto** , "*." se debe agregar a la lista de extensiones.|Para establecer esta opción de forma dinámica, utilice la palabra clave **extensions** en una llamada a [SQLConfigDataSource](../../odbc/microsoft/sqlconfigdatasource-text-file-driver.md).|  
|Solo lectura|Designa la base de datos como de solo lectura.|Para establecer esta opción de forma dinámica, utilice la palabra clave **ReadOnly** en una llamada a [SQLConfigDataSource](../../odbc/microsoft/sqlconfigdatasource-text-file-driver.md).|  
|Filas que se van a examinar|Número de filas que se van a examinar para determinar el tipo de datos de cada columna. El tipo de datos determina el número máximo de tipos de datos encontrados. Si se encuentran datos que no coinciden con el tipo de datos adivinado para la columna, el tipo de datos se devolverá como un valor NULL.<br /><br /> En el caso del controlador de texto, puede escribir un número comprendido entre 1 y 32767 para el número de filas que se van a examinar; sin embargo, el valor siempre se establecerá de forma predeterminada en 25. (Un número fuera del límite devolverá un error).|Para establecer esta opción de forma dinámica, utilice la palabra clave **MAXSCANROWS** en una llamada a [SQLConfigDataSource](../../odbc/microsoft/sqlconfigdatasource-text-file-driver.md).|  
|Seleccionar directorio|Muestra un cuadro de diálogo en el que puede seleccionar un directorio que contenga los archivos a los que desea obtener acceso.<br /><br /> Al definir un directorio de origen de datos, especifique el directorio donde se encuentran los archivos que se usan con más frecuencia. El controlador ODBC utiliza este directorio como directorio predeterminado. Copie otros archivos en este directorio si se usan con frecuencia. Como alternativa, puede calificar nombres de archivo en una instrucción SELECT con el nombre de directorio:`SELECT * FROM C:\MYDIR\EMP`<br /><br /> O bien, puede especificar un nuevo directorio predeterminado mediante la función **SQLSetConnectOption** con la opción SQL_CURRENT_QUALIFIER.|Para establecer esta opción de forma dinámica, utilice la palabra clave **DEFAULTDIR** en una llamada a [SQLConfigDataSource](../../odbc/microsoft/sqlconfigdatasource-text-file-driver.md).|
