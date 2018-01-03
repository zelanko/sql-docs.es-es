---
title: SQLTables (controlador de acceso) | Documentos de Microsoft
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: odbc
ms.reviewer: 
ms.suite: sql
ms.technology: drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- SQLTables function [ODBC], Access Driver
- Access driver [ODBC], SQLTables
ms.assetid: 94423cf9-341a-4db6-bb10-8f5448df7fc3
caps.latest.revision: "6"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 895c4d86c11d88fcf544b9a3c7612e1a6cdf4764
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 12/21/2017
---
# <a name="sqltables-access-driver"></a>SQLTables (controlador de Access)
> [!NOTE]  
>  En este tema se proporciona información específica del controlador de acceso. Para obtener información general acerca de esta función, vea el tema correspondiente en [referencia de la API de ODBC](../../odbc/reference/syntax/odbc-api-reference.md).  
  
|Argumento|Comentarios|  
|--------------|--------------|  
|*szTableOwner*|El argumento solo es válido para *szTableOwner* es NULL porque ninguno de los controladores admite nombres de propietario. Con *szTableOwner* establecido en NULL, se devuelven todas las tablas. Se devuelve NULL en la columna TABLE_OWNER.|  
|*szTableQualifier*|En la columna TABLE_QUALIFIER, **SQLTables** devolverá la ruta de acceso a un archivo de base de datos.|  
|*SzTableType*|Cuando se utiliza el controlador de Microsoft Access, "Tabla del sistema" se admite para *szTableType* para las tablas del sistema, "Sinónimo" se admite para tablas asociadas, y se admite la "Vista" para devolver filas consultas.|  
  
## <a name="see-also"></a>Vea también  
 [Función SQLTables](../../odbc/reference/syntax/sqltables-function.md)
