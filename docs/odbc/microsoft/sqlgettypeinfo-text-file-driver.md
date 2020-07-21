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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 7b70b58e4760959db102450b5f8b7beed042df95
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/26/2020
ms.locfileid: "81295005"
---
# <a name="sqlgettypeinfo-text-file-driver"></a>SQLGetTypeInfo (controlador de archivo de texto)
> [!NOTE]  
>  En este tema se proporciona información específica del controlador de archivo de texto. Para obtener información general sobre esta función, vea el tema correspondiente en referencia de la [API de ODBC](../../odbc/reference/syntax/odbc-api-reference.md).  
  
 El nombre del tipo (TYPE_NAME) devuelto en la tabla generada por **SQLGetTypeInfo** será el nombre utilizado con más frecuencia por el origen de datos.  
  
 SQL_ALL_EXCEPT_LIKE se devolverán en la columna en la que se pueden buscar los tipos de datos byte, Counter, Double, single, Long y Short. (La capacidad LIKE se puede lograr convirtiendo el valor en un carácter mediante las funciones de conversión canónica de ODBC y realizando la comparación).  
  
 Cuando se usa el controlador de texto, **SQLGetTypeInfo** devuelve un valor de CASE_SENSITIVE false para los tipos de datos de texto (char y LONGCHAR), cuando los tipos de datos realmente distinguen mayúsculas de minúsculas.
