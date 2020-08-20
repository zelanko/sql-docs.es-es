---
description: SQLTables (controlador de Paradox)
title: SQLTables (controlador de Paradox) | Microsoft Docs
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
ms.openlocfilehash: 5da80e16a63431bd7a0ddf46c2efaa236ecefd3e
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/17/2020
ms.locfileid: "88500138"
---
# <a name="sqltables-paradox-driver"></a>SQLTables (controlador de Paradox)
> [!NOTE]  
>  En este tema se proporciona información específica del controlador de Paradox. Para obtener información general sobre esta función, vea el tema correspondiente en referencia de la [API de ODBC](../../odbc/reference/syntax/odbc-api-reference.md).  
  
|Argumento|Comentarios|  
|--------------|--------------|  
|*szTableOwner*|El único argumento válido para *szTableOwner* es null porque ninguno de los controladores admite nombres de propietario. Con *szTableOwner* establecido en null, se devuelven todas las tablas. Se devuelve NULL en el TABLE_OWNER columna.|  
|*szTableQualifier*|En la columna TABLE_QUALIFIER, **SQLTables** devolverá la ruta de acceso a un directorio.|  
|*SzTableType*|En el caso de los archivos de Paradox, "tabla" es el único tipo de tabla admitido.|  
  
## <a name="see-also"></a>Consulte también  
 [Función SQLTables](../../odbc/reference/syntax/sqltables-function.md)
