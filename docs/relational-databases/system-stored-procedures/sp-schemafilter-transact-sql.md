---
title: sp_schemafilter (Transact-SQL) | Documentos de Microsoft
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
- sp_schemafilter_TSQL
- sp_schemafilter
helpviewer_keywords:
- sp_schemafilter
ms.assetid: 199e869b-2cd2-44ee-b2ee-69edb06a1bc4
caps.latest.revision: 24
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: dfa3e7382988a83764302d686815a23781709389
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/16/2018
---
# <a name="spschemafilter-transact-sql"></a>sp_schemafilter (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Modifica y muestra la información del esquema que se excluye al incluir tablas de Oracle aptas para su publicación.  
  
 ![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
sp_schemafilter [ @publisher = ] 'publisher'   
   [ , [ @schema = ] 'schema' ]   
   [ , [ @operation = ] 'operation' ]   
```  
  
## <a name="arguments"></a>Argumentos  
 [**@publisher** =] **'***publisher***'**  
 Es el nombre de no es[!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Publisher. *Publisher* es **sysname**, no tiene ningún valor predeterminado.  
  
 [**@schema** =] **'***esquema***'**  
 Es el nombre del esquema. *esquema* es **sysname**, su valor predeterminado es null.  
  
 [**@operation** =] **'***operación***'**  
 Es la acción que se realiza en este esquema. *operación* es **nvarchar (4)**, y puede tener uno de los siguientes valores.  
  
|Value|Description|  
|-----------|-----------------|  
|**Agregar**|Agrega el esquema especificado a la lista de esquemas no aptos para su publicación.|  
|**quitar**|Quita el esquema especificado de la lista de esquemas no aptos para su publicación.|  
|**Ayuda**|Devuelve la lista de esquemas no aptos para su publicación.|  
  
## <a name="result-sets"></a>Conjuntos de resultados  
  
|Nombre de columna|Tipo de datos|Description|  
|-----------------|---------------|-----------------|  
|**SchemaName**|**sysname**|Es el nombre del esquema no apto para su publicación.|  
  
## <a name="return-code-values"></a>Valores de código de retorno  
 **0** (correcto) o **1** (error)  
  
## <a name="remarks"></a>Comentarios  
 **sp_schemafilter** solo debe usarse para los publicadores heterogéneos.  
  
## <a name="permissions"></a>Permissions  
 Solo los miembros de la **sysadmin** rol fijo de servidor en el distribuidor puede ejecutar **sp_schemafilter**.  
  
## <a name="see-also"></a>Vea también  
 [Procedimientos almacenados de replicación &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/replication-stored-procedures-transact-sql.md)  
  
  
