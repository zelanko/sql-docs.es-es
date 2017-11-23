---
title: QUITAR la directiva de seguridad (Transact-SQL) | Documentos de Microsoft
ms.custom: 
ms.date: 05/11/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database
ms.service: 
ms.component: t-sql|statements
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- DROP_SECURITY_POLICY_TSQL
- DROP SECURITY POLICY
- DROP SECURITY
- DROP_SECURITY_TSQL
dev_langs: TSQL
helpviewer_keywords: DROP SECURITY POLICY statement
ms.assetid: 5bd3393d-2fa5-4db0-a69a-a1a72d638e9d
caps.latest.revision: "8"
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 251fecc3ef17dc575308a9a0adf05e0643245c58
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/21/2017
---
# <a name="drop-security-policy-transact-sql"></a>QUITAR la directiva de seguridad (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2016-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2016-asdb-xxxx-xxx-md.md)]

  Elimina una directiva de seguridad.  
  
 ![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxis  
  
```  
DROP SECURITY POLICY [ IF EXISTS ] [schema_name. ] security_policy_name    
[;]  
```  
  
## <a name="arguments"></a>Argumentos  
 *IF EXISTE*  
 **Se aplica a**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ([!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] a través de la [versión actual](http://go.microsoft.com/fwlink/p/?LinkId=299658)).  
  
 Condicionalmente quita la directiva de seguridad solamente si ya existe.  
  
 *schema_name*  
 Es el nombre del esquema al que pertenece la directiva de seguridad.  
  
 *security_policy_name*  
 El nombre de la directiva de seguridad. Los nombres de directivas de seguridad deben seguir las reglas de los identificadores y deben ser únicos en la base de datos y para su esquema.  
  
## <a name="remarks"></a>Comentarios  
  
## <a name="permissions"></a>Permissions  
 Requiere el permiso ALTER ANY SECURITY POLICY y el permiso ALTER en el esquema.  
  
## <a name="example"></a>Ejemplo  
  
```  
DROP SECURITY POLICY secPolicy;  
```  
  
## <a name="see-also"></a>Vea también  
 [Seguridad de nivel de fila](../../relational-databases/security/row-level-security.md)   
 [CREATE SECURITY POLICY &#40;Transact-SQL&#41;](../../t-sql/statements/create-security-policy-transact-sql.md)   
 [ALTER SECURITY POLICY &#40;Transact-SQL&#41;](../../t-sql/statements/alter-security-policy-transact-sql.md)   
 [sys.security_policies &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-security-policies-transact-sql.md)   
 [Sys.security_predicates &#40; Transact-SQL &#41;](../../relational-databases/system-catalog-views/sys-security-predicates-transact-sql.md)  
  
  
