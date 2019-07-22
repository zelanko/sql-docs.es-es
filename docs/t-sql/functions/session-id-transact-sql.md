---
title: SESSION_ID (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 02/23/2018
ms.prod: sql
ms.prod_service: sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
dev_langs:
- TSQL
author: VanMSFT
ms.author: vanto
monikerRange: '>= aps-pdw-2016 || = azure-sqldw-latest || = sqlallproducts-allversions'
ms.openlocfilehash: 3b63cbd1498021fdf9ed8418c3ff36ddec9143f0
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 07/15/2019
ms.locfileid: "68022233"
---
# <a name="sessionid-transact-sql"></a>SESSION_ID (Transact-SQL)
[!INCLUDE[tsql-appliesto-xxxxxx-xxxx-asdw-pdw-md](../../includes/tsql-appliesto-xxxxxx-xxxx-asdw-pdw-md.md)]

  Devuelve el identificador de la sesión de [!INCLUDE[ssSDW](../../includes/sssdw-md.md)] o [!INCLUDE[ssPDW_md](../../includes/sspdw-md.md)] actual.  
  
 ![Icono de vínculo a temas](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Convenciones de sintaxis de Transact-SQL &#40;Transact-SQL&#41;](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxis  
  
```  
-- Azure SQL Data Warehouse and Parallel Data Warehouse  
SESSION_ID ( )  
```  
  
## <a name="return-value"></a>Valor devuelto  
 Devuelve un valor **nvarchar(32)** .  
  
## <a name="general-remarks"></a>Notas generales  
 El identificador de sesión se asigna a cada conexión de usuario en el momento de realizarla. Este identificador persiste mientras dure la conexión. Cuando la conexión finalice, el identificador de sesión se libera.  
  
 Los identificadores de sesión comienzan por los caracteres alfabéticos "SID". Distinguen mayúsculas de minúsculas y se deben escribir en mayúsculas cuando se usan en comandos [!INCLUDE[DWsql](../../includes/dwsql-md.md)].  
  
 Puede consultar la vista [sys.dm_pdw_exec_sessions](../../relational-databases/system-dynamic-management-views/sys-dm-pdw-exec-sessions-transact-sql.md) para recuperar la misma información que esta función.  
  
## <a name="examples"></a>Ejemplos  
 En el siguiente ejemplo se devuelve el identificador de sesión actual.  
  
```  
SELECT SESSION_ID();  
```  
  
## <a name="see-also"></a>Consulte también  
 [DB_NAME &#40;Transact-SQL&#41;](../../t-sql/functions/db-name-transact-sql.md)   
 [VERSION &#40;SQL Data Warehouse&#41;](../../t-sql/functions/version-transact-sql-configuration-functions.md)
  
  
