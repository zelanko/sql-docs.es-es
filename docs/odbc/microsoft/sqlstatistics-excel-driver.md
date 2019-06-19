---
title: SQLStatistics (controlador de Excel) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- Excel driver [ODBC], SQLStatistics
- SQLStatistics function [ODBC], Excel Driver
ms.assetid: 02506664-8dcc-4bd0-a8bb-d49fcbdd5722
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 044ea7e2c536685afef3534eacb5745fb33edf49
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/15/2019
ms.locfileid: "63135284"
---
# <a name="sqlstatistics-excel-driver"></a>SQLStatistics (controlador de Excel)
> [!NOTE]  
>  En este tema se proporciona información específica del controlador de Excel. Para obtener información general acerca de esta función, vea el tema correspondiente en [referencia de la API de ODBC](../../odbc/reference/syntax/odbc-api-reference.md).  
  
|columna|Comentarios|  
|------------|--------------|  
|TABLE_QUALIFIER|La ruta de acceso a un directorio.<br /><br /> No se admite la coincidencia de patrones en el *szTableQualifier* argumento.|  
|TABLE_OWNER|Se devuelve NULL en esta columna porque no se admite el nombre del propietario.|  
|TABLE_NAME|Nombre de tabla no delimitado.<br /><br /> No se admite la coincidencia de patrones en el *szTableName* argumento.|  
|INDEX_QUALIFIER|Siempre se devuelve NULL.|  
|INDEX_NAME|Dependientes del índice.|  
|TYPE|Para el tipo se devolverá sólo SQL_TABLE_STAT o SQL_INDEX_OTHER.|  
|SEQ_IN_INDEX|Dependientes del índice.|  
|COLUMN_NAME|Dependientes del índice.|  
|COLLATION|Dependientes del índice.|  
|PAGES|Siempre se devuelve NULL.|  
  
 El filtrado se basa en la unicidad (la *fUnique* argumento). El *fAccuracy* parámetro se omite.
