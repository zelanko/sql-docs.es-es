---
title: SQLConfigDataSource (Controlador de archivo de texto) Microsoft Docs
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 2d2809f9b15dd6843e4404c7cf1887c3caa015a3
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/14/2020
ms.locfileid: "81283925"
---
# <a name="sqlconfigdatasource-text-file-driver"></a>SQLConfigDataSource (controlador de archivo de texto)
> [!NOTE]  
>  En este tema se proporciona información específica del controlador de archivo de texto. Para obtener información general sobre esta función, consulte el tema adecuado en Referencia de [la API ODBC](../../odbc/reference/syntax/odbc-api-reference.md).  
  
 La función **SQLConfigDataSource** que se usa para agregar, modificar o eliminar un origen de datos utiliza dinámicamente las siguientes palabras clave.  
  
|Palabra clave|Descripción|  
|-------------|-----------------|  
|CHARACTERSET|Para el controlador de texto, OEM o ANSI.|  
|COLNAMEHEADER|Para el controlador de texto, indica si el primer registro de datos especificará los nombres de columna. TRUE o FALSE.|  
|DEFAULTDIR|La especificación de ruta de acceso al directorio.|  
|DESCRIPTION|Una descripción de los datos en el origen de datos.<br /><br /> Esto establece la misma opción que **Descripción** en el cuadro de diálogo de configuración.|  
|DRIVER|La especificación de ruta de acceso al archivo DLL del controlador.|  
|DRIVERID|Un identificador entero para el controlador. 27 (Texto)|  
|Extensiones|Enumera las extensiones de nombre de archivo de los archivos de texto en el origen de datos.<br /><br /> Esto establece la misma opción que Lista de **extensiones** en el cuadro de diálogo de configuración.|  
|Fil|Tipo de archivo Texto|  
|Eltipo|Tipo de archivo para el controlador de texto (texto).|  
|FORMAT|Para el controlador de texto, puede ser FIXEDLENGTH, TABDELIMITED, CSVDELIMITED (por una coma) o DELIMITED() (por el carácter especial especificado entre paréntesis). El carácter especial tiene un carácter de longitud y puede estar en formato de carácter, decimal o hexadecimal.|  
|MAXSCANROWS|El número de filas que se analizarán al establecer el tipo de datos de una columna en función de los datos existentes.<br /><br /> Para el controlador de texto, puede introducir un número del 1 al 32767 para el número de filas que se van a escanear; sin embargo, el valor siempre se establecerá de forma predeterminada en 25. (Un número fuera del límite devolverá un error.)<br /><br /> Esto establece la misma opción que **Filas para escanear** en el cuadro de diálogo de configuración.|  
|READONLY|TRUE para que el archivo sea de solo lectura; FALSE para que el archivo no sea de solo lectura.<br /><br /> Esto establece la misma opción que **solo lectura** en el cuadro de diálogo de configuración.|
