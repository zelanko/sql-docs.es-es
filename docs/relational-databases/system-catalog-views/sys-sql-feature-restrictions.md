---
title: sys.sql_feature_restrictions (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 01/20/2016
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
ms.openlocfilehash: 9ffdcaaefe60c1972993501814cae555fb907f26
ms.sourcegitcommit: 561cee96844b82ade6cf543a228028ad5c310768
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/04/2019
ms.locfileid: "66507003"
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