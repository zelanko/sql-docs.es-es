---
title: SQLDriverConnect (controlador de Paradox) | Documentos de Microsoft
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
- SQLDriverConnect function [ODBC], Paradox Driver
- Paradox driver [ODBC], SQLDriverConnect
ms.assetid: c2ba486e-5e01-4e67-adb1-68511f5f0206
caps.latest.revision: 6
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: f9265657327f71e41c124707ab66c8ad621bda55
ms.contentlocale: es-es
ms.lasthandoff: 09/09/2017

---
# <a name="sqldriverconnect-paradox-driver"></a>SQLDriverConnect (controlador de Paradox)
> [!NOTE]  
>  En este tema se proporciona información específica del controlador Paradox. Para obtener información general acerca de esta función, vea el tema correspondiente en [referencia de la API de ODBC](../../odbc/reference/syntax/odbc-api-reference.md).  
  
 **SQLDriverConnect** le permite conectarse a un controlador sin crear un origen de datos (DSN).  
  
 Se admiten las siguientes palabras clave en la cadena de conexión para todos los controladores: **DSN**, **DBQ**, y **FIL**.  
  
 El **PWD** también se admite la palabra clave. La palabra clave PWD no debe incluir ninguno de los caracteres especiales (consulte SQL_SPECIAL_CHARACTERS en **SQLGetInfo** valores devueltos).  
  
 Después de que un usuario ha abierto un archivo protegido con contraseña, no se admiten otros usuarios para abrir el mismo archivo.  
  
 En la siguiente tabla muestra las palabras clave mínima necesarias para conectarse a cada controlador y proporciona un ejemplo de los pares palabra clave-valor utilizado con **SQLDriverConnect**. Para obtener una lista completa de valores DRIVERID, consulte [SQLConfigDataSource](../../odbc/microsoft/sqlconfigdatasource-paradox-driver.md).  
  
> [!NOTE]  
>  Si DBQ o valor de esta opción no se especifica para el controlador de Paradox, el controlador se conectará al directorio actual.  
  
|Controlador|Palabras clave necesaria|Ejemplo|  
|------------|-----------------------|-------------|  
|Paradox|Controlador, DriverID|Driver = {Microsoft Paradox Driver (*.db)}; DBQ = c:\temp; DriverID = 26|
