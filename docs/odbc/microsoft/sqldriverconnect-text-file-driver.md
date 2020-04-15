---
title: SQLDriverConnect (Controlador de archivo de texto) Microsoft Docs
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
ms.openlocfilehash: 2768669b7dbb2066de0acedd5711911be0eac8fa
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/14/2020
ms.locfileid: "81307106"
---
# <a name="sqldriverconnect-text-file-driver"></a>SQLDriverConnect (controlador de archivo de texto)
> [!NOTE]  
>  En este tema se proporciona información específica del controlador de archivo de texto. Para obtener información general sobre esta función, consulte el tema adecuado en Referencia de [la API ODBC](../../odbc/reference/syntax/odbc-api-reference.md).  
  
 **SQLDriverConnect** le permite conectarse a un controlador sin crear un origen de datos (DSN).  
  
 Las siguientes palabras clave se admiten en la cadena de conexión para todos los controladores: **DSN**, **DBQ**y **FIL**.  
  
 En la tabla siguiente se muestran las palabras clave mínimas necesarias para conectarse a cada controlador y se proporciona un ejemplo de pares de palabra clave/valor utilizados con **SQLDriverConnect**. Para obtener una lista completa de los valores DRIVERID, vea [SQLConfigDataSource](../../odbc/microsoft/sqlconfigdatasource-text-file-driver.md).  
  
> [!NOTE]  
>  Si dbQ o DefaultDir no se especifica para el controlador de texto, el controlador se conectará al directorio actual.  
  
|Controlador|Palabras clave requeridas|Ejemplos|  
|------------|-----------------------|--------------|  
|Texto|Controlador|Controlador de microsoft Text Driver\*(*.txt; . csv)-; DefaultDir-c:-temp|
