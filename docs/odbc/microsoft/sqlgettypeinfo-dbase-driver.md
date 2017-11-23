---
title: SQLGetTypeInfo (controlador dBASE) | Documentos de Microsoft
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: microsoft
ms.reviewer: 
ms.suite: sql
ms.technology: drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- SQLGetTypeInfo function [ODBC], dBASE Driver
- DBase driver [ODBC], SQLGetTypeInfo
ms.assetid: 6e9ce02b-97c7-4c1a-91e0-829df7459c84
caps.latest.revision: "6"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 46c81ee7aa70ff01a6a284da6612f9fb965c0cad
ms.sourcegitcommit: 7f8aebc72e7d0c8cff3990865c9f1316996a67d5
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/20/2017
---
# <a name="sqlgettypeinfo-dbase-driver"></a>SQLGetTypeInfo (dBASE controlador)
> [!NOTE]  
>  Este tema proporciona información de dBASE específicos del controlador. Para obtener información general acerca de esta función, vea el tema correspondiente en [referencia de la API de ODBC](../../odbc/reference/syntax/odbc-api-reference.md).  
  
 Devuelve el nombre del tipo (TYPE_NAME) en la tabla generada por **SQLGetTypeInfo** será el nombre más utilizado por el origen de datos.  
  
 SQL_ALL_EXCEPT_LIKE se devolverán en la columna de búsqueda para el Byte, contador, Double, tipos de datos único, larga y corta. (La capacidad de LIKE se consigue convertir el valor a un carácter mediante las funciones de conversión canónica de ODBC, a continuación, realizar la comparación.)
