---
title: SQLConfigDataSource (controlador dBASE) | Documentos de Microsoft
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
- DBase driver [ODBC], SQLConfigDataSource
- SQLConfigDataSource function [ODBC], dBASE Driver
ms.assetid: 19909902-054c-4e19-9c06-a212aace13fe
caps.latest.revision: 7
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: f4db30f9e0c291151409d5af6a63226c0c2292bd
ms.contentlocale: es-es
ms.lasthandoff: 09/09/2017

---
# <a name="sqlconfigdatasource-dbase-driver"></a>SQLConfigDataSource (dBASE controlador)
> [!NOTE]  
>  Este tema proporciona información de dBASE específicos del controlador. Para obtener información general acerca de esta función, vea el tema correspondiente en [referencia de la API de ODBC](../../odbc/reference/syntax/odbc-api-reference.md).  
  
 El **SQLConfigDataSource** función que se utiliza para agregar, modificar o eliminar un origen de datos dinámicamente usa las siguientes palabras clave.  
  
|Palabra clave|Description|  
|-------------|-----------------|  
|COLLATINGSEQUENCE|La secuencia en la que se ordenan los campos.<br /><br /> La secuencia puede ser: ASCII (valor predeterminado) o internacional.<br /><br /> Esto establece la misma opción como **secuencia de intercalación** en el cuadro de diálogo de instalación.|  
|VALOR DE ESTA OPCIÓN|La especificación de ruta de acceso al directorio.|  
|DELETED|Para el controlador dBASE, especifica si no se pueden recuperar o colocados en filas que se han marcado como eliminada. Si se establece en 1, las filas eliminadas no se muestra. Si se establece en 0, filas eliminadas se trata igual que las filas no se han eliminado.<br /><br /> Esto establece la misma opción como **mostrar filas eliminadas** en el cuadro de diálogo de instalación.|  
|DESCRIPTION|Una descripción de los datos del origen de datos.<br /><br /> Esto establece la misma opción como **descripción** en el cuadro de diálogo de instalación.|  
|DRIVER|La especificación de ruta de acceso a la DLL del controlador.|  
|DRIVERID|Un identificador entero para el controlador.<br /><br /> 21 (dBASE III)<br /><br /> 277 (dBASE IV)<br /><br /> 533 (dBASE 5.0)|  
|FIL|Archivos dBase III, dBase IV o dBase 5 de tipo|  
|PAGETIMEOUT|Especifica el período de tiempo, en décimas de segundo, que una página (si no se utiliza) permanece en el búfer antes de que se va a quitar. El valor predeterminado es 600 décimas de segundo (60 segundos). Tenga en cuenta que esta opción se aplica a todos los orígenes de datos que utilizan el controlador ODBC.<br /><br /> Esto establece la misma opción como **Page Timeout** en el cuadro de diálogo de instalación.|  
|READONLY|TRUE para que el archivo de solo lectura; FALSE para que el archivo no sea de sólo lectura.<br /><br /> Esto establece la misma opción como **de sólo lectura** en el cuadro de diálogo de instalación.|  
|STATISTICS|Para el controlador dBASE, determina si las estadísticas de tamaño de tabla son aproximadas. Tenga en cuenta que esta opción se aplica a todos los orígenes de datos que utilizan el controlador ODBC.<br /><br /> Esto establece la misma opción como **recuento de filas aproximado** en el cuadro de diálogo de instalación.|  
|SUBPROCESOS|El número de subprocesos en segundo plano para el motor para usar. Este valor es 3 y no se puede cambiar.<br /><br /> Esto establece la misma opción como **subprocesos** en el cuadro de diálogo de instalación.|
