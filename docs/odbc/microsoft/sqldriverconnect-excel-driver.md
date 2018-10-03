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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: b2d7e879c35e7cbf2f2b261d94eff22936f7880b
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/01/2018
ms.locfileid: "47775353"
---
# <a name="sqldriverconnect-excel-driver"></a>SQLDriverConnect (controlador de Excel)
> [!NOTE]  
>  En este tema se proporciona información específica del controlador de Excel. Para obtener información general acerca de esta función, vea el tema correspondiente en [referencia de la API de ODBC](../../odbc/reference/syntax/odbc-api-reference.md).  
  
 **SQLDriverConnect** le permite conectarse a un controlador sin necesidad de crear un origen de datos (DSN).  
  
 Se admiten las siguientes palabras clave en la cadena de conexión para todos los controladores: **DSN**, **DBQ**, y **FIL**.  
  
 En la tabla siguiente muestra las palabras clave mínimas necesarias para conectarse a cada controlador y proporciona un ejemplo de pares de palabra clave y valor utilizada con **SQLDriverConnect**. Para obtener una lista completa de valores DRIVERID, consulte [SQLConfigDataSource](../../odbc/microsoft/odbc-jet-sqlconfigdatasource-excel-driver.md).  
  
> [!NOTE]  
>  Si no se especifica DBQ o valor de esta opción para Microsoft Excel 3.0 o 4.0 de controlador, el controlador se conectará en el directorio actual.  
  
|Controlador|Palabras clave necesarias|Ejemplos|  
|------------|-----------------------|--------------|  
|Microsoft Excel 3.0 o 4.0|Controlador, DriverID|Driver = {controlador de Microsoft Excel (*.xls)}; DBQ = c:\temp; DriverID = 278|  
|Microsoft Excel 5.0/7.0|Controlador, DriverID, DBQ|Driver = {controlador de Microsoft Excel (*.xls)}; DBQ=c:\temp\sample.xls; DriverID = 22|  
|Microsoft Excel 97 y versiones posterior|Controlador, DriverID, DBQ|Driver = {controlador de Microsoft Excel (*.xls)}; DBQ=c:\temp\sample.xls; DriverID = 790|
