---
title: SQLProcedureColumns (controlador de Access) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- Access driver [ODBC], SQLProcedureColumns
- SQLProcedureColumns function [ODBC], Access Driver
ms.assetid: 34fee995-5848-4ecb-bda0-fc362a77b2d9
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: a438823d1aa71eecb25c4935026c1b43e45842d1
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/01/2018
ms.locfileid: "47812703"
---
# <a name="sqlprocedurecolumns-access-driver"></a>SQLProcedureColumns (controlador de Access)
> [!NOTE]  
>  En este tema se proporciona información específica del controlador de acceso. Para obtener información general acerca de esta función, vea el tema correspondiente en [referencia de la API de ODBC](../../odbc/reference/syntax/odbc-api-reference.md).  
  
 Los desarrolladores de aplicaciones deberían buscar columnas definidos por el controlador de inicio al final del conjunto de resultados y continuando hacia atrás.  
  
|columna|Comentarios|  
|------------|--------------|  
|COLUMN_TYPE|SQL_PARAM_INPUT o SQL_RESULT_COL|  
|ORDINAL|Se trata de una columna específica del controlador que se devuelve al final del conjunto de resultados. El tipo SQL de la columna es un entero.|
