---
title: SQLConfigDataSource (controlador de archivo de texto) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- text file driver [ODBC], SQLConfigDataSource
- SQLConfigDataSource function [ODBC], Text File Driver
ms.assetid: c505d36e-1e72-47b2-a9e5-e4926b408468
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 46bb00fb01ed3fee8098420794af089f2d8b981e
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/08/2020
ms.locfileid: "68054084"
---
# <a name="sqlconfigdatasource-text-file-driver"></a>SQLConfigDataSource (controlador de archivo de texto)
> [!NOTE]  
>  En este tema se proporciona información específica del controlador de archivo de texto. Para obtener información general sobre esta función, vea el tema correspondiente en referencia de la [API de ODBC](../../odbc/reference/syntax/odbc-api-reference.md).  
  
 La función **SQLConfigDataSource** que se utiliza para agregar, modificar o eliminar un origen de datos utiliza de forma dinámica las siguientes palabras clave.  
  
|Palabra clave|Descripción|  
|-------------|-----------------|  
|CHARACTERSET|Para el controlador de texto, OEM o ANSI.|  
|COLNAMEHEADER|En el caso del controlador de texto, indica si el primer registro de datos especificará los nombres de columna. ES TRUE o FALSE.|  
|DEFAULTDIR|Especificación de la ruta de acceso al directorio.|  
|Description|Descripción de los datos del origen de datos.<br /><br /> Esto establece la misma opción que la **Descripción** en el cuadro de diálogo de configuración.|  
|DRIVER|Especificación de la ruta de acceso al archivo DLL del controlador.|  
|DRIVERID|IDENTIFICADOR entero para el controlador. 27 (texto)|  
|Extension|Enumera las extensiones de nombre de archivo de los archivos de texto en el origen de datos.<br /><br /> Esto establece la misma opción que la **lista Extensiones** en el cuadro de diálogo de configuración.|  
|FIL|Texto de tipo de archivo|  
|FILETYPE|Tipo de archivo del controlador de texto (texto).|  
|FORMAT|En el caso del controlador de texto, puede ser FIXEDLENGTH, TABDELIMITED, CSVDELIMITED (con una coma) o delimitado (por el carácter especial especificado en los paréntesis). El carácter especial es un carácter de longitud y puede estar en formato de caracteres, decimales o hexadecimales.|  
|MAXSCANROWS|Número de filas que se van a examinar al establecer el tipo de datos de una columna en función de los datos existentes.<br /><br /> En el caso del controlador de texto, puede escribir un número entre 1 y 32767 para el número de filas que se van a examinar; sin embargo, el valor siempre se establecerá de forma predeterminada en 25. (Un número fuera del límite devolverá un error).<br /><br /> Esto establece la misma opción que las **filas que se van a examinar** en el cuadro de diálogo de configuración.|  
|READONLY|TRUE para hacer que el archivo sea de solo lectura; FALSE para que el archivo no sea de solo lectura.<br /><br /> Esto establece la misma opción que **solo lectura** en el cuadro de diálogo de instalación.|
