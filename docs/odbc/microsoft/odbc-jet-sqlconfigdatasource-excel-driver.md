---
title: ODBC Jet SQLConfigDataSource (controlador de Excel) | Documentos de Microsoft
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- SQLConfigDataSource function [ODBC], Excel Driver
- Excel driver [ODBC], SqlConfigDataSource
ms.assetid: 885b3bea-f4b6-4902-b994-f78a912b612f
caps.latest.revision: 8
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 9a4d5d0b2feb0a09aafeb441c6b33260e4f0738b
ms.contentlocale: es-es
ms.lasthandoff: 09/09/2017

---
# <a name="odbc-jet-sqlconfigdatasource-excel-driver"></a>ODBC Jet SQLConfigDataSource (controlador de Excel)
> [!NOTE]  
>  En este tema se proporciona información específica del controlador de Excel. Para obtener información general acerca de esta función, vea el tema correspondiente en [referencia de la API de ODBC](../../odbc/reference/syntax/odbc-api-reference.md).  
  
 El **SQLConfigDataSource** función que se utiliza para agregar, modificar o eliminar un origen de datos dinámicamente usa las siguientes palabras clave.  
  
|Palabra clave|Description|  
|-------------|-----------------|  
|DBQ|Para el controlador de Microsoft Excel cuando tiene acceso a Microsoft Excel 5.0 o archivos de una versión posterior, el nombre del archivo de libro.<br /><br /> Esto establece la misma opción como **base de datos** en el cuadro de diálogo de instalación.|  
|VALOR DE ESTA OPCIÓN|La especificación de ruta de acceso al directorio.<br /><br /> Esto establece la misma opción como **Seleccionar directorio** o **Seleccionar libro** en el cuadro de diálogo de instalación.|  
|DESCRIPTION|Una descripción de los datos del origen de datos.<br /><br /> Esto establece la misma opción como **descripción** en el cuadro de diálogo de instalación.|  
|DRIVER|La especificación de ruta de acceso a la DLL del controlador.|  
|DRIVERID|Un identificador entero para el controlador.<br /><br /> 534 (Microsoft Excel 3.0)<br /><br /> 278 (Microsoft Excel 4.0)<br /><br /> 22 (Microsoft Excel 5.0/7.0)<br /><br /> 790 (Microsoft Excel 97-2003)|  
|FIL|Archivo de tipo, por ejemplo, Excel 3.0, 4.0 de Excel, Excel 5.0, 7.0 de Excel, Excel 97, Excel 2000 o Excel 2003.|  
|FIRSTROWHASNAMES|Indica si las celdas de la primera fila del intervalo contienen los nombres de columna para la tabla (1) o no (0).|  
|MAXSCANROWS|El número de filas que deben analizarse al establecer el tipo de datos de una columna en función de los datos existentes.<br /><br /> Un número comprendido entre 1 y 16 puede especificarse para que las filas que se va a buscar. El valor predeterminado es 8; Si se establece en 0, se examinan todas las filas. (Un número que está fuera del límite devolverá un error.)<br /><br /> Esto establece la misma opción como **filas para explorar** en el cuadro de diálogo de instalación.|  
|READONLY|TRUE para que el archivo de solo lectura; FALSE para que el archivo no sea de sólo lectura.<br /><br /> Esto establece la misma opción como **de sólo lectura** en el cuadro de diálogo de instalación.|  
|SUBPROCESOS|El número de subprocesos en segundo plano para el motor para usar. Para el controlador de Microsoft Access, este valor predeterminado es 3, pero puede cambiarse. Para dBASE, MicrosoftExceldriver este valor es 3 y no se puede cambiar.<br /><br /> Esto establece la misma opción como **subprocesos** en el cuadro de diálogo de instalación.|

