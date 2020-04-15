---
title: SQLDriverConnect (controlador de paradoja) Microsoft Docs
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
ms.openlocfilehash: 68171cfab2b65634433b107d829dd2a6e9b5c985
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/14/2020
ms.locfileid: "81307116"
---
# <a name="sqldriverconnect-paradox-driver"></a>SQLDriverConnect (controlador de Paradox)
> [!NOTE]  
>  En este tema se proporciona información específica del controlador de Paradox. Para obtener información general sobre esta función, consulte el tema adecuado en Referencia de [la API ODBC](../../odbc/reference/syntax/odbc-api-reference.md).  
  
 **SQLDriverConnect** le permite conectarse a un controlador sin crear un origen de datos (DSN).  
  
 Las siguientes palabras clave se admiten en la cadena de conexión para todos los controladores: **DSN**, **DBQ**y **FIL**.  
  
 También se admite la palabra clave **PWD.** La palabra clave PWD no debe incluir ninguno de los caracteres especiales (consulte SQL_SPECIAL_CHARACTERS en **SQLGetInfo** Valores devueltos).  
  
 Después de que un usuario haya abierto un archivo protegido con contraseña, no se permite que otros usuarios abran el mismo archivo.  
  
 En la tabla siguiente se muestran las palabras clave mínimas necesarias para conectarse a cada controlador y se proporciona un ejemplo de pares de palabra clave/valor utilizados con **SQLDriverConnect**. Para obtener una lista completa de los valores DRIVERID, vea [SQLConfigDataSource](../../odbc/microsoft/sqlconfigdatasource-paradox-driver.md).  
  
> [!NOTE]  
>  Si no se especifica DBQ o DefaultDir para el controlador Paradox, el controlador se conectará al directorio actual.  
  
|Controlador|Palabras clave requeridas|Ejemplo|  
|------------|-----------------------|-------------|  
|Paradoja|Conductor, DriverID|Controlador-Controlador paradox de Microsoft (*.db );; DBQ-c:-temp;DriverID-26|
