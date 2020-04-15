---
title: SQLDriverConnect (controlador dBASE) Microsoft Docs
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
ms.openlocfilehash: 39d3d062ef8371ce37f812216cbb642d103eff98
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/14/2020
ms.locfileid: "81302926"
---
# <a name="sqldriverconnect-dbase-driver"></a>SQLDriverConnect (dBASE controlador)
> [!NOTE]  
>  En este tema se proporciona información específica del controlador dBASE. Para obtener información general sobre esta función, consulte el tema adecuado en Referencia de [la API ODBC](../../odbc/reference/syntax/odbc-api-reference.md).  
  
 **SQLDriverConnect** le permite conectarse a un controlador sin crear un origen de datos (DSN).  
  
 Las siguientes palabras clave se admiten en la cadena de conexión para todos los controladores: **DSN**, **DBQ**y **FIL**.  
  
 Cuando se utiliza el controlador Paradox, después de que un usuario haya abierto un archivo protegido con contraseña, otros usuarios no pueden abrir el mismo archivo.  
  
 En la tabla siguiente se muestran las palabras clave mínimas necesarias para conectarse a cada controlador y se proporciona un ejemplo de pares de palabra clave/valor utilizados con **SQLDriverConnect**. Para obtener una lista completa de los valores DRIVERID, vea [SQLConfigDataSource](../../odbc/microsoft/sqlconfigdatasource-dbase-driver.md).  
  
> [!NOTE]  
>  Si dbQ o DefaultDir no se especifica para el controlador dBASE, el controlador se conectará al directorio actual.  
  
|Controlador|Palabras clave requeridas|Ejemplos|  
|------------|-----------------------|--------------|  
|Dbase|Conductor, DriverID|Controlador de Microsoft dBASE Driver (*.dbf); DBQ-c:-temp; Id. de conductor 277|
