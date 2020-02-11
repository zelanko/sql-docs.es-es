---
title: SQLGetTypeInfo (controlador de Excel) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SQLGetTypeInfo function [ODBC], Excel Driver
- Excel driver [ODBC], SQLGetTypeInfo
ms.assetid: 708845be-e6a1-4677-8113-c52819a43fa4
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 227fef1ecd28e5099b599e86c82c3cc42fbacd0c
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/08/2020
ms.locfileid: "67898708"
---
# <a name="sqlgettypeinfo-excel-driver"></a>SQLGetTypeInfo (controlador de Excel)
> [!NOTE]  
>  En este tema se proporciona información específica del controlador de Excel. Para obtener información general sobre esta función, vea el tema correspondiente en referencia de la [API de ODBC](../../odbc/reference/syntax/odbc-api-reference.md).  
  
 El nombre del tipo (TYPE_NAME) devuelto en la tabla generada por **SQLGetTypeInfo** será el nombre utilizado con más frecuencia por el origen de datos.  
  
 SQL_ALL_EXCEPT_LIKE se devolverán en la columna en la que se pueden buscar los tipos de datos byte, Counter, Double, single, Long y Short. (La capacidad LIKE se puede lograr convirtiendo el valor en un carácter mediante las funciones de conversión canónica de ODBC y realizando la comparación).  
  
 Cuando se usa el controlador de Microsoft Excel, los nombres de tipo ODBC se devuelven en la TYPE_NAME columna devuelta por **SQLGetTypeInfo**.
