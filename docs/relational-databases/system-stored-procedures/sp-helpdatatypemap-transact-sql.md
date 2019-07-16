---
title: sp_helpdatatypemap (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_helpdatatypemap
- sp_helpdatatypemap_TSQL
helpviewer_keywords:
- sp_helpdatatypemap
ms.assetid: 800c9c65-723e-4961-a63d-327987f129f0
author: stevestein
ms.author: sstein
ms.openlocfilehash: ee304c9847019b21f1e08f57a3e0fdf0b439d241
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/15/2019
ms.locfileid: "68101402"
---
# <a name="sphelpdatatypemap-transact-sql"></a>sp_helpdatatypemap (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Devuelve información sobre las asignaciones de tipos de datos definido entre [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] y no- [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] base de datos (DBMS) de los sistemas de administración. Este procedimiento almacenado se ejecuta en el distribuidor de cualquier base de datos.  
  
 ![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
sp_helpdatatypemap [ @source_dbms = ] 'source_dbms'   
    [ , [ @source_version = ] 'source_version' ]  
    [ , [ @source_type = ] 'source_type' ]   
    [ , [ @destination_dbms = ] 'destination_dbms' ]  
    [ , [ @destination_version = ] 'destination_version' ]  
    [ , [ @destination_type = ] 'destination_type' ]  
    [ , [ @defaults_only = ] defaults_only ]  
```  
  
## <a name="arguments"></a>Argumentos  
`[ @source_dbms = ] 'source_dbms'` Es el nombre del DBMS desde el que se asignan los tipos de datos. *source_dbms* es **sysname**, y puede tener uno de los siguientes valores.  
  
|Valor|Descripción|  
|-----------|-----------------|  
|**MSSQLSERVER**|El origen es una base de datos de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].|  
|**ORACLE**|El origen es una base de datos de Oracle.|  
  
`[ @source_version = ] 'source_version'` Es la versión del producto del DBMS de origen. *source_version*es **varchar (10)** , y si no se especifica, los datos de asignaciones de tipos para todas las versiones de la fuente de DBMS se devuelven. Permite filtrar el conjunto de resultados por la versión de origen del DBMS.  
  
`[ @source_type = ] 'source_type'` El tipo de datos aparece en el DBMS de origen. *source_type* es **sysname**, y si no se especifica, se devuelven las asignaciones para todos los tipos de datos del DBMS de origen. Permite filtrar el conjunto de resultados por tipo de datos en el DBMS de origen.  
  
`[ @destination_dbms = ] 'destination_dbms'` Es el nombre del DBMS de destino. *destination_dbms* es **sysname**, y puede tener uno de los siguientes valores.  
  
|Valor|Descripción|  
|-----------|-----------------|  
|**MSSQLSERVER**|El destino es una base de datos de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].|  
|**ORACLE**|El destino es una base de datos de Oracle.|  
|**DB2**|El destino es una base de datos IBM DB2.|  
|**SYBASE**|El destino es una base de datos Sybase.|  
  
`[ @destination_version = ] 'destination_version'` Es la versión del producto del DBMS de destino. *destination_version*es **varchar (10)** , y si no se especifica, se devuelven las asignaciones para todas las versiones del DBMS de destino. Permite filtrar el conjunto de resultados por la versión de destino del DBMS.  
  
`[ @destination_type = ] 'destination_type'` El tipo de datos aparece en el DBMS de destino. *destination_type*es **sysname**, y si no se especifica, se devuelven las asignaciones para todos los tipos de datos del DBMS de destino. Permite filtrar el conjunto de resultados por tipo de datos en el DBMS de destino.  
  
`[ @defaults_only = ] defaults_only` Indica si solo se devuelven las asignaciones de tipos de datos de forma predeterminada. *defaults_only* es **bit**, su valor predeterminado es **0**. **1** significa que solo los datos predeterminados asignaciones de tipos se devuelve. **0** significa que el valor predeterminado y cualquier dato definido por el usuario escriba las asignaciones se devuelve.  
  
## <a name="result-sets"></a>Conjuntos de resultados  
  
|Nombre de columna|Descripción|  
|-----------------|-----------------|  
|**mapping_id**|Identifica una asignación de tipos de datos.|  
|**source_dbms**|El nombre y el número de versión del DBMS de origen.|  
|**source_type**|Es el tipo de datos del DBMS de origen.|  
|**destination_dbms**|Es el nombre del DBMS de destino.|  
|**destination_type**|Es el tipo de datos del DBMS de destino.|  
|**is_default**|Indica si se trata de una asignación predeterminada o alternativa. Un valor de **0** indica que esta asignación es definido por el usuario.|  
  
## <a name="return-code-values"></a>Valores de código de retorno  
 **0** (correcto) o **1** (error)  
  
## <a name="remarks"></a>Comentarios  
 **sp_helpdatatypemap** define asignaciones de tipos de datos tanto de que no son publicadores de SQL Server y desde [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] los publicadores que no sean de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] los suscriptores.  
  
 Cuando no se admite la combinación especificada de origen y el DBMS de destino, **sp_helpdatatypemap** devuelve un conjunto de resultados vacío.  
  
## <a name="permissions"></a>Permisos  
 Solo los miembros de la **sysadmin** rol fijo de servidor en el distribuidor o los miembros de la **db_owner** rol fijo de base de datos en la base de datos de distribución puede ejecutar **sp_helpdatatypemap**.  
  
## <a name="see-also"></a>Vea también  
 [sp_getdefaultdatatypemapping &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-getdefaultdatatypemapping-transact-sql.md)   
 [sp_setdefaultdatatypemapping &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-setdefaultdatatypemapping-transact-sql.md)  
  
  
