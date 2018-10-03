---
title: SQLGetTypeInfo (controlador de archivo de texto) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SQLGetTypeInfo function [ODBC], Text File Driver
- text file driver [ODBC], SQLGetTypeInfo
ms.assetid: 05a58975-093c-4bd9-bd72-b5f0026a6e36
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 3c1c38b66e9b8a3c1cbed4a3712f7af866935089
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/01/2018
ms.locfileid: "47847733"
---
# <a name="sqlgettypeinfo-text-file-driver"></a>SQLGetTypeInfo (controlador de archivo de texto)
> [!NOTE]  
>  En este tema se proporciona información específica del controlador de archivo de texto. Para obtener información general acerca de esta función, vea el tema correspondiente en [referencia de la API de ODBC](../../odbc/reference/syntax/odbc-api-reference.md).  
  
 Devuelve el nombre del tipo (TYPE_NAME) en la tabla generada por **SQLGetTypeInfo** será el nombre más utilizado por el origen de datos.  
  
 SQL_ALL_EXCEPT_LIKE se devolverá en la columna de búsqueda para el Byte, contador, Double, tipos de datos único, larga y corta. (La capacidad similar puede lograrse mediante la conversión del valor en un carácter mediante las funciones de conversión canónica de ODBC, a continuación, realizar la comparación).  
  
 Cuando se usa el controlador de texto, **SQLGetTypeInfo** devuelve un valor CASE_SENSITIVE es False para el texto (CHAR y LONGCHAR), los tipos de datos cuando los tipos de datos realmente distinguen mayúsculas de minúsculas.
