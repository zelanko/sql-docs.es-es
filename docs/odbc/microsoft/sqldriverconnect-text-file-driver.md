---
description: SQLDriverConnect (controlador de archivo de texto)
title: SQLDriverConnect (controlador de archivo de texto) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SQLDriverConnect function [ODBC], Text File Driver
- text file driver [ODBC], SQLDriverConnect
ms.assetid: d7769021-bd18-4d8e-96e0-e184a82d6ca3
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: c2eb5c35e9f6ae56caa3c6e4ca7473defe3b8bc0
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/17/2020
ms.locfileid: "88421809"
---
# <a name="sqldriverconnect-text-file-driver"></a>SQLDriverConnect (controlador de archivo de texto)
> [!NOTE]  
>  En este tema se proporciona información específica del controlador de archivo de texto. Para obtener información general sobre esta función, vea el tema correspondiente en referencia de la [API de ODBC](../../odbc/reference/syntax/odbc-api-reference.md).  
  
 **SQLDriverConnect** le permite conectarse a un controlador sin crear un origen de datos (DSN).  
  
 Las palabras clave siguientes se admiten en la cadena de conexión para todos los controladores: **DSN**, **DBQ**y **Fil**.  
  
 En la tabla siguiente se muestran las palabras clave mínimas necesarias para conectarse a cada controlador y se proporciona un ejemplo de pares de palabra clave y valor que se usan con **SQLDriverConnect**. Para obtener una lista completa de los valores de DRIVERID, consulte [SQLConfigDataSource](../../odbc/microsoft/sqlconfigdatasource-text-file-driver.md).  
  
> [!NOTE]  
>  Si no se especifica DBQ o DefaultDir para el controlador de texto, el controlador se conectará al directorio actual.  
  
|Controlador|Palabras clave necesarias|Ejemplos|  
|------------|-----------------------|--------------|  
|Texto|Controlador|Driver = {controlador de texto de Microsoft (*. txt; \* . CSV)}; DefaultDir = c:\temp|
