---
title: SQLTables (controlador de acceso) | Documentos de Microsoft
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
- SQLTables function [ODBC], Access Driver
- Access driver [ODBC], SQLTables
ms.assetid: 94423cf9-341a-4db6-bb10-8f5448df7fc3
caps.latest.revision: 6
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 4f6ca61bf3bc72e5640271e1eaed55cd10664d04
ms.contentlocale: es-es
ms.lasthandoff: 09/09/2017

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
 [SQLTables, función](../../odbc/reference/syntax/sqltables-function.md)

