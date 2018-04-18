---
title: sp_helpdatatypemap (Transact-SQL) | Documentos de Microsoft
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.service: ''
ms.component: system-stored-procedures
ms.reviewer: ''
ms.suite: sql
ms.technology:
- replication
ms.tgt_pltfrm: ''
ms.topic: language-reference
applies_to:
- SQL Server
f1_keywords:
- sp_helpdatatypemap
- sp_helpdatatypemap_TSQL
helpviewer_keywords:
- sp_helpdatatypemap
ms.assetid: 800c9c65-723e-4961-a63d-327987f129f0
caps.latest.revision: 31
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 7e594c9b1d13730df2ccc93bf04d0348a5d2175b
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/16/2018
---
# <a name="sphelpdatatypemap-transact-sql"></a>sp_helpdatatypemap (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Devuelve información sobre las asignaciones de tipos de datos definidos entre [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] y no-[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] base de datos (DBMS) de sistemas de administración. Este procedimiento almacenado se ejecuta en el distribuidor de cualquier base de datos.  
  
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
 [ **@source_dbms**=] **'***source_dbms***'**  
 Es el nombre del DBMS desde el que se asignan los tipos de datos. *source_dbms* es **sysname**, y puede tener uno de los siguientes valores.  
  
|Value|Description|  
|-----------|-----------------|  
|**MSSQLSERVER**|El origen es una base de datos de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].|  
|**ORACLE**|El origen es una base de datos de Oracle.|  
  
 [ **@source_version**=] **'***source_version***'**  
 Es la versión del producto del DBMS de origen. *source_version*es **varchar (10)**, y si no se especifica, los datos de asignaciones de tipos para todas las versiones de la fuente de DBMS se devuelven. Permite filtrar el conjunto de resultados por la versión de origen del DBMS.  
  
 [ **@source_type**=] **'***source_type***'**  
 Es el tipo de datos indicado en el DBMS de origen. *source_type* es **sysname**, y si no se especifica, se devuelven las asignaciones de todos los tipos de datos del DBMS de origen. Permite filtrar el conjunto de resultados por tipo de datos en el DBMS de origen.  
  
 [ **@destination_dbms** =] **'***destination_dbms***'**  
 Es el nombre del DBMS de destino. *destination_dbms* es **sysname**, y puede tener uno de los siguientes valores.  
  
|Value|Description|  
|-----------|-----------------|  
|**MSSQLSERVER**|El destino es una base de datos de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].|  
|**ORACLE**|El destino es una base de datos de Oracle.|  
|**DB2**|El destino es una base de datos IBM DB2.|  
|**SYBASE**|El destino es una base de datos Sybase.|  
  
 [ **@destination_version**=] **'***destination_version***'**  
 Es la versión de producto del sistema DBMS de destino. *destination_version*es **varchar (10)**, y si no se especifica, se devuelven las asignaciones de todas las versiones del DBMS de destino. Permite filtrar el conjunto de resultados por la versión de destino del DBMS.  
  
 [ **@destination_type**=] **'***destination_type***'**  
 Es el tipo de datos que se enumera en el DBMS de destino. *destination_type*es **sysname**, y si no se especifica, se devuelven las asignaciones de todos los tipos de datos del DBMS de destino. Permite filtrar el conjunto de resultados por tipo de datos en el DBMS de destino.  
  
 [ **@defaults_only**=] *defaults_only*  
 Indica si solo se devuelven las asignaciones de los tipos de datos predeterminados. *defaults_only* es **bits**, su valor predeterminado es **0**. **1** significa que solo los datos predeterminados asignaciones de tipo se devuelve. **0** significa que el valor predeterminado y los datos definidos por el usuario escriba asignaciones se devuelve.  
  
## <a name="result-sets"></a>Conjuntos de resultados  
  
|Nombre de columna|Description|  
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
 **sp_helpdatatypemap** define las asignaciones de tipos de datos tanto de no publicadores de SQL Server y de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] publicadores que no son[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] los suscriptores.  
  
 Cuando no se admite la combinación especificada de origen y destino DBMS, **sp_helpdatatypemap** devuelve un conjunto de resultados vacío.  
  
## <a name="permissions"></a>Permissions  
 Solo los miembros de la **sysadmin** rol fijo de servidor en el distribuidor o los miembros de la **db_owner** rol fijo de base de datos en la base de datos de distribución puede ejecutar **sp_helpdatatypemap**.  
  
## <a name="see-also"></a>Vea también  
 [sp_getdefaultdatatypemapping &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-getdefaultdatatypemapping-transact-sql.md)   
 [sp_setdefaultdatatypemapping &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-setdefaultdatatypemapping-transact-sql.md)  
  
  
