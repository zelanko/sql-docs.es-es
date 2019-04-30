---
title: ODBC Jet SQLConfigDataSource (controlador de Excel) | Microsoft Docs
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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: dbad3b1e6dda82a9f9fc584683e53f8e2a109cca
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/23/2019
ms.locfileid: "63233595"
---
# <a name="odbc-jet-sqlconfigdatasource-excel-driver"></a>ODBC Jet SQLConfigDataSource (controlador de Excel)
> [!NOTE]  
>  En este tema se proporciona información específica del controlador de Excel. Para obtener información general acerca de esta función, vea el tema correspondiente en [referencia de la API de ODBC](../../odbc/reference/syntax/odbc-api-reference.md).  
  
 El **SQLConfigDataSource** función que se usa para agregar, modificar o eliminar un origen de datos usa dinámicamente las siguientes palabras clave.  
  
|Palabra clave|Descripción|  
|-------------|-----------------|  
|DBQ|Para el controlador de Microsoft Excel al acceder a Microsoft Excel 5.0 o posterior archivos, el nombre del archivo de libro.<br /><br /> Esto establece la misma opción como **base de datos** en el cuadro de diálogo programa de instalación.|  
|DEFAULTDIR|La especificación de ruta de acceso al directorio.<br /><br /> Esto establece la misma opción como **Seleccionar directorio** o **Seleccionar libro** en el cuadro de diálogo programa de instalación.|  
|DESCRIPTION|Una descripción de los datos del origen de datos.<br /><br /> Esto establece la misma opción como **descripción** en el cuadro de diálogo programa de instalación.|  
|DRIVER|La especificación de ruta de acceso a la DLL del controlador.|  
|DRIVERID|Un identificador entero para el controlador.<br /><br /> 534 (Microsoft Excel 3.0)<br /><br /> 278 (Microsoft Excel 4.0)<br /><br /> 22 (5.0 o 7.0 de Microsoft Excel)<br /><br /> 790 (Microsoft Excel 97-2003)|  
|FIL|Archivo de tipo, por ejemplo, Excel 3.0, Excel 4.0, 5.0 de Excel, Excel 7.0, Excel 97, Excel 2000 o Excel 2003.|  
|FIRSTROWHASNAMES|Indica si las celdas de la primera fila del rango contienen los nombres de columna para la tabla (1) o no (0).|  
|MAXSCANROWS|El número de filas a explorar al establecer el tipo de datos de una columna en función de los datos existentes.<br /><br /> Un número entre 1 y 16 se puede especificar para que las filas que se va a analizar. El valor predeterminado es 8; Si se establece en 0, se examinan todas las filas. (Un número fuera del límite devolverá un error).<br /><br /> Esto establece la misma opción como **filas para explorar** en el cuadro de diálogo programa de instalación.|  
|READONLY|TRUE para que el archivo de solo lectura. FALSE para que el archivo no sea de sólo lectura.<br /><br /> Esto establece la misma opción como **de sólo lectura** en el cuadro de diálogo programa de instalación.|  
|SUBPROCESOS|El número de subprocesos en segundo plano para el motor para usar. Para el controlador de Microsoft Access, este valor predeterminado es 3, pero puede cambiarse. Para el dBASE, MicrosoftExceldriver este valor es 3 y no se puede cambiar.<br /><br /> Esto establece la misma opción como **subprocesos** en el cuadro de diálogo programa de instalación.|
