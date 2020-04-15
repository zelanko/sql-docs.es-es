---
title: ODBC Jet SQLConfigDataSource (controlador de Excel) Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SQLConfigDataSource function [ODBC], Excel Driver
- Excel driver [ODBC], SqlConfigDataSource
ms.assetid: 885b3bea-f4b6-4902-b994-f78a912b612f
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: a76482acd1182d900336d7ac9826b16968e00caa
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/14/2020
ms.locfileid: "81293015"
---
# <a name="odbc-jet-sqlconfigdatasource-excel-driver"></a>ODBC Jet SQLConfigDataSource (controlador de Excel)
> [!NOTE]  
>  En este tema se proporciona información específica del controlador de Excel. Para obtener información general sobre esta función, consulte el tema adecuado en Referencia de [la API ODBC](../../odbc/reference/syntax/odbc-api-reference.md).  
  
 La función **SQLConfigDataSource** que se usa para agregar, modificar o eliminar un origen de datos utiliza dinámicamente las siguientes palabras clave.  
  
|Palabra clave|Descripción|  
|-------------|-----------------|  
|DBQ|Para el controlador de Microsoft Excel al acceder a archivos de Microsoft Excel 5.0 o posterior, el nombre del archivo de libro.<br /><br /> Esto establece la misma opción que **Base de datos** en el cuadro de diálogo de configuración.|  
|DEFAULTDIR|La especificación de ruta de acceso al directorio.<br /><br /> Esto establece la misma opción que **Seleccionar directorio** o Seleccionar libro de **trabajo** en el cuadro de diálogo de configuración.|  
|DESCRIPTION|Una descripción de los datos en el origen de datos.<br /><br /> Esto establece la misma opción que **Descripción** en el cuadro de diálogo de configuración.|  
|DRIVER|La especificación de ruta de acceso al archivo DLL del controlador.|  
|DRIVERID|Un identificador entero para el controlador.<br /><br /> 534 (Microsoft Excel 3.0)<br /><br /> 278 (Microsoft Excel 4.0)<br /><br /> 22 (Microsoft Excel 5.0/7.0)<br /><br /> 790 (Microsoft Excel 97-2003)|  
|Fil|Tipo de archivo, por ejemplo, Excel 3.0, Excel 4.0, Excel 5.0, Excel 7.0, Excel 97, Excel 2000 o Excel 2003.|  
|FIRSTROWHASNAMES|Indica si las celdas de la primera fila del rango contienen los nombres de columna para la tabla (1) o no (0).|  
|MAXSCANROWS|El número de filas que se analizarán al establecer el tipo de datos de una columna en función de los datos existentes.<br /><br /> Se puede introducir un número del 1 al 16 para que las filas se escaneen. El valor predeterminado es 8; si se establece en 0, se analizan todas las filas. (Un número fuera del límite devolverá un error.)<br /><br /> Esto establece la misma opción que **Filas para escanear** en el cuadro de diálogo de configuración.|  
|READONLY|TRUE para que el archivo sea de solo lectura; FALSE para que el archivo no sea de solo lectura.<br /><br /> Esto establece la misma opción que **solo lectura** en el cuadro de diálogo de configuración.|  
|Hilos|El número de subprocesos en segundo plano que va a utilizar el motor. Para el controlador de Microsoft Access, este valor predeterminado es 3, pero se puede cambiar. Para dBASE, MicrosoftExceldriver este valor es 3 y no se puede cambiar.<br /><br /> Esto establece la misma opción que **subprocesos** en el cuadro de diálogo de configuración.|
