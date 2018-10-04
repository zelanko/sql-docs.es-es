---
title: Sys.fn_translate_permissions (Transact-SQL) | Microsoft Docs
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
manager: craigg
ms.openlocfilehash: b098dafc5764db96bdf3dc9e604f3e69a687ab94
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/01/2018
ms.locfileid: "47700503"
---
# <a name="sysfntranslatepermissions-transact-sql"></a>sys.fn_translate_permissions (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Traduce la máscara de bits de permisos devuelta por Seguimiento de SQL a una tabla de nombres de permisos.  
  
 ![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
sys.fn_translate_permissions ( level , perms )  
```  
  
## <a name="arguments"></a>Argumentos  
 *Nivel*  
 El tipo de elemento protegible al que se aplica el permiso. *nivel* es **nvarchar (60)**.  
  
 *Perms*  
 Es una máscara de bits que se devuelve en la columna de permisos. *Perms* es **varbinary (16)**.  
  
## <a name="returns"></a>Devuelve  
 **table**  
  
## <a name="remarks"></a>Comentarios  
 El valor devuelto en el **permisos** columna de un seguimiento de SQL es una representación de entero de una máscara de bits utilizada por [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para calcular los permisos efectivos. Cada una de las 25 clases de elementos protegibles tiene su propio conjunto de permisos con sus valores numéricos correspondientes. **Sys.fn_translate_permissions** traduce esta máscara de bits en una tabla de nombres de permisos.  
  
## <a name="permissions"></a>Permisos  
 Debe pertenecer al rol **public** .  
  
## <a name="example"></a>Ejemplo  
 La consulta siguiente utiliza `sys.fn_builtin_permissions` para mostrar los permisos que se aplican a los certificados y, a continuación, usa `sys.fn_translate_permissions` para devolver los resultados de la máscara de bits de permisos.  
  
```  
SELECT * FROM sys.fn_builtin_permissions('CERTIFICATE');  
SELECT '0001' AS Input, * FROM sys.fn_translate_permissions('CERTIFICATE', 0001);  
SELECT '0010' AS Input, * FROM sys.fn_translate_permissions('CERTIFICATE', 0010);  
SELECT '0011' AS Input, * FROM sys.fn_translate_permissions('CERTIFICATE', 0011);  
```  
  
## <a name="see-also"></a>Vea también  
 [Permisos &#40;motor de base de datos&#41;](../../relational-databases/security/permissions-database-engine.md)   
 [sys.server_permissions &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-server-permissions-transact-sql.md)   
 [sys.database_permissions &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-database-permissions-transact-sql.md)  
  
  
