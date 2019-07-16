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
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/15/2019
ms.locfileid: "68054084"
---
# <a name="sqlconfigdatasource-text-file-driver"></a>SQLConfigDataSource (controlador de archivo de texto)
> [!NOTE]  
>  En este tema se proporciona información específica del controlador de archivo de texto. Para obtener información general acerca de esta función, vea el tema correspondiente en [referencia de la API de ODBC](../../odbc/reference/syntax/odbc-api-reference.md).  
  
 El **SQLConfigDataSource** función que se usa para agregar, modificar o eliminar un origen de datos usa dinámicamente las siguientes palabras clave.  
  
|Palabra clave|Descripción|  
|-------------|-----------------|  
|CHARACTERSET|Para el controlador de texto, OEM o ANSI.|  
|COLNAMEHEADER|Para el controlador de texto, indica si el primer registro de datos se especifican los nombres de columna. TRUE o FALSE.|  
|VALOR DE ESTA OPCIÓN|La especificación de ruta de acceso al directorio.|  
|DESCRIPTION|Una descripción de los datos del origen de datos.<br /><br /> Esto establece la misma opción como **descripción** en el cuadro de diálogo programa de instalación.|  
|DRIVER|La especificación de ruta de acceso a la DLL del controlador.|  
|DRIVERID|Un identificador entero para el controlador. 27 (texto)|  
|EXTENSIONES|Enumera las extensiones de nombre de archivo de los archivos de texto en el origen de datos.<br /><br /> Esto establece la misma opción como **lista de extensiones** en el cuadro de diálogo programa de instalación.|  
|FIL|Tipo de archivo texto|  
|TIPO DE ARCHIVO|Tipo de archivo para el controlador de texto (texto).|  
|FORMAT|El controlador de texto, puede ser FIXEDLENGTH, TABDELIMITED, CSVDELIMITED (por una coma) o DELIMITED() (mediante el carácter especial especificado entre paréntesis). El carácter especial es un carácter de longitud y puede estar en el formato de caracteres, decimal o hexadecimal.|  
|MAXSCANROWS|El número de filas a explorar al establecer el tipo de datos de una columna en función de los datos existentes.<br /><br /> Para el controlador de texto, puede escribir un número comprendido entre 1 y 32767 para el número de filas para buscar; Sin embargo, el valor siempre será 25. (Un número fuera del límite devolverá un error).<br /><br /> Esto establece la misma opción como **filas para explorar** en el cuadro de diálogo programa de instalación.|  
|READONLY|TRUE para que el archivo de solo lectura. FALSE para que el archivo no sea de sólo lectura.<br /><br /> Esto establece la misma opción como **de sólo lectura** en el cuadro de diálogo programa de instalación.|
