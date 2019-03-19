---
title: sys.security_predicates (Transact-SQL) | Microsoft Docs
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
manager: craigg
monikerRange: =azuresqldb-current||>=sql-server-2016||=azure-sqldw-latest||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 48505a7e33d8d691314216846ee054d6625b7cf4
ms.sourcegitcommit: 11ab8a241a6d884b113b3cf475b2b9ed61ff00e3
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 03/18/2019
ms.locfileid: "58161802"
---
# <a name="syssecuritypredicates-transact-sql"></a>sys.security_predicates (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2016-asdb-asdw-xxx-md](../../includes/tsql-appliesto-ss2016-asdb-asdw-xxx-md.md)]

  Devuelve una fila para cada predicado de seguridad de la base de datos.  
  
|Nombre de columna|Tipo de datos|Descripción|  
|-----------------|---------------|-----------------|  
|object_id|**int**|Identificador de la directiva de seguridad que contiene este predicado.|  
|security_predicate_id|**int**|Identificador del predicado dentro de esta directiva de seguridad.|  
|target_object_id|**int**|Identificador del objeto en el que está enlazado el predicado de seguridad.|  
|predicate_definition|**nvarchar(max)**|Nombre completo de la función que se utilizará como predicado de seguridad, incluidos los argumentos. Tenga en cuenta que el nombre `schema.function` puede estar normalizado (es decir, convertido), así como cualquier otro elemento en el texto para mantener la coherencia. Por ejemplo:<br /><br /> `[dbo].[fn_securitypredicate]([wing], [startTime], [endTime])`|  
|predicate_type|**int**|El tipo de predicado que se usa la directiva de seguridad:<br /><br /> 0 = EL PREDICADO DE FILTRO<br /><br /> 1 = EL PREDICADO DE BLOQUEO|  
|predicate_type_desc|**nvarchar(60)**|El tipo de predicado que se usa la directiva de seguridad:<br /><br /> FILTER<br /><br /> BLOQUE|  
|operación|**int**|El tipo de operación especificada para el predicado:<br /><br /> NULL = todas las operaciones aplicables<br /><br /> 1 = DESPUÉS DE INSERTAR<br /><br /> 2 = DESPUÉS DE LA ACTUALIZACIÓN<br /><br /> 3 = ANTES DE LA ACTUALIZACIÓN<br /><br /> 4 = ANTES DE ELIMINAR|  
|operation_desc|**nvarchar(60)**|El tipo de operación especificada para el predicado:<br /><br /> NULL<br /><br /> DESPUÉS DE INSERTAR<br /><br /> AFTER UPDATE<br /><br /> ANTES DE LA ACTUALIZACIÓN<br /><br /> ANTES DE ELIMINAR|  
  
## <a name="permissions"></a>Permisos  
 Las entidades de seguridad con el **ALTER ANY SECURITY POLICY** permiso tiene acceso a todos los objetos en esta vista de catálogo, así como cualquier persona con **VIEW DEFINITION** en el objeto.  
  
## <a name="see-also"></a>Vea también  
 [Seguridad de nivel de fila](../../relational-databases/security/row-level-security.md)   
 [sys.security_policies &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-security-policies-transact-sql.md)   
 [CREATE SECURITY POLICY &#40;Transact-SQL&#41;](../../t-sql/statements/create-security-policy-transact-sql.md)   
 [Vistas de catálogo de seguridad &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/security-catalog-views-transact-sql.md)   
 [Vistas de catálogo &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/catalog-views-transact-sql.md)   
 [Entidades de seguridad &#40;motor de base de datos&#41;](../../relational-databases/security/authentication-access/principals-database-engine.md)  
  
  
