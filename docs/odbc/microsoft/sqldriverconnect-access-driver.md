---
title: SQLDriverConnect (controlador de Access) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- Access driver [ODBC], SQLDriverConnect
- SQLDriverConnect function [ODBC], Access Driver
ms.assetid: 9d133e9b-7545-464d-aa3c-677fa7e2a41d
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 9a71874c91e48c25072fbfed8f66a312d65b4697
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/01/2018
ms.locfileid: "47626389"
---
# <a name="sqldriverconnect-access-driver"></a>SQLDriverConnect (controlador de Access)
> [!NOTE]  
>  En este tema se proporciona información específica del controlador de acceso. Para obtener información general acerca de esta función, vea el tema correspondiente en [referencia de la API de ODBC](../../odbc/reference/syntax/odbc-api-reference.md).  
  
 **SQLDriverConnect** le permite conectarse a un controlador sin necesidad de crear un origen de datos (DSN).  
  
 Se admiten las siguientes palabras clave en la cadena de conexión para todos los controladores: **DSN**, **DBQ**, y **FIL**.  
  
 El **UID** y **PWD** también son compatibles con las palabras clave.  
  
 No debe incluir la palabra clave PWD cualquiera de los caracteres especiales (consulte SQL_SPECIAL_CHARACTERS en **SQLGetInfo** devuelven valores).  
  
 En la tabla siguiente muestra las palabras clave mínimas necesarias para conectarse a cada controlador y proporciona un ejemplo de pares de palabra clave y valor utilizada con **SQLDriverConnect**. Para obtener una lista completa de valores DRIVERID, consulte [SQLConfigDataSource](../../odbc/microsoft/sqlconfigdatasource-access-driver.md).  
  
|Controlador|Palabras clave necesarias|Ejemplos|  
|------------|-----------------------|--------------|  
|Microsoft Access|Controlador, DBQ|Driver = {controlador de Microsoft Access (*.mdb)}; DBQ = c:\\\temp\\\sample.mdb|
