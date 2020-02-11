---
title: SQLConfigDataSource (dBASE driver) | Microsoft Docs
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
ms.openlocfilehash: 569a83110d7d5a3cd25eed8f68753d13793f8b10
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/08/2020
ms.locfileid: "68054100"
---
# <a name="sqlconfigdatasource-dbase-driver"></a>SQLConfigDataSource (dBASE controlador)
> [!NOTE]  
>  En este tema se proporciona información específica del controlador de dBASE. Para obtener información general sobre esta función, vea el tema correspondiente en referencia de la [API de ODBC](../../odbc/reference/syntax/odbc-api-reference.md).  
  
 La función **SQLConfigDataSource** que se utiliza para agregar, modificar o eliminar un origen de datos utiliza de forma dinámica las siguientes palabras clave.  
  
|Palabra clave|Descripción|  
|-------------|-----------------|  
|COLLATINGSEQUENCE|Secuencia en la que se ordenan los campos.<br /><br /> La secuencia puede ser: ASCII (valor predeterminado) o internacional.<br /><br /> Esto establece la misma opción que la **secuencia de intercalación** en el cuadro de diálogo de instalación.|  
|DEFAULTDIR|Especificación de la ruta de acceso al directorio.|  
|DELETED|En el caso del controlador dBASE, especifica si las filas que se han marcado como eliminadas se pueden recuperar o colocar en. Si se establece en 1, las filas eliminadas no se muestran; Si se establece en 0, las filas eliminadas se tratan igual que las filas no eliminadas.<br /><br /> Esto establece la misma opción que **mostrar filas eliminadas** en el cuadro de diálogo de configuración.|  
|Description|Descripción de los datos del origen de datos.<br /><br /> Esto establece la misma opción que la **Descripción** en el cuadro de diálogo de configuración.|  
|DRIVER|Especificación de la ruta de acceso al archivo DLL del controlador.|  
|DRIVERID|IDENTIFICADOR entero para el controlador.<br /><br /> 21 (dBASE III)<br /><br /> 277 (dBASE IV)<br /><br /> 533 (dBASE 5,0)|  
|FIL|Tipo de archivo dBase III, dBase IV o dBase 5|  
|PAGETIMEOUT|Especifica el período de tiempo, en décimas de segundo, que una página (si no se usa) permanece en el búfer antes de quitarse. El valor predeterminado es 600 décimas de segundo (60 segundos). Tenga en cuenta que esta opción se aplica a todos los orígenes de datos que utilizan el controlador ODBC.<br /><br /> Esto establece la misma opción que el **tiempo de espera de página** en el cuadro de diálogo de instalación.|  
|READONLY|TRUE para hacer que el archivo sea de solo lectura; FALSE para que el archivo no sea de solo lectura.<br /><br /> Esto establece la misma opción que **solo lectura** en el cuadro de diálogo de instalación.|  
|STATISTICS|En el caso del controlador dBASE, determina si se aproximan las estadísticas de tamaño de tabla. Tenga en cuenta que esta opción se aplica a todos los orígenes de datos que utilizan el controlador ODBC.<br /><br /> Esto establece la misma opción que el **recuento aproximado de filas** en el cuadro de diálogo de instalación.|  
|THREADPOOL|Número de subprocesos en segundo plano que va a usar el motor. Este valor es 3 y no se puede cambiar.<br /><br /> Esto establece la misma opción que los **subprocesos** en el cuadro de diálogo de instalación.|
