---
description: SQLDriverConnect (controlador de Paradox)
title: SQLDriverConnect (controlador de Paradox) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SQLDriverConnect function [ODBC], Paradox Driver
- Paradox driver [ODBC], SQLDriverConnect
ms.assetid: c2ba486e-5e01-4e67-adb1-68511f5f0206
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 8b6bffe650bfc204660d7345b1bd5a051105fb5b
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/17/2020
ms.locfileid: "88421819"
---
# <a name="sqldriverconnect-paradox-driver"></a>SQLDriverConnect (controlador de Paradox)
> [!NOTE]  
>  En este tema se proporciona información específica del controlador de Paradox. Para obtener información general sobre esta función, vea el tema correspondiente en referencia de la [API de ODBC](../../odbc/reference/syntax/odbc-api-reference.md).  
  
 **SQLDriverConnect** le permite conectarse a un controlador sin crear un origen de datos (DSN).  
  
 Las palabras clave siguientes se admiten en la cadena de conexión para todos los controladores: **DSN**, **DBQ**y **Fil**.  
  
 También se admite la palabra clave **pwd** . La palabra clave PWD no debe incluir ninguno de los caracteres especiales (vea SQL_SPECIAL_CHARACTERS en los valores devueltos de **SQLGetInfo** ).  
  
 Una vez que un usuario ha abierto un archivo protegido por contraseña, no se permite que otros usuarios abran el mismo archivo.  
  
 En la tabla siguiente se muestran las palabras clave mínimas necesarias para conectarse a cada controlador y se proporciona un ejemplo de pares de palabra clave y valor que se usan con **SQLDriverConnect**. Para obtener una lista completa de los valores de DRIVERID, consulte [SQLConfigDataSource](../../odbc/microsoft/sqlconfigdatasource-paradox-driver.md).  
  
> [!NOTE]  
>  Si no se especifica DBQ o DefaultDir para el controlador de Paradox, el controlador se conectará al directorio actual.  
  
|Controlador|Palabras clave necesarias|Ejemplo|  
|------------|-----------------------|-------------|  
|Paradox|Controlador, DriverID|Driver = {controlador de Microsoft Paradox (*. dB)}; DBQ = c:\temp; DriverID = 26|
