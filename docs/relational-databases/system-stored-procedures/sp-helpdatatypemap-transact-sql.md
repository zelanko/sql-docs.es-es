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
ms.openlocfilehash: 0b9666c13a2e4d8183d19fade64bf49b13377b9a
ms.sourcegitcommit: 728a4fa5a3022c237b68b31724fce441c4e4d0ab
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/03/2019
ms.locfileid: "68771061"
---
# <a name="sphelpdatatypemap-transact-sql"></a>sp_helpdatatypemap (Transact-SQL)
[!INCLUDE[appliesto-ss-asdbmi-xxxx-xxx-md](../../includes/appliesto-ss-asdbmi-xxxx-xxx-md.md)]

  Devuelve información sobre las asignaciones de tipos de datos definidos [!INCLUDE[msCoName](../../includes/msconame-md.md)] entre [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] y los [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] sistemas de administración de bases de datos (DBMS) que no son de. Este procedimiento almacenado se ejecuta en el distribuidor de cualquier base de datos.  
  
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
`[ @source_dbms = ] 'source_dbms'`Es el nombre del DBMS desde el que se asignan los tipos de datos. *source_dbms* es de **tipo sysname**y puede tener uno de los valores siguientes.  
  
|Valor|Descripción|  
|-----------|-----------------|  
|**MSSQLSERVER**|El origen es una base de datos de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].|  
|**ORACLE**|El origen es una base de datos de Oracle.|  
  
`[ @source_version = ] 'source_version'`Es la versión del producto del DBMS de origen. *source_version*es de tipo **VARCHAR (10)** y, si no se especifica, se devuelven las asignaciones de tipos de datos para todas las versiones del DBMS de origen. Permite filtrar el conjunto de resultados por la versión de origen del DBMS.  
  
`[ @source_type = ] 'source_type'`Es el tipo de datos que aparece en el DBMS de origen. *source_type* es de **tipo sysname**y, si no se especifica, se devuelven las asignaciones de todos los tipos de datos del DBMS de origen. Permite filtrar el conjunto de resultados por tipo de datos en el DBMS de origen.  
  
`[ @destination_dbms = ] 'destination_dbms'`Es el nombre del DBMS de destino. *destination_dbms* es de **tipo sysname**y puede tener uno de los valores siguientes.  
  
|Valor|Descripción|  
|-----------|-----------------|  
|**MSSQLSERVER**|El destino es una base de datos de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].|  
|**ORACLE**|El destino es una base de datos de Oracle.|  
|**DB2**|El destino es una base de datos IBM DB2.|  
|**SYBASE**|El destino es una base de datos Sybase.|  
  
`[ @destination_version = ] 'destination_version'`Es la versión del producto del DBMS de destino. *destination_version*es de tipo **VARCHAR (10)** y, si no se especifica, se devuelven las asignaciones de todas las versiones del DBMS de destino. Permite filtrar el conjunto de resultados por la versión de destino del DBMS.  
  
`[ @destination_type = ] 'destination_type'`Es el tipo de datos que aparece en el DBMS de destino. *destination_type*es de **tipo sysname**y, si no se especifica, se devuelven las asignaciones de todos los tipos de datos del DBMS de destino. Permite filtrar el conjunto de resultados por tipo de datos en el DBMS de destino.  
  
`[ @defaults_only = ] defaults_only`Es si solo se devuelven las asignaciones de tipos de datos predeterminados. *defaults_only* es de **bit**y su valor predeterminado es **0**. **1** significa que solo se devuelven las asignaciones de tipos de datos predeterminados. **0** significa que se devuelven las asignaciones predeterminadas y de tipos de datos definidos por el usuario.  
  
## <a name="result-sets"></a>Conjuntos de resultados  
  
|Nombre de columna|Descripción|  
|-----------------|-----------------|  
|**mapping_id**|Identifica una asignación de tipos de datos.|  
|**source_dbms**|El nombre y el número de versión del DBMS de origen.|  
|**source_type**|Es el tipo de datos del DBMS de origen.|  
|**destination_dbms**|Es el nombre del DBMS de destino.|  
|**destination_type**|Es el tipo de datos del DBMS de destino.|  
|**is_default**|Indica si se trata de una asignación predeterminada o alternativa. Un valor de **0** indica que esta asignación está definida por el usuario.|  
  
## <a name="return-code-values"></a>Valores de código de retorno  
 **0** (correcto) o **1** (error)  
  
## <a name="remarks"></a>Comentarios  
 **sp_helpdatatypemap** define las asignaciones de tipos de datos tanto de los publicadores que [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] no son de SQL Server [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] como de los publicadores que no son de.  
  
 Cuando no se admite la combinación especificada de DBMS de origen y de destino, **sp_helpdatatypemap** devuelve un conjunto de resultados vacío.  
  
## <a name="permissions"></a>Permisos  
 Solo los miembros del rol fijo de servidor **sysadmin** en el distribuidor o los miembros del rol fijo de base de datos **db_owner** en la base de datos de distribución pueden ejecutar **sp_helpdatatypemap**.  
  
## <a name="see-also"></a>Vea también  
 [sp_getdefaultdatatypemapping &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-getdefaultdatatypemapping-transact-sql.md)   
 [sp_setdefaultdatatypemapping &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-setdefaultdatatypemapping-transact-sql.md)  
  
  
