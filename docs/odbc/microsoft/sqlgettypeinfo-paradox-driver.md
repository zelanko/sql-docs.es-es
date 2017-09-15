---
title: SQLGetTypeInfo (controlador de Paradox) | Documentos de Microsoft
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
- SQLGetTypeInfo function [ODBC], Paradox Driver
- Paradox driver [ODBC], SQLGetTypeInfo
ms.assetid: e65063c7-ba9e-4cf0-ac13-4bb5bd2937db
caps.latest.revision: 6
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 1c95d4c4519b420324e9ec1364d2ac9f352ba346
ms.contentlocale: es-es
ms.lasthandoff: 09/09/2017

---
# <a name="sqlgettypeinfo-paradox-driver"></a>SQLGetTypeInfo (controlador de Paradox)
> [!NOTE]  
>  En este tema se proporciona información específica del controlador Paradox. Para obtener información general acerca de esta función, vea el tema correspondiente en [referencia de la API de ODBC](../../odbc/reference/syntax/odbc-api-reference.md).  
  
 Devuelve el nombre del tipo (TYPE_NAME) en la tabla generada por **SQLGetTypeInfo** será el nombre más utilizado por el origen de datos.  
  
 SQL_ALL_EXCEPT_LIKE se devolverán en la columna de búsqueda para el Byte, contador, Double, tipos de datos único, larga y corta. (La capacidad LIKE se puede lograr mediante la conversión del valor en un carácter utilizando las funciones de conversión canónica de ODBC y, a continuación, realizar la comparación.)
