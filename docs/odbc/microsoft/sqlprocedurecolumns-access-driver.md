---
title: SQLProcedureColumns (controlador de acceso) | Documentos de Microsoft
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- Access driver [ODBC], SQLProcedureColumns
- SQLProcedureColumns function [ODBC], Access Driver
ms.assetid: 34fee995-5848-4ecb-bda0-fc362a77b2d9
caps.latest.revision: 6
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: c8a2f1fc2a37dcdce65a145eec966d3b118bf734
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/03/2018
---
# <a name="sqlprocedurecolumns-access-driver"></a>SQLProcedureColumns (controlador de Access)
> [!NOTE]  
>  En este tema se proporciona información específica del controlador de acceso. Para obtener información general acerca de esta función, vea el tema correspondiente en [referencia de la API de ODBC](../../odbc/reference/syntax/odbc-api-reference.md).  
  
 Los desarrolladores de aplicaciones deben buscar las columnas definidas por el controlador empezando por el final del conjunto de resultados y continuando hacia atrás.  
  
|Columna|Comentarios|  
|------------|--------------|  
|COLUMN_TYPE|SQL_PARAM_INPUT o SQL_RESULT_COL|  
|ORDINAL|Se trata de una columna específica del controlador que se devuelve al final del conjunto de resultados. El tipo SQL de la columna es un entero.|
