---
title: SQLDriverConnect (controlador de archivo de texto) | Documentos de Microsoft
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
- SQLDriverConnect function [ODBC], Text File Driver
- text file driver [ODBC], SQLDriverConnect
ms.assetid: d7769021-bd18-4d8e-96e0-e184a82d6ca3
caps.latest.revision: 6
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 117b619b351e5a8c1e2c0865fe0ed6add5589ecb
ms.contentlocale: es-es
ms.lasthandoff: 09/09/2017

---
# <a name="sqldriverconnect-text-file-driver"></a>SQLDriverConnect (controlador de archivo de texto)
> [!NOTE]  
>  En este tema se proporciona información específica del controlador de archivo de texto. Para obtener información general acerca de esta función, vea el tema correspondiente en [referencia de la API de ODBC](../../odbc/reference/syntax/odbc-api-reference.md).  
  
 **SQLDriverConnect** le permite conectarse a un controlador sin crear un origen de datos (DSN).  
  
 Se admiten las siguientes palabras clave en la cadena de conexión para todos los controladores: **DSN**, **DBQ**, y **FIL**.  
  
 En la siguiente tabla muestra las palabras clave mínima necesarias para conectarse a cada controlador y proporciona un ejemplo de los pares palabra clave-valor utilizado con **SQLDriverConnect**. Para obtener una lista completa de valores DRIVERID, consulte [SQLConfigDataSource](../../odbc/microsoft/sqlconfigdatasource-text-file-driver.md).  
  
> [!NOTE]  
>  Si DBQ o valor de esta opción no se especifica para el controlador de texto, el controlador se conectará al directorio actual.  
  
|Controlador|Palabras clave necesaria|Ejemplos|  
|------------|-----------------------|--------------|  
|Texto|Controlador|Driver = {controlador Microsoft texto (*.txt;\*. CSV)}; Valor de esta opción = c:\temp|

