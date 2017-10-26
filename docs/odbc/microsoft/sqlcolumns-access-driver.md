---
title: SQLColumns (controlador de acceso) | Documentos de Microsoft
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- SQLColumns function [ODBC], Access Driver
- Access driver [ODBC], SQLColumns
ms.assetid: 1eac255c-6110-4805-a1bc-feee1eec35d0
caps.latest.revision: 6
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 6359fe8948e670a05a076537e2acf3e28b3cba1d
ms.contentlocale: es-es
ms.lasthandoff: 09/09/2017

---
# <a name="sqlcolumns-access-driver"></a>SQLColumns (controlador de Access)
> [!NOTE]  
>  En este tema se proporciona información específica del controlador de acceso. Para obtener información general acerca de esta función, vea el tema correspondiente en [referencia de la API de ODBC](../../odbc/reference/syntax/odbc-api-reference.md).  
  
|Columna|Comentarios|  
|------------|--------------|  
|TABLE_QUALIFIER|Se devuelve la ruta de acceso a un archivo de base de datos.|  
|TABLE_OWNER|Se devuelve NULL en esta columna porque no se admite el nombre del propietario.|  
|NULLABLE|SQL_NO_NULLS se devuelve para las columnas que participan en una clave principal o índice único.|

