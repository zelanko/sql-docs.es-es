---
description: ODBC Jet SQLConfigDataSource (controlador de Excel)
title: ODBC jet SQLConfigDataSource (controlador de Excel) | Microsoft Docs
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
ms.openlocfilehash: 61fcc1e7df00f14a7b92e294262b7806382a3d52
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/17/2020
ms.locfileid: "88500308"
---
# <a name="odbc-jet-sqlconfigdatasource-excel-driver"></a>ODBC Jet SQLConfigDataSource (controlador de Excel)
> [!NOTE]  
>  En este tema se proporciona información específica del controlador de Excel. Para obtener información general sobre esta función, vea el tema correspondiente en referencia de la [API de ODBC](../../odbc/reference/syntax/odbc-api-reference.md).  
  
 La función **SQLConfigDataSource** que se utiliza para agregar, modificar o eliminar un origen de datos utiliza de forma dinámica las siguientes palabras clave.  
  
|Palabra clave|Descripción|  
|-------------|-----------------|  
|DBQ|Para el controlador de Microsoft Excel al obtener acceso a los archivos de Microsoft Excel 5,0 o versiones posteriores, el nombre del archivo de libro.<br /><br /> Esto establece la misma opción que la **base de datos** en el cuadro de diálogo de configuración.|  
|DEFAULTDIR|Especificación de la ruta de acceso al directorio.<br /><br /> Esto establece la misma opción que **seleccionar directorio** o **seleccionar libro** en el cuadro de diálogo de configuración.|  
|DESCRIPTION|Descripción de los datos del origen de datos.<br /><br /> Esto establece la misma opción que la **Descripción** en el cuadro de diálogo de configuración.|  
|DRIVER|Especificación de la ruta de acceso al archivo DLL del controlador.|  
|DRIVERID|IDENTIFICADOR entero para el controlador.<br /><br /> 534 (Microsoft Excel 3,0)<br /><br /> 278 (Microsoft Excel 4,0)<br /><br /> 22 (Microsoft Excel 5.0/7.0)<br /><br /> 790 (Microsoft Excel 97-2003)|  
|FIL|Tipo de archivo, por ejemplo, Excel 3,0, Excel 4,0, Excel 5,0, Excel 7,0, Excel 97, Excel 2000 o Excel 2003.|  
|FIRSTROWHASNAMES|Indica si las celdas de la primera fila del intervalo contienen los nombres de columna de la tabla (1) o no (0).|  
|MAXSCANROWS|Número de filas que se van a examinar al establecer el tipo de datos de una columna en función de los datos existentes.<br /><br /> Se puede especificar un número comprendido entre 1 y 16 para las filas que se van a examinar. El valor predeterminado es 8; Si se establece en 0, se examinan todas las filas. (Un número fuera del límite devolverá un error).<br /><br /> Esto establece la misma opción que las **filas que se van a examinar** en el cuadro de diálogo de configuración.|  
|READONLY|TRUE para hacer que el archivo sea de solo lectura; FALSE para que el archivo no sea de solo lectura.<br /><br /> Esto establece la misma opción que **solo lectura** en el cuadro de diálogo de instalación.|  
|THREADPOOL|Número de subprocesos en segundo plano que va a usar el motor. En el caso del controlador de Microsoft Access, este valor tiene como valor predeterminado 3, pero se puede cambiar. En el caso de dBASE, MicrosoftExceldriver este valor es 3 y no se puede cambiar.<br /><br /> Esto establece la misma opción que los **subprocesos** en el cuadro de diálogo de instalación.|
