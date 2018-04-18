---
title: SQLConfigDataSource (controlador de archivo de texto) | Documentos de Microsoft
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: odbc
ms.reviewer: ''
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- text file driver [ODBC], SQLConfigDataSource
- SQLConfigDataSource function [ODBC], Text File Driver
ms.assetid: c505d36e-1e72-47b2-a9e5-e4926b408468
caps.latest.revision: 6
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: f3afa8094eb945306fcc74e555f18409f98cfb63
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/16/2018
---
# <a name="sqlconfigdatasource-text-file-driver"></a>SQLConfigDataSource (controlador de archivo de texto)
> [!NOTE]  
>  En este tema se proporciona información específica del controlador de archivo de texto. Para obtener información general acerca de esta función, vea el tema correspondiente en [referencia de la API de ODBC](../../odbc/reference/syntax/odbc-api-reference.md).  
  
 El **SQLConfigDataSource** función que se utiliza para agregar, modificar o eliminar un origen de datos dinámicamente usa las siguientes palabras clave.  
  
|Palabra clave|Description|  
|-------------|-----------------|  
|CHARACTERSET|Para el controlador de texto, OEM o ANSI.|  
|COLNAMEHEADER|En el controlador de texto, indica si el primer registro de datos se especifica los nombres de columna. TRUE o FALSE.|  
|VALOR DE ESTA OPCIÓN|La especificación de ruta de acceso al directorio.|  
|DESCRIPTION|Una descripción de los datos del origen de datos.<br /><br /> Esto establece la misma opción como **descripción** en el cuadro de diálogo de instalación.|  
|DRIVER|La especificación de ruta de acceso a la DLL del controlador.|  
|DRIVERID|Un identificador entero para el controlador. 27 (texto)|  
|EXTENSIONES|Enumera las extensiones de nombre de archivo de los archivos de texto en el origen de datos.<br /><br /> Esto establece la misma opción como **lista de extensiones de** en el cuadro de diálogo de instalación.|  
|FIL|Tipo de archivo de texto|  
|TIPO DE ARCHIVO|Tipo de archivo para el controlador de texto (texto).|  
|FORMAT|En el controlador de texto, puede FIXEDLENGTH, TABDELIMITED, CSVDELIMITED (por una coma) o DELIMITED() (mediante el carácter especial especificado en paréntesis). El carácter especial es un carácter de longitud y puede estar en el formato de caracteres, decimal o hexadecimal.|  
|MAXSCANROWS|El número de filas que deben analizarse al establecer el tipo de datos de una columna en función de los datos existentes.<br /><br /> Para el controlador de texto, puede escribir un número entre 1 y 32767 para el número de filas para buscar; Sin embargo, el valor siempre predeterminado será 25. (Un número que está fuera del límite devolverá un error.)<br /><br /> Esto establece la misma opción como **filas para explorar** en el cuadro de diálogo de instalación.|  
|READONLY|TRUE para que el archivo de solo lectura; FALSE para que el archivo no sea de sólo lectura.<br /><br /> Esto establece la misma opción como **de sólo lectura** en el cuadro de diálogo de instalación.|
