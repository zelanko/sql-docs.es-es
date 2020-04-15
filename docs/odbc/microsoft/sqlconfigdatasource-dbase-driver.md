---
title: SQLConfigDataSource (controlador dBASE) Microsoft Docs
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 18c6721b4f34772e8c3cd8e4f515233f80566fb3
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/14/2020
ms.locfileid: "81283975"
---
# <a name="sqlconfigdatasource-dbase-driver"></a>SQLConfigDataSource (dBASE controlador)
> [!NOTE]  
>  En este tema se proporciona información específica del controlador dBASE. Para obtener información general sobre esta función, consulte el tema adecuado en Referencia de [la API ODBC](../../odbc/reference/syntax/odbc-api-reference.md).  
  
 La función **SQLConfigDataSource** que se usa para agregar, modificar o eliminar un origen de datos utiliza dinámicamente las siguientes palabras clave.  
  
|Palabra clave|Descripción|  
|-------------|-----------------|  
|SECUENCIA DE INTERCALACIÓN|La secuencia en la que se ordenan los campos.<br /><br /> La secuencia puede ser: ASCII (valor predeterminado) o Internacional.<br /><br /> Esto establece la misma opción **que Secuencia de intercalación** en el cuadro de diálogo de configuración.|  
|DEFAULTDIR|La especificación de ruta de acceso al directorio.|  
|DELETED|Para el controlador dBASE, especifica si se pueden recuperar o colocar o no filas que se han marcado como eliminadas. Si se establece en 1, no se muestran las filas eliminadas; si se establece en 0, las filas eliminadas se tratan igual que las filas no eliminadas.<br /><br /> Esto establece la misma opción que **Mostrar filas eliminadas** en el cuadro de diálogo de configuración.|  
|DESCRIPTION|Una descripción de los datos en el origen de datos.<br /><br /> Esto establece la misma opción que **Descripción** en el cuadro de diálogo de configuración.|  
|DRIVER|La especificación de ruta de acceso al archivo DLL del controlador.|  
|DRIVERID|Un identificador entero para el controlador.<br /><br /> 21 (dBASE III)<br /><br /> 277 (dBASE IV)<br /><br /> 533 (dBASE 5.0)|  
|Fil|Tipo de archivo dBase III, dBase IV o dBase 5|  
|PAGETIMEOUT|Especifica el período de tiempo, en décimas de segundo, que una página (si no se utiliza) permanece en el búfer antes de quitarse. El valor predeterminado es 600 décimas de segundo (60 segundos). Tenga en cuenta que esta opción se aplica a todos los orígenes de datos que usan el controlador ODBC.<br /><br /> Esto establece la misma opción que Tiempo de espera de **página** en el cuadro de diálogo de configuración.|  
|READONLY|TRUE para que el archivo sea de solo lectura; FALSE para que el archivo no sea de solo lectura.<br /><br /> Esto establece la misma opción que **solo lectura** en el cuadro de diálogo de configuración.|  
|STATISTICS|Para el controlador dBASE, determina si las estadísticas de tamaño de tabla son aproximadas. Tenga en cuenta que esta opción se aplica a todos los orígenes de datos que usan el controlador ODBC.<br /><br /> Esto establece la misma opción que **Recuento aproximado** de filas en el cuadro de diálogo de configuración.|  
|Hilos|El número de subprocesos en segundo plano que va a utilizar el motor. Este valor es 3 y no se puede cambiar.<br /><br /> Esto establece la misma opción que **subprocesos** en el cuadro de diálogo de configuración.|
