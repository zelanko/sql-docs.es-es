---
description: SQLDriverConnect (dBASE controlador)
title: SQLDriverConnect (dBASE driver) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- DBase driver [ODBC], SQLDriverConnect
- SQLDriverConnect function [ODBC], dBASE Driver
ms.assetid: c837aa31-068e-4fa3-bc00-aae09bec21de
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: e15925b52c096acb1a1021c1a2f968c0863eacf0
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/17/2020
ms.locfileid: "88449207"
---
# <a name="sqldriverconnect-dbase-driver"></a>SQLDriverConnect (dBASE controlador)
> [!NOTE]  
>  En este tema se proporciona información específica del controlador de dBASE. Para obtener información general sobre esta función, vea el tema correspondiente en referencia de la [API de ODBC](../../odbc/reference/syntax/odbc-api-reference.md).  
  
 **SQLDriverConnect** le permite conectarse a un controlador sin crear un origen de datos (DSN).  
  
 Las palabras clave siguientes se admiten en la cadena de conexión para todos los controladores: **DSN**, **DBQ**y **Fil**.  
  
 Cuando se usa el controlador de Paradox, una vez que un usuario ha abierto un archivo protegido por contraseña, no se permite que otros usuarios abran el mismo archivo.  
  
 En la tabla siguiente se muestran las palabras clave mínimas necesarias para conectarse a cada controlador y se proporciona un ejemplo de pares de palabra clave y valor que se usan con **SQLDriverConnect**. Para obtener una lista completa de los valores de DRIVERID, consulte [SQLConfigDataSource](../../odbc/microsoft/sqlconfigdatasource-dbase-driver.md).  
  
> [!NOTE]  
>  Si no se especifica DBQ o DefaultDir para dBASEdriver, el controlador se conectará al directorio actual.  
  
|Controlador|Palabras clave necesarias|Ejemplos|  
|------------|-----------------------|--------------|  
|dBASE|Controlador, DriverID|Driver = {controlador dBASE de Microsoft (*. dbf)}; DBQ = c:\temp; DriverID = 277|
