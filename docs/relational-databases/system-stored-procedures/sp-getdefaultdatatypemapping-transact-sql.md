---
title: sp_getdefaultdatatypemapping (Transact-SQL) | Documentos de Microsoft
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
- sp_getdefaultdatatypemapping_TSQL
- sp_getdefaultdatatypemapping
helpviewer_keywords:
- sp_getdefaultdatatypemapping
ms.assetid: b8401de1-f135-41d0-ba79-ce8fe1f48c00
caps.latest.revision: 18
author: edmacauley
ms.author: edmaca
manager: craigg
ms.openlocfilehash: bcb469245fdfb60c7a8063b68d749aa194e5f87a
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 05/03/2018
---
# <a name="spgetdefaultdatatypemapping-transact-sql"></a>sp_getdefaultdatatypemapping (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Devuelve información sobre la asignación predeterminada para el tipo de datos especificado entre [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] y que no es[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] base de datos (DBMS) del sistema de administración. Este procedimiento almacenado se ejecuta en el distribuidor de cualquier base de datos.  
  
 ![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
sp_getdefaultdatatypemapping [ @source_dbms = ] 'source_dbms'   
    [ , [ @source_version = ] 'source_version' ]  
        , [ @source_type = ] 'source_type'    
    [ , [ @source_length = ] source_length ]  
    [ , [ @source_precision = ] source_precision ]  
    [ , [ @source_scale = ] source_scale ]  
    [ , [ @source_nullable = ] source_nullable ]  
        , [ @destination_dbms = ] 'destination_dbms'   
    [ , [ @destination_version = ] 'destination_version' ]  
    [ , [ @destination_type = ] 'destination_type' OUTPUT ]  
    [ , [ @destination_length = ] destination_length OUTPUT ]  
    [ , [ @destination_precision = ] destination_precision OUTPUT ]  
    [ , [ @destination_scale = ] destination_scale OUTPUT ]  
    [ , [ @destination_nullable = ] source_nullable OUTPUT ]  
    [ , [ @dataloss = ] dataloss OUTPUT ]  
```  
  
## <a name="arguments"></a>Argumentos  
 [ **@source_dbms**=] **'***source_dbms***'**  
 Es el nombre del DBMS desde el que se asignan los tipos de datos. *source_dbms* es **sysname**, y puede tener uno de los siguientes valores:  
  
|Value|Description|  
|-----------|-----------------|  
|**MSSQLSERVER**|El origen es una base de datos de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].|  
|**ORACLE**|El origen es una base de datos de Oracle.|  
  
 Es necesario especificar este parámetro.  
  
 [  **@source_version=** ] **'***source_version***'**  
 Es el número de versión del DBMS de origen. *source_version* es **varchar (10)**, su valor predeterminado es null.  
  
 [ **@source_type**=] **'***source_type***'**  
 Es el tipo de datos del DBMS de origen. *source_type* es **sysname**, no tiene ningún valor predeterminado.  
  
 [  **@source_length=** ] *source_length*  
 Longitud del tipo de datos en el sistema DBMS de origen. *source_length* es **bigint**, su valor predeterminado es null.  
  
 [  **@source_precision=** ] *source_precision*  
 Es la precisión del tipo de datos del sistema DBMS de origen. *source_precision* es **bigint**, su valor predeterminado es null.  
  
 [  **@source_scale=** ] *source_scale*  
 Es la escala del tipo de datos del sistema DBMS de origen. *source_scale* es **int**, su valor predeterminado es null.  
  
 [  **@source_nullable=** ] *source_nullable*  
 Indica si el tipo de datos del DBMS de origen admite un valor NULL. *source_nullable* es **bits**, con un valor predeterminado de **1**, lo que significa que se admiten valores NULL.  
  
 [ **@destination_dbms** =] **'***destination_dbms***'**  
 Es el nombre del DBMS de destino. *destination_dbms* es **sysname**, y puede tener uno de los siguientes valores:  
  
|Value|Description|  
|-----------|-----------------|  
|**MSSQLSERVER**|El destino es una base de datos de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].|  
|**ORACLE**|El destino es una base de datos de Oracle.|  
|**DB2**|El destino es una base de datos IBM DB2.|  
|**SYBASE**|El destino es una base de datos Sybase.|  
  
 Es necesario especificar este parámetro.  
  
 [ **@destination_version**=] **'***destination_version***'**  
 Es la versión de producto del sistema DBMS de destino. *destination_version* es **varchar (10)**, su valor predeterminado es null.  
  
 [ **@destination_type**=] **'***destination_type***'** salida  
 Es el tipo de datos que se enumera en el DBMS de destino. *destination_type* es **sysname**, su valor predeterminado es null.  
  
 [  **@destination_length=** ] *destination_length* salida  
 Es la longitud del tipo de datos en el sistema DBMS de destino. *destination_length* es **bigint**, su valor predeterminado es null.  
  
 [  **@destination_precision=** ] *destination_precision* salida  
 Es la precisión del tipo de datos en el sistema DBMS de destino. *destination_precision* es **bigint**, su valor predeterminado es null.  
  
 [  **@destination_scale=** ] *destination_scale *** salida**  
 Es la escala del tipo de datos en el sistema DBMS de destino. *destination_scale* es **int**, su valor predeterminado es null.  
  
 [  **@destination_nullable=** ] *destination_nullable *** salida**  
 Indica si el tipo de datos del DBMS de destino admite un valor NULL. *destination_nullable* es **bits**, su valor predeterminado es null. **1** significa que se admiten valores NULL.  
  
 [  **@dataloss=** ] *dataloss *** salida**  
 Indica si la asignación tiene el potencial de pérdida de datos. *DataLoss* es **bits**, su valor predeterminado es null. **1** significa que hay un posible pérdida de datos.  
  
## <a name="return-code-values"></a>Valores de código de retorno  
 **0** (correcto) o **1** (error)  
  
## <a name="remarks"></a>Comentarios  
 **sp_getdefaultdatatypemapping** se utiliza en todos los tipos de replicación entre [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] y que no es[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] DBMS.  
  
 **sp_getdefaultdatatypemapping** devuelve el tipo de los datos de destino predeterminado que es la coincidencia más cercana al tipo de datos de origen especificada.  
  
## <a name="permissions"></a>Permissions  
 Solo los miembros de la **sysadmin** rol fijo de servidor puede ejecutar **sp_getdefaultdatatypemapping**.  
  
## <a name="see-also"></a>Vea también  
 [sp_helpdatatypemap &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-helpdatatypemap-transact-sql.md)   
 [sp_setdefaultdatatypemapping &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-setdefaultdatatypemapping-transact-sql.md)   
 [Data Type Mapping for Oracle Publishers](../../relational-databases/replication/non-sql/data-type-mapping-for-oracle-publishers.md)   
 [IBM DB2 Subscribers](../../relational-databases/replication/non-sql/ibm-db2-subscribers.md)   
 [Suscriptores de Oracle](../../relational-databases/replication/non-sql/oracle-subscribers.md)  
  
  
