---
description: SQLProcedureColumns (controlador de Access)
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 289a4af7f329e88156e1ae3451f12aa40aeaa660
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/17/2020
ms.locfileid: "88500148"
---
# <a name="sqlprocedurecolumns-access-driver"></a>SQLProcedureColumns (controlador de Access)
> [!NOTE]  
>  En este tema se proporciona información específica del controlador de acceso. Para obtener información general sobre esta función, vea el tema correspondiente en referencia de la [API de ODBC](../../odbc/reference/syntax/odbc-api-reference.md).  
  
 Los desarrolladores de aplicaciones deben buscar las columnas definidas por el controlador a partir del final del conjunto de resultados y continuar.  
  
|Columna|Comentarios|  
|------------|--------------|  
|COLUMN_TYPE|SQL_PARAM_INPUT o SQL_RESULT_COL|  
|NÚMEROS|Se trata de una columna específica del controlador que se devuelve al final del conjunto de resultados. El tipo SQL de la columna es un entero.|
