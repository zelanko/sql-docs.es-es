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
author: MashaMSFT
ms.author: mathoma
manager: craigg
monikerRange: '>= aps-pdw-2016 || = azure-sqldw-latest || = sqlallproducts-allversions'
ms.openlocfilehash: 9feb899a0a46a04ad52ef15fb801e2eb4866e478
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 10/01/2018
ms.locfileid: "47698573"
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
 Devuelve un valor **nvarchar(32)**.  
  
## <a name="general-remarks"></a>Notas generales  
 El identificador de sesión se asigna a cada conexión de usuario en el momento de realizarla. Este identificador persiste mientras dure la conexión. Cuando la conexión finalice, el identificador de sesión se libera.  
  
 Los identificadores de sesión comienzan por los caracteres alfabéticos "SID". Distinguen mayúsculas de minúsculas y se deben escribir en mayúsculas cuando se usan en comandos [!INCLUDE[DWsql](../../includes/dwsql-md.md)].  
  
 Puede consultar la vista [sys.dm_pdw_exec_sessions](../../relational-databases/system-dynamic-management-views/sys-dm-pdw-exec-sessions-transact-sql.md) para recuperar la misma información que esta función.  
  
## <a name="examples"></a>Ejemplos  
 En el siguiente ejemplo se devuelve el identificador de sesión actual.  
  
```  
SELECT SESSION_ID();  
```  
  
## <a name="see-also"></a>Ver también  
 [DB_NAME &#40;Transact-SQL&#41;](../../t-sql/functions/db-name-transact-sql.md)   
 [VERSION &#40;SQL Data Warehouse&#41;](../../t-sql/functions/version-transact-sql-configuration-functions.md)
  
  
