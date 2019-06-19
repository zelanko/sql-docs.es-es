---
title: SQLDriverConnect (Paradox Driver) | Microsoft Docs
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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: bae4a842729c8d302731ebf5fec22abb817f4c75
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/15/2019
ms.locfileid: "63238378"
---
# <a name="sqldriverconnect-paradox-driver"></a>SQLDriverConnect (controlador de Paradox)
> [!NOTE]  
>  En este tema se proporciona información específica del controlador de Paradox. Para obtener información general acerca de esta función, vea el tema correspondiente en [referencia de la API de ODBC](../../odbc/reference/syntax/odbc-api-reference.md).  
  
 **SQLDriverConnect** le permite conectarse a un controlador sin necesidad de crear un origen de datos (DSN).  
  
 Se admiten las siguientes palabras clave en la cadena de conexión para todos los controladores: **DSN**, **DBQ**, y **FIL**.  
  
 El **PWD** también se admite la palabra clave. No debe incluir la palabra clave PWD cualquiera de los caracteres especiales (consulte SQL_SPECIAL_CHARACTERS en **SQLGetInfo** devuelven valores).  
  
 Después de abrir un archivo protegido por contraseña por un usuario, no se permiten otros usuarios para abrir el mismo archivo.  
  
 En la tabla siguiente muestra las palabras clave mínimas necesarias para conectarse a cada controlador y proporciona un ejemplo de pares de palabra clave y valor utilizada con **SQLDriverConnect**. Para obtener una lista completa de valores DRIVERID, consulte [SQLConfigDataSource](../../odbc/microsoft/sqlconfigdatasource-paradox-driver.md).  
  
> [!NOTE]  
>  Si no se especifica DBQ o valor de esta opción para el controlador de Paradox, el controlador se conectará al directorio actual.  
  
|Controlador|Palabras clave necesarias|Ejemplo|  
|------------|-----------------------|-------------|  
|Paradox|Controlador, DriverID|Driver={Microsoft Paradox Driver (*.db )}; DBQ=c:\temp;DriverID=26|
