---
title: SQLColumns (Controlador de archivo de texto) Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- text file driver [ODBC], SQLColumns
- SQLColumns function [ODBC], Text File Driver
ms.assetid: c99e5f8d-4e43-48f8-9e0e-086707b411f5
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 78c2e20f12dedf399ab36dd908f83aa93bebffc4
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/14/2020
ms.locfileid: "81307876"
---
# <a name="sqlcolumns-text-file-driver"></a>SQLColumns (controlador de archivo de texto)
> [!NOTE]  
>  En este tema se proporciona información específica del controlador de archivo de texto. Para obtener información general sobre esta función, consulte el tema adecuado en Referencia de [la API ODBC](../../odbc/reference/syntax/odbc-api-reference.md).  
  
|Columna|Comentarios|  
|------------|--------------|  
|TABLE_QUALIFIER|Se devuelve la ruta de acceso a un directorio.|  
|TABLE_OWNER|NULL se devuelve en esta columna porque no se admite el nombre del propietario.|  
|NULLABLE|SQL_NO_NULLS se devuelve para las columnas que participan en una clave principal o un índice único.|
