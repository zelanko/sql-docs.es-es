---
title: SQLStatistics (controlador de acceso) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- Access driver [ODBC], SQLStatistics
- SQLStatistics function [ODBC], Access Driver
ms.assetid: 6117ac77-1020-4f0c-8eed-e671c34c1f21
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: f75f41bf63cbf224772955effa0f120b5d384111
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/27/2020
ms.locfileid: "81299365"
---
# <a name="sqlstatistics-access-driver"></a>SQLStatistics (controlador de Access)
> [!NOTE]  
>  En este tema se proporciona información específica del controlador de acceso. Para obtener información general sobre esta función, vea el tema correspondiente en referencia de la [API de ODBC](../../odbc/reference/syntax/odbc-api-reference.md).  
  
|Columna|Comentarios|  
|------------|--------------|  
|TABLE_QUALIFIER|La ruta de acceso a un archivo de base de datos se devuelve para Microsoft Access.<br /><br /> No se admite la coincidencia de patrones en el argumento *szTableQualifier* .|  
|TABLE_OWNER|Se devuelve NULL en esta columna porque no se admite el nombre del propietario.|  
|TABLE_NAME|Nombre de tabla no delimitado.<br /><br /> No se admite la coincidencia de patrones en el argumento *szTableName* .|  
|INDEX_QUALIFIER|Siempre se devuelve NULL.|  
|INDEX_NAME|Dependiente del índice.|  
|TYPE|Solo se devolverá SQL_TABLE_STAT o SQL_INDEX_OTHER para el tipo.|  
|SEQ_IN_INDEX|Dependiente del índice.|  
|COLUMN_NAME|Dependiente del índice.|  
|COLLATION|Dependiente del índice.|  
|CARDINALITY|Solo se devuelve para Microsoft Access.|  
|PAGES|Siempre se devuelve NULL.|  
  
 El filtrado se basa en la unicidad (el argumento *fUnique* ). Se omite el parámetro *fAccuracy* .
