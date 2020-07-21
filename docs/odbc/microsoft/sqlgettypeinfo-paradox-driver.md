---
title: SQLGetTypeInfo (controlador de Paradox) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SQLGetTypeInfo function [ODBC], Paradox Driver
- Paradox driver [ODBC], SQLGetTypeInfo
ms.assetid: e65063c7-ba9e-4cf0-ac13-4bb5bd2937db
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 693441c088865be85b18106a4c769a9f3f676f13
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/26/2020
ms.locfileid: "81295105"
---
# <a name="sqlgettypeinfo-paradox-driver"></a>SQLGetTypeInfo (controlador de Paradox)
> [!NOTE]  
>  En este tema se proporciona información específica del controlador de Paradox. Para obtener información general sobre esta función, vea el tema correspondiente en referencia de la [API de ODBC](../../odbc/reference/syntax/odbc-api-reference.md).  
  
 El nombre del tipo (TYPE_NAME) devuelto en la tabla generada por **SQLGetTypeInfo** será el nombre utilizado con más frecuencia por el origen de datos.  
  
 SQL_ALL_EXCEPT_LIKE se devolverán en la columna en la que se pueden buscar los tipos de datos byte, Counter, Double, single, Long y Short. (La capacidad LIKE se puede lograr convirtiendo el valor en un carácter mediante las funciones de conversión canónica de ODBC y, a continuación, realizando la comparación).
