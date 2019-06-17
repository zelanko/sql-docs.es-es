---
title: SQLConfigDataSource (dBASE controlador) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- DBase driver [ODBC], SQLConfigDataSource
- SQLConfigDataSource function [ODBC], dBASE Driver
ms.assetid: 19909902-054c-4e19-9c06-a212aace13fe
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 63d1951cfe835cbfca23ab366db2216215aa92c3
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/15/2019
ms.locfileid: "62665357"
---
# <a name="sqlconfigdatasource-dbase-driver"></a>SQLConfigDataSource (dBASE controlador)
> [!NOTE]  
>  Este tema proporciona información específica del controlador de dBASE. Para obtener información general acerca de esta función, vea el tema correspondiente en [referencia de la API de ODBC](../../odbc/reference/syntax/odbc-api-reference.md).  
  
 El **SQLConfigDataSource** función que se usa para agregar, modificar o eliminar un origen de datos usa dinámicamente las siguientes palabras clave.  
  
|Palabra clave|Descripción|  
|-------------|-----------------|  
|COLLATINGSEQUENCE|La secuencia en la que se ordenan los campos.<br /><br /> La secuencia puede ser: ASCII (valor predeterminado) o internacional.<br /><br /> Esto establece la misma opción como **secuencia de intercalación** en el cuadro de diálogo programa de instalación.|  
|DEFAULTDIR|La especificación de ruta de acceso al directorio.|  
|DELETED|Para el controlador de dBASE, especifica si se pueden recuperar o colocadas en las filas que se han marcado como eliminado. Si se establece en 1, las filas eliminadas no se muestra. Si se establece en 0, filas eliminadas se trata igual que las filas no eliminados.<br /><br /> Esto establece la misma opción como **mostrar filas eliminadas** en el cuadro de diálogo programa de instalación.|  
|DESCRIPTION|Una descripción de los datos del origen de datos.<br /><br /> Esto establece la misma opción como **descripción** en el cuadro de diálogo programa de instalación.|  
|DRIVER|La especificación de ruta de acceso a la DLL del controlador.|  
|DRIVERID|Un identificador entero para el controlador.<br /><br /> 21 (dBASE III)<br /><br /> 277 (dBASE IV)<br /><br /> 533 (dBASE 5.0)|  
|FIL|Archivo de tipo dBase III, dBase IV o dBase 5|  
|PAGETIMEOUT|Especifica el período de tiempo, en décimas de segundo, que permanece una página (si no usa) en el búfer antes de eliminarse. El valor predeterminado es 600 décimas de segundo (60 segundos). Tenga en cuenta que esta opción se aplica a todos los orígenes de datos que usan el controlador ODBC.<br /><br /> Esto establece la misma opción como **Page Timeout** en el cuadro de diálogo programa de instalación.|  
|READONLY|TRUE para que el archivo de solo lectura. FALSE para que el archivo no sea de sólo lectura.<br /><br /> Esto establece la misma opción como **de sólo lectura** en el cuadro de diálogo programa de instalación.|  
|STATISTICS|Para el controlador de dBASE, determina si se aproximan las estadísticas de tamaño de tabla. Tenga en cuenta que esta opción se aplica a todos los orígenes de datos que usan el controlador ODBC.<br /><br /> Esto establece la misma opción como **recuento de filas aproximado** en el cuadro de diálogo programa de instalación.|  
|SUBPROCESOS|El número de subprocesos en segundo plano para el motor para usar. Este valor es 3 y no se puede cambiar.<br /><br /> Esto establece la misma opción como **subprocesos** en el cuadro de diálogo programa de instalación.|
