---
title: SQLTables (controlador de paradoja) Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- Paradox driver [ODBC], SQLTables
- SQLTables function [ODBC], Paradox Driver
ms.assetid: d68adad6-97bd-4b47-bcf9-0102aafb00d4
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: aa13b5395d8f3c2cb470a4eff1b1ef02a43bad53
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/14/2020
ms.locfileid: "81299295"
---
# <a name="sqltables-paradox-driver"></a>SQLTables (controlador de Paradox)
> [!NOTE]  
>  En este tema se proporciona información específica del controlador de Paradox. Para obtener información general sobre esta función, consulte el tema adecuado en Referencia de [la API ODBC](../../odbc/reference/syntax/odbc-api-reference.md).  
  
|Argumento|Comentarios|  
|--------------|--------------|  
|*szTableOwner*|El único argumento válido para *szTableOwner* es NULL porque ninguno de los controladores admite nombres de propietario. Con *szTableOwner* establecido en NULL, se devuelven todas las tablas. NULL se devuelve en la columna TABLE_OWNER.|  
|*szTableQualifier*|En la columna TABLE_QUALIFIER, **SQLTables** devolverá la ruta de acceso a un directorio.|  
|*SzTableType*|Para los archivos Paradox, "TABLE" es el único tipo de tabla admitido.|  
  
## <a name="see-also"></a>Consulte también  
 [Función SQLTables](../../odbc/reference/syntax/sqltables-function.md)
