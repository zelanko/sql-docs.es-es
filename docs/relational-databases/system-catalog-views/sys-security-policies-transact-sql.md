---
title: Sys.security_policies (Transact-SQL) | Documentos de Microsoft
ms.custom: 
ms.date: 06/10/2016
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database
ms.service: 
ms.component: system-catalog-views
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
applies_to:
- Azure SQL Database
- SQL Server 2016 Preview
f1_keywords:
- SYS.SECURITY_POLICIES_TSQL
- SECURITY_POLICIES_TSQL
- SYS.SECURITY_POLICIES
- SECURITY_POLICIES
dev_langs:
- TSQL
helpviewer_keywords:
- sys.security_policies catalog view
- security_policies catalog view
ms.assetid: 35362f5b-e601-4049-9e1d-c5307e823831
caps.latest.revision: 
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 9e30a903e31ce8ba7951f9756a8fd258375fb8e2
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/21/2017
---
# <a name="syssecuritypolicies-transact-sql"></a>Sys.security_policies (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2016-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2016-asdb-xxxx-xxx-md.md)]

  Devuelve una fila para cada directiva de seguridad de la base de datos.  
  
|Nombre de columna|Tipo de datos|Descripción|  
|-----------------|---------------|-----------------|  
|name|**sysname**|Nombre de la directiva de seguridad, único dentro de la base de datos.|  
|object_id|**int**|Identificador de la directiva de seguridad.|  
|principal_id|**int**|Identificador del propietario de la directiva de seguridad, tal y como se registró en la base de datos. Es NULL si el propietario se determina con el esquema.|  
|schema_id|**int**|Identificador del esquema en el que reside el objeto.|  
|parent_object_id|**int**|Identificador del objeto al que pertenece la directiva. Debe ser 0.|  
|Tipo|**vachar(2)**|Debe ser **SP**.|  
|type_desc|**nvarchar (60)**|**SECURITY_POLICY**.|  
|create_date|**datetime**|Fecha UTC de creación de la directiva de seguridad.|  
|modify_date|**datetime**|Fecha UTC en la que la directiva de seguridad se modificó por última vez.|  
|is_ms_shipped|**bit**|Siempre false.|  
|is_enabled|**bit**|Estado de la especificación de la directiva de seguridad:<br /><br /> 0 = deshabilitado<br /><br /> 1 = habilitado|  
|is_not_for_replication|**bit**|La directiva se creó con la opción NOT FOR REPLICATION.|  
|uses_database_collation|**bit**|Utiliza la misma intercalación que la base de datos.|  
|is_schemabinding_enabled|**bit**|Estado de SCHEMABINDING para la directiva de seguridad:<br /><br /> 0 o NULL = habilitado<br /><br /> 1 = deshabilitado|  
  
## <a name="permissions"></a>Permissions  
 Entidades de seguridad con la **ALTER ANY SECURITY POLICY** permiso tiene acceso a todos los objetos en esta vista de catálogo, así como cualquier persona con **VIEW DEFINITION** en el objeto.  
  
## <a name="see-also"></a>Vea también  
 [Seguridad de nivel de fila](../../relational-databases/security/row-level-security.md)   
 [sys.security_predicates &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-security-predicates-transact-sql.md)   
 [CREATE SECURITY POLICY &#40;Transact-SQL&#41;](../../t-sql/statements/create-security-policy-transact-sql.md)   
 [Vistas de catálogo de seguridad &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/security-catalog-views-transact-sql.md)   
 [Vistas de catálogo &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/catalog-views-transact-sql.md)   
 [Entidades de seguridad &#40;motor de base de datos&#41;](../../relational-databases/security/authentication-access/principals-database-engine.md)  
  
  
