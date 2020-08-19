---
description: Sys. security_predicates (Transact-SQL)
title: Sys. security_predicates (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- SYS.SECURITY_PREDICATES
- SECURITY_PREDICATES
- SECURITY_PREDICATES_TSQL
- SYS.SECURITY_PREDICATES_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.security_predicates catalog view
- security_predicates catalog view
ms.assetid: c7a2f28c-98da-463d-8b8a-8e5619e2c6a6
author: VanMSFT
ms.author: vanto
monikerRange: =azuresqldb-current||>=sql-server-2016||=azure-sqldw-latest||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: c2ba8b6c9c4a2fc2f6b3beb562edfac0728678fe
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/17/2020
ms.locfileid: "88490143"
---
# <a name="syssecurity_predicates-transact-sql"></a>Sys. security_predicates (Transact-SQL)
[!INCLUDE [sqlserver2016-asdb-asdbmi-asa](../../includes/applies-to-version/sqlserver2016-asdb-asdbmi-asa.md)]

  Devuelve una fila para cada predicado de seguridad en la base de datos.  
  
|Nombre de la columna|Tipo de datos|Descripción|  
|-----------------|---------------|-----------------|  
|object_id|**int**|Identificador de la directiva de seguridad que contiene este predicado.|  
|security_predicate_id|**int**|Identificador del predicado dentro de esta directiva de seguridad.|  
|target_object_id|**int**|Identificador del objeto en el que está enlazado el predicado de seguridad.|  
|predicate_definition|**nvarchar(max)**|Nombre completo de la función que se utilizará como predicado de seguridad, incluidos los argumentos. Tenga en cuenta que el nombre `schema.function` puede estar normalizado (es decir, convertido), así como cualquier otro elemento en el texto para mantener la coherencia. Por ejemplo:<br /><br /> `[dbo].[fn_securitypredicate]([wing], [startTime], [endTime])`|  
|predicate_type|**int**|El tipo de predicado utilizado por la Directiva de seguridad:<br /><br /> 0 = PREDICADO DE FILTRO<br /><br /> 1 = PREDICADO DE BLOQUE|  
|predicate_type_desc|**nvarchar(60)**|El tipo de predicado utilizado por la Directiva de seguridad:<br /><br /> FILTER<br /><br /> BLOQUEAR|  
|operation|**int**|El tipo de operación especificado para el predicado:<br /><br /> NULL = todas las operaciones aplicables<br /><br /> 1 = DESPUÉS DE LA INSERCIÓN<br /><br /> 2 = DESPUÉS DE LA ACTUALIZACIÓN<br /><br /> 3 = ANTES DE LA ACTUALIZACIÓN<br /><br /> 4 = ANTES DE LA ELIMINACIÓN|  
|operation_desc|**nvarchar(60)**|El tipo de operación especificado para el predicado:<br /><br /> NULL<br /><br /> DESPUÉS DE LA INSERCIÓN<br /><br /> AFTER UPDATE<br /><br /> ANTES DE LA ACTUALIZACIÓN<br /><br /> ANTES DE LA ELIMINACIÓN|  
  
## <a name="permissions"></a>Permisos  
 Las entidades de seguridad con el permiso **ALTER any Security Policy** tienen acceso a todos los objetos de esta vista de catálogo, así como a cualquier persona con **View definition** en el objeto.  
  
## <a name="see-also"></a>Consulte también  
 [Seguridad de nivel de fila](../../relational-databases/security/row-level-security.md)   
 [sys.security_policies &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-security-policies-transact-sql.md)   
 [CREATE SECURITY POLICY &#40;Transact-SQL&#41;](../../t-sql/statements/create-security-policy-transact-sql.md)   
 [Vistas de catálogo de seguridad &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/security-catalog-views-transact-sql.md)   
 [Vistas de catálogo &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/catalog-views-transact-sql.md)   
 [Entidades de seguridad &#40;motor de base de datos&#41;](../../relational-databases/security/authentication-access/principals-database-engine.md)  
  
  
