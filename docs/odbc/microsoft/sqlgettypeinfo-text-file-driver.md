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
ms.openlocfilehash: 2659b3251cf77882f3762ce5699c36441e6c8ebc
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/15/2019
ms.locfileid: "67898646"
---
# <a name="sqlgettypeinfo-text-file-driver"></a>SQLGetTypeInfo (controlador de archivo de texto)
> [!NOTE]  
>  En este tema se proporciona información específica del controlador de archivo de texto. Para obtener información general acerca de esta función, vea el tema correspondiente en [referencia de la API de ODBC](../../odbc/reference/syntax/odbc-api-reference.md).  
  
 Devuelve el nombre del tipo (TYPE_NAME) en la tabla generada por **SQLGetTypeInfo** será el nombre más utilizado por el origen de datos.  
  
 SQL_ALL_EXCEPT_LIKE se devolverá en la columna de búsqueda para el Byte, contador, Double, tipos de datos único, larga y corta. (La capacidad similar puede lograrse mediante la conversión del valor en un carácter mediante las funciones de conversión canónica de ODBC, a continuación, realizar la comparación).  
  
 Cuando se usa el controlador de texto, **SQLGetTypeInfo** devuelve un valor CASE_SENSITIVE es False para el texto (CHAR y LONGCHAR), los tipos de datos cuando los tipos de datos realmente distinguen mayúsculas de minúsculas.
