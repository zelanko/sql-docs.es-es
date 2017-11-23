---
title: SQLTables (controlador dBASE) | Documentos de Microsoft
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: microsoft
ms.reviewer: 
ms.suite: sql
ms.technology: drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- DBase driver [ODBC], SQLTables
- SQLTables function [ODBC], dBASE Driver
ms.assetid: 45938efb-b678-47d8-9345-644fa26ad679
caps.latest.revision: "6"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 83d58070e945c7ed68874aa3bd2d210e04f8bc6a
ms.sourcegitcommit: 7f8aebc72e7d0c8cff3990865c9f1316996a67d5
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/20/2017
---
# <a name="sqltables-dbase-driver"></a>SQLTables (dBASE controlador)
> [!NOTE]  
>  Este tema proporciona información de dBASE específicos del controlador. Para obtener información general acerca de esta función, vea el tema correspondiente en [referencia de la API de ODBC](../../odbc/reference/syntax/odbc-api-reference.md).  
  
|Argumento|Comentarios|  
|--------------|--------------|  
|*szTableOwner*|El argumento solo es válido para *szTableOwner* es NULL porque ninguno de los controladores es compatible con nombres de propietario. Con *szTableOwner* establecido en NULL, se devuelven todas las tablas. Se devuelve NULL en la columna TABLE_OWNER.|  
|*szTableQualifier*|En la columna TABLE_QUALIFIER, **SQLTables** devolverá la ruta de acceso a un directorio.|  
|*SzTableType*|Para los archivos de dBASE, "TABLE" es el único tipo de tabla admitido.|
