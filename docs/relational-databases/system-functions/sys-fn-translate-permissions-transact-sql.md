---
title: Sys. fn_translate_permissions (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/15/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sys.fn_translate_permissions
- sys.fn_translate_permissions_TSQL
- fn_translate_permissions
- fn_translate_permissions_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- permissions bitmask [SQL Server]
- sys.fn_translate_permissions function
- fn_translate_permissions function
ms.assetid: ac97121f-2bd0-4f71-8e45-42c8584edbc5
author: rothja
ms.author: jroth
ms.openlocfilehash: c3d7a464f3faba633dd09be12ef4c3d006ef19ef
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/01/2020
ms.locfileid: "85738586"
---
# <a name="sysfn_translate_permissions-transact-sql"></a>sys.fn_translate_permissions (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/applies-to-version/sqlserver.md)]

  Traduce la máscara de bits de permisos devuelta por Seguimiento de SQL a una tabla de nombres de permisos.  
  
 ![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
sys.fn_translate_permissions ( level , perms )  
```  
  
## <a name="arguments"></a>Argumentos  
 *Nivel*  
 El tipo de elemento protegible al que se aplica el permiso. *LEVEL* es de tipo **nvarchar (60)**.  
  
 *perms*  
 Es una máscara de bits que se devuelve en la columna de permisos. *perms* es **varbinary (16)**.  
  
## <a name="returns"></a>Devoluciones  
 **table**  
  
## <a name="remarks"></a>Comentarios  
 El valor devuelto en la columna **Permissions** de un seguimiento de SQL es una representación de entero de una máscara de máscara utilizada por [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para calcular los permisos efectivos. Cada una de las 25 clases de elementos protegibles tiene su propio conjunto de permisos con sus valores numéricos correspondientes. **Sys. fn_translate_permissions** traduce esta máscara de máscara en una tabla de nombres de permisos.  
  
## <a name="permissions"></a>Permisos  
 Debe pertenecer al rol **public** .  
  
## <a name="example"></a>Ejemplo  
 En la siguiente consulta `sys.fn_builtin_permissions` se usa para mostrar los permisos que se aplican a los certificados y, a continuación, `sys.fn_translate_permissions` se usa para devolver los resultados de la máscara de vídeo de permisos.  
  
```  
SELECT * FROM sys.fn_builtin_permissions('CERTIFICATE');  
SELECT '0001' AS Input, * FROM sys.fn_translate_permissions('CERTIFICATE', 0001);  
SELECT '0010' AS Input, * FROM sys.fn_translate_permissions('CERTIFICATE', 0010);  
SELECT '0011' AS Input, * FROM sys.fn_translate_permissions('CERTIFICATE', 0011);  
```  
  
## <a name="see-also"></a>Consulte también  
 [Permisos &#40;Motor de base de datos&#41;](../../relational-databases/security/permissions-database-engine.md)   
 [Sys. server_permissions &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-server-permissions-transact-sql.md)   
 [sys.database_permissions &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-database-permissions-transact-sql.md)  
  
  
