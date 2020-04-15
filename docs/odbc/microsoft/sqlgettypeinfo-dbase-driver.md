---
title: SQLGetTypeInfo (controlador dBASE) Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SQLGetTypeInfo function [ODBC], dBASE Driver
- DBase driver [ODBC], SQLGetTypeInfo
ms.assetid: 6e9ce02b-97c7-4c1a-91e0-829df7459c84
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 711652e22318d089b02fe8e79cb592f0a42dfff9
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/14/2020
ms.locfileid: "81295135"
---
# <a name="sqlgettypeinfo-dbase-driver"></a>SQLGetTypeInfo (dBASE controlador)
> [!NOTE]  
>  En este tema se proporciona información específica del controlador dBASE. Para obtener información general sobre esta función, consulte el tema adecuado en Referencia de [la API ODBC](../../odbc/reference/syntax/odbc-api-reference.md).  
  
 El nombre del tipo (TYPE_NAME) devuelto en la tabla generada por **SQLGetTypeInfo** será el nombre más utilizado por el origen de datos.  
  
 SQL_ALL_EXCEPT_LIKE se devolverá en la columna SEARCHABLE para los tipos de datos Byte, Counter, Double, Single, Long y Short. (La capacidad LIKE se puede lograr convirtiendo el valor en un carácter mediante las funciones de conversión canónica ODBC y, a continuación, realizando la comparación.)
