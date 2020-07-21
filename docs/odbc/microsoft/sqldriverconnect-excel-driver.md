---
title: SQLDriverConnect (controlador de Excel) | Microsoft Docs
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
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/27/2020
ms.locfileid: "81307126"
---
# <a name="sqldriverconnect-excel-driver"></a>SQLDriverConnect (controlador de Excel)
> [!NOTE]  
>  En este tema se proporciona información específica del controlador de Excel. Para obtener información general sobre esta función, vea el tema correspondiente en referencia de la [API de ODBC](../../odbc/reference/syntax/odbc-api-reference.md).  
  
 **SQLDriverConnect** le permite conectarse a un controlador sin crear un origen de datos (DSN).  
  
 Las palabras clave siguientes se admiten en la cadena de conexión para todos los controladores: **DSN**, **DBQ**y **Fil**.  
  
 En la tabla siguiente se muestran las palabras clave mínimas necesarias para conectarse a cada controlador y se proporciona un ejemplo de pares de palabra clave y valor que se usan con **SQLDriverConnect**. Para obtener una lista completa de los valores de DRIVERID, consulte [SQLConfigDataSource](../../odbc/microsoft/odbc-jet-sqlconfigdatasource-excel-driver.md).  
  
> [!NOTE]  
>  Si no se especifica DBQ o DefaultDir para el controlador Microsoft Excel 3,0 o 4,0, el controlador se conectará al directorio actual.  
  
|Controlador|Palabras clave necesarias|Ejemplos|  
|------------|-----------------------|--------------|  
|Microsoft Excel 3,0 o 4,0|Controlador, DriverID|Driver = {controlador de Microsoft Excel (*. xls)}; DBQ = c:\temp; DriverID = 278|  
|Microsoft Excel 5.0/7.0|Driver, DriverID, DBQ|Driver = {controlador de Microsoft Excel (*. xls)}; DBQ = c:\temp\sample.xls; DriverID = 22|  
|Microsoft Excel 97 y versiones posteriores|Driver, DriverID, DBQ|Driver = {controlador de Microsoft Excel (*. xls)}; DBQ = c:\temp\sample.xls; DriverID = 790|
