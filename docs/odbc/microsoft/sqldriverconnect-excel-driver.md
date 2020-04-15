---
title: SQLDriverConnect (controlador de Excel) Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- Excel driver [ODBC], SQLDriverConnect
- SQLDriverConnect function [ODBC], Excel Driver
ms.assetid: 285cb1ea-f461-4596-97f2-fc57af05dede
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 1108206bf38183887540b114fda5a1e913aa67d9
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/14/2020
ms.locfileid: "81307126"
---
# <a name="sqldriverconnect-excel-driver"></a>SQLDriverConnect (controlador de Excel)
> [!NOTE]  
>  En este tema se proporciona información específica del controlador de Excel. Para obtener información general sobre esta función, consulte el tema adecuado en Referencia de [la API ODBC](../../odbc/reference/syntax/odbc-api-reference.md).  
  
 **SQLDriverConnect** le permite conectarse a un controlador sin crear un origen de datos (DSN).  
  
 Las siguientes palabras clave se admiten en la cadena de conexión para todos los controladores: **DSN**, **DBQ**y **FIL**.  
  
 En la tabla siguiente se muestran las palabras clave mínimas necesarias para conectarse a cada controlador y se proporciona un ejemplo de pares de palabra clave/valor utilizados con **SQLDriverConnect**. Para obtener una lista completa de los valores DRIVERID, vea [SQLConfigDataSource](../../odbc/microsoft/odbc-jet-sqlconfigdatasource-excel-driver.md).  
  
> [!NOTE]  
>  Si no se especifica DBQ o DefaultDir para el controlador de Microsoft Excel 3.0 o 4.0, el controlador se conectará al directorio actual.  
  
|Controlador|Palabras clave requeridas|Ejemplos|  
|------------|-----------------------|--------------|  
|Microsoft Excel 3.0 o 4.0|Conductor, DriverID|Controlador de Microsoft Excel Driver (*.xls); DBQ-c:-temp; Id. de conductor 278|  
|Microsoft Excel 5.0/7.0|Controlador, DriverID, DBQ|Controlador de Microsoft Excel Driver (*.xls); DBQ-c:-temp-sample.xls; Id. de conductor 22|  
|Microsoft Excel 97 y versiones posteriores|Controlador, DriverID, DBQ|Controlador de Microsoft Excel Driver (*.xls); DBQ-c:-temp-sample.xls; Id. de conductor 790|
