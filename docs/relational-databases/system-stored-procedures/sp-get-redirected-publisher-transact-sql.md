---
title: sp_get_redirected_publisher (Transact-SQL) | Documentos de Microsoft
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
- sp_get_redirected_publisher_TSQL
- sp_get_redirected_publisher
ms.assetid: d47a9ab5-f2cc-42a8-8be9-a33895ce44f0
caps.latest.revision: 10
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 746f55b0230bf75ac835be901432d0e8eae278d0
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/16/2018
---
# <a name="spgetredirectedpublisher-transact-sql"></a>sp_get_redirected_publisher (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  Lo utilizan los agentes de replicación para consultar a un distribuidor a fin de determinar si se ha redirigido el publicador original.  
  
 ![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
sp_get_redirected_publisher   
    [ @original_publisher = ] 'original_publisher',  
    [ @publisher_db = ] 'database_name',   
    [ @bypass_publisher_validation = ] [0 | 1 ]  
```  
  
## <a name="arguments"></a>Argumentos  
 [ **@original_publisher** =] **'***original_publisher***'**  
 El nombre de la base de datos que se va a publicar. *publisher_db* es **sysname**, no tiene ningún valor predeterminado.  
  
 [ **@publisher_db** = ] **'***publisher_db***'**  
 El nombre de la base de datos que se va a publicar. *publisher_db* es **sysname**, no tiene ningún valor predeterminado.  
  
 [ **@bypass_publisher_validation** = ] [0 | 1 ]  
 Se utiliza para omitir la validación del publicador redirigido. Si es 0, se realiza la validación. Si es 1, no se realiza la validación. *bypass_publisher_validation* es **bits**, con un valor predeterminado es 0.  
  
## <a name="return-code-values"></a>Valores de código de retorno  
 **0** (correcto) o **1** (error)  
  
## <a name="result-sets"></a>Conjuntos de resultados  
  
|Nombre de columna|Tipo de datos|Description|  
|-----------------|---------------|-----------------|  
|**redirected_publisher**|**sysname**|El nombre del publicador después de la redirección.|  
|**error_number**|**int**|El número de error del error de validación.|  
|**error_severity**|**int**|La gravedad del error de validación.|  
|**error_message**|**nvarchar(4000)**|El texto del mensaje de error de validación.|  
  
## <a name="remarks"></a>Comentarios  
 *redirected_publisher* devuelve el nombre del publicador actual. Devuelve null si el publicador y la publicación de bases de datos no se ha redirigido mediante **sp_redirect_publisher**.  
  
 Si no se solicita la validación o si no existe ninguna entrada para el publicador y la base de datos de publicación, *error_number* y *error_severity* devuelven 0 y *error_message* Devuelve null.  
  
 Si se solicita la validación, la validación del procedimiento almacenado [sp_validate_redirected_publisher &#40;Transact-SQL&#41; ](../../relational-databases/system-stored-procedures/sp-validate-redirected-publisher-transact-sql.md) se llama para comprobar que el destino de la redirección es un host adecuado para la publicación base de datos. Si la validación es correcta, **sp_get_redirected_publisher** devuelve el nombre del publicador redirigido, 0 para el *error_number* y *error_severity* y null en columnas el *error_message* columna.  
  
 Si se solicita la validación y se produce un error, se devuelve el nombre del publicador redirigido junto con información sobre el error.  
  
## <a name="permissions"></a>Permissions  
 Autor de la llamada debe ser un miembro de la **sysadmin** rol fijo de servidor, el **db_owner** rol fijo de base de datos para la base de datos de distribución o un miembro de una lista de acceso de publicación para una publicación definida asociado a la base de datos del publicador.  
  
## <a name="see-also"></a>Vea también  
 [Procedimientos almacenados de replicación &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/replication-stored-procedures-transact-sql.md)   
 [sp_validate_redirected_publisher &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-validate-redirected-publisher-transact-sql.md)   
 [sp_redirect_publisher &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-redirect-publisher-transact-sql.md)   
 [sp_validate_replica_hosts_as_publishers &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-validate-replica-hosts-as-publishers-transact-sql.md)  
  
  
