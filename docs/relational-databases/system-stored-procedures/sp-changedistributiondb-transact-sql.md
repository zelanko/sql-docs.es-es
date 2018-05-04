---
title: sp_changedistributiondb (Transact-SQL) | Documentos de Microsoft
ms.custom: ''
ms.date: 03/03/2017
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
- sp_changedistributiondb_TSQL
- sp_changedistributiondb
helpviewer_keywords:
- sp_changedistributiondb
ms.assetid: 66f73185-ea9e-43f9-86ed-9dd933cee2f6
caps.latest.revision: 28
author: edmacauley
ms.author: edmaca
manager: craigg
ms.openlocfilehash: 4db7eed568a00ecb2bd20fd874fd94fd187a1453
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 05/03/2018
---
# <a name="spchangedistributiondb-transact-sql"></a>sp_changedistributiondb (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Cambia las propiedades de la base de datos de distribución. Este procedimiento almacenado se ejecuta en el distribuidor de cualquier base de datos.  
  
 ![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
sp_changedistributiondb [ @database= ] 'database'   
    [ , [ @property= ] 'property' ]   
    [ , [ @value= ] 'value' ]  
```  
  
## <a name="arguments"></a>Argumentos  
 [  **@database=**] **'***base de datos***'**  
 Es el nombre de la base de datos de distribución. *base de datos* es **sysname**, no tiene ningún valor predeterminado.  
  
 [  **@property=**] **'***propiedad***'**  
 Es la propiedad que se va a cambiar para la base de datos especificada. *propiedad* es **sysname**, y puede tener uno de estos valores.  
  
|Value|Description|  
|-----------|-----------------|  
|**history_retention**|Período de retención de la tabla de historial.|  
|**max_distretention**|Período máximo de retención de la distribución.|  
|**min_distretention**|Período mínimo de retención de la distribución.|  
|NULL (predeterminado)|Disposición *propiedad* se imprimen los valores.|  
  
 [  **@value=**] **'***valor***'**  
 Es el nuevo valor para la propiedad especificada. *valor* es **nvarchar (255)**, su valor predeterminado es null.  
  
## <a name="return-code-values"></a>Valores de código de retorno  
 **0** (correcto) o **1** (error)  
  
## <a name="remarks"></a>Comentarios  
 **sp_changedistributiondb** se utiliza en todos los tipos de replicación.  
  
## <a name="example"></a>Ejemplo  
 [!code-sql[HowTo#sp_changedistributiondb](../../relational-databases/replication/codesnippet/tsql/sp-changedistributiondb-_1.sql)]  
  
## <a name="permissions"></a>Permissions  
 Solo los miembros de la **sysadmin** rol fijo de servidor puede ejecutar **sp_changedistributiondb**.  
  
## <a name="see-also"></a>Vea también  
 [Ver y modificar las propiedades del distribuidor y del publicador](../../relational-databases/replication/view-and-modify-distributor-and-publisher-properties.md)   
 [sp_adddistributiondb &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-adddistributiondb-transact-sql.md)   
 [sp_dropdistributiondb &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-dropdistributiondb-transact-sql.md)   
 [sp_helpdistributiondb &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-helpdistributiondb-transact-sql.md)   
 [Procedimientos almacenados de replicación &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/replication-stored-procedures-transact-sql.md)  
  
  
