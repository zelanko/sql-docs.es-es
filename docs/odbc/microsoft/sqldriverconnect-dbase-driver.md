---
title: SQLDriverConnect (controlador dBASE) | Documentos de Microsoft
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: microsoft
ms.reviewer: 
ms.suite: sql
ms.technology: drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- DBase driver [ODBC], SQLDriverConnect
- SQLDriverConnect function [ODBC], dBASE Driver
ms.assetid: c837aa31-068e-4fa3-bc00-aae09bec21de
caps.latest.revision: "6"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: edddede97d820b98a66bbbb75bb5cf14afe5c2c5
ms.sourcegitcommit: 7f8aebc72e7d0c8cff3990865c9f1316996a67d5
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/20/2017
---
# <a name="sqldriverconnect-dbase-driver"></a>SQLDriverConnect (dBASE controlador)
> [!NOTE]  
>  Este tema proporciona información de dBASE específicos del controlador. Para obtener información general acerca de esta función, vea el tema correspondiente en [referencia de la API de ODBC](../../odbc/reference/syntax/odbc-api-reference.md).  
  
 **SQLDriverConnect** le permite conectarse a un controlador sin crear un origen de datos (DSN).  
  
 Se admiten las siguientes palabras clave en la cadena de conexión para todos los controladores: **DSN**, **DBQ**, y **FIL**.  
  
 Cuando se utiliza el controlador de Paradox, después de que un usuario ha abierto un archivo protegido con contraseña, otros usuarios no puedan abrir el mismo archivo.  
  
 En la siguiente tabla muestra las palabras clave mínima necesarias para conectarse a cada controlador y proporciona un ejemplo de los pares palabra clave-valor utilizado con **SQLDriverConnect**. Para obtener una lista completa de valores DRIVERID, consulte [SQLConfigDataSource](../../odbc/microsoft/sqlconfigdatasource-dbase-driver.md).  
  
> [!NOTE]  
>  Si DBQ o valor de esta opción no se especifica para el dBASEdriver, el controlador se conectará al directorio actual.  
  
|Controlador|Palabras clave necesaria|Ejemplos|  
|------------|-----------------------|--------------|  
|dBASE|Controlador, DriverID|Driver = {Microsoft dBASE Driver (*.dbf)}; DBQ = c:\temp; DriverID = 277|
