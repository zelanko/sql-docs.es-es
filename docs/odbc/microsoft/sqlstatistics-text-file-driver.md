---
title: SQLStatistics (controlador de archivo de texto) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- text file driver [ODBC], SQLStatistics
- SQLStatistics function [ODBC], Text File Driver
ms.assetid: 311afc01-d656-425f-be43-4a8e7cbc9a97
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 76b9810236b4ec415f8abb8ecefca748c13b51c8
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/27/2020
ms.locfileid: "81299315"
---
# <a name="sqlstatistics-text-file-driver"></a>SQLStatistics (controlador de archivo de texto)
> [!NOTE]  
>  En este tema se proporciona información específica del controlador de archivo de texto. Para obtener información general sobre esta función, vea el tema correspondiente en referencia de la [API de ODBC](../../odbc/reference/syntax/odbc-api-reference.md).  
  
|Columna|Comentarios|  
|------------|--------------|  
|TABLE_QUALIFIER|La ruta de acceso a un directorio.<br /><br /> No se admite la coincidencia de patrones en el argumento *szTableQualifier* .|  
|TABLE_OWNER|Se devuelve NULL en esta columna porque no se admite el nombre del propietario.|  
|TABLE_NAME|Nombre de tabla no delimitado.<br /><br /> No se admite la coincidencia de patrones en el argumento *szTableName* .|  
|INDEX_QUALIFIER|Siempre se devuelve NULL.|  
|INDEX_NAME|Dependiente del índice.|  
|TYPE|Solo se devolverá SQL_TABLE_STAT o SQL_INDEX_OTHER para el tipo.|  
|SEQ_IN_INDEX|Dependiente del índice.|  
|COLUMN_NAME|Dependiente del índice.|  
|COLLATION|Dependiente del índice.|  
|PAGES|Siempre se devuelve NULL.|  
  
 El filtrado se basa en la unicidad (el argumento *fUnique* ). Se omite el parámetro *fAccuracy* .
