---
title: sys.sql_feature_restrictions (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 06/07/2019
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sys.sql_sql_feature_restrictions
dev_langs:
- TSQL
helpviewer_keywords:
- sys.sql_feature_restrictions catalog view
author: vainolo
ms.author: arib
manager: tomerw
monikerRange: '>= sql-server-ver15 || = sqlallproducts-allversions'
ms.openlocfilehash: b583afef9f52da7801384d4a7a9c76deaf8d4ee4
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/15/2019
ms.locfileid: "66822679"
---
# <a name="syssqlfeaturerestrictions-transact-sql"></a>sys.sql_feature_restrictions (Transact-SQL)

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

Devuelve una fila por cada restricción en la base de datos.
  
| Nombre de columna | Tipo de datos | Descripción |
|-------------|-----------|-------------|
| class       | nvarchar(128) | Clase de objeto al que se aplica la restricción |
| objeto      | nvarchar(256) | Nombre del objeto al que se aplica la restricción |
| Característica     | nvarchar(128) | Característica que está restringido |
  
## <a name="remarks"></a>Comentarios

Actualmente pueden restringirse las siguientes características:

| Característica          | Descripción |
|------------------|-------------|
| 'N'ErrorMessages | Cuando restringido, se enmascare los datos de usuario en el mensaje de error. |
| N'Waitfor'       | Cuando restringido, el comando devolverá inmediatamente sin ningún retraso. |
  
## <a name="permissions"></a>Permisos

La entidad que se está ejecuta debe tener el `CONTROL` permiso en la base de datos.
  
## <a name="see-also"></a>Vea también

 [Restricciones de características](../../relational-databases/security/feature-restrictions.md)
