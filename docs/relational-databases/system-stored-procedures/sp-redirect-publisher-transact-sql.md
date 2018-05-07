---
title: sp_redirect_publisher (Transact-SQL) | Documentos de Microsoft
ms.custom: ''
ms.date: 03/15/2017
ms.prod: sql
ms.prod_service: database-engine
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
- sp_redirect_publisher_TSQL
- sp_redirect_publisher
helpviewer_keywords:
- sp_redirect_publisher
ms.assetid: af45e2b2-57fb-4bcd-a58b-e61401fb3b26
caps.latest.revision: 14
author: edmacauley
ms.author: edmaca
manager: craigg
ms.openlocfilehash: e8df59d709ef04d94626ac2ab6a3ba268d63ab76
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/03/2018
---
# <a name="spredirectpublisher-transact-sql"></a>sp_redirect_publisher (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  Especifica un publicador redirigido para un par de publicador y base de datos. Si la base de datos del publicador pertenece a un grupo de disponibilidad AlwaysOn, el publicador redirigido es el nombre de agente de escucha del grupo de disponibilidad asociado al grupo de disponibilidad.  
  
 ![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
sp_redirect_publisher   
    [ @original_publisher = ] 'original_publisher',  
    [ @publisher_db = ] 'database_name'   
    [ , [ @redirected_publisher = ] 'new_publisher' ]  
```  
  
## <a name="arguments"></a>Argumentos  
 [ **@original_publisher** =] **'***original_publisher***'**  
 El nombre de la instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] que publicó originalmente la base de datos. *original_publisher* es **sysname**, no tiene ningún valor predeterminado.  
  
 [ **@publisher_db** = ] **'***publisher_db***'**  
 El nombre de la base de datos que se va a publicar. *publisher_db* es **sysname**, no tiene ningún valor predeterminado.  
  
 [ **@redirected_publisher** =] **'***redirected_publisher***'**  
 El nombre del agente de escucha del grupo de disponibilidad asociado al grupo de disponibilidad que se convertirá en el nuevo publicador. *redirected_publisher* es **sysname**, no tiene ningún valor predeterminado. Cuando el agente de escucha de grupo de disponibilidad está configurado en un puerto que no es el predeterminado, especifique el número de puerto junto con el nombre del agente de escucha, como `'Listenername,51433'`  
  
## <a name="return-code-values"></a>Valores de código de retorno  
 **0** (correcto) o **1** (error)  
  
## <a name="result-sets"></a>Conjuntos de resultados  
 None  
  
## <a name="remarks"></a>Comentarios  
 **sp_redirect_publisher** se utiliza para permitir que un publicador de replicación se redirija a la réplica principal actual de un grupo de disponibilidad Always On asociando el par publicador/base de datos con el agente de escucha de un grupo de disponibilidad. Ejecutar **sp_redirect_publisher** después de que del agente de escucha se ha configurado para el grupo de disponibilidad que contiene la base de datos publicada.  
  
 Si la base de datos de publicación del publicador original se quita de un grupo de disponibilidad en la réplica principal, ejecute **sp_redirect_publisher** sin especificar un valor para el *@redirected_publisher* parámetro para quitar el redireccionamiento del par publicador/base de datos. Para obtener más información sobre cómo redirigir el publicador, vea [mantener una base de datos de publicación AlwaysOn &#40;SQL Server&#41;](../../database-engine/availability-groups/windows/maintaining-an-always-on-publication-database-sql-server.md).  
  
## <a name="permissions"></a>Permissions  
 Autor de la llamada debe ser un miembro de la **sysadmin** rol fijo de servidor, el **db_owner** rol fijo de base de datos para la base de datos de distribución o un miembro de una lista de acceso de publicación para una publicación definida asociado a la base de datos del publicador.  
  
## <a name="see-also"></a>Vea también  
 [Procedimientos almacenados de replicación &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/replication-stored-procedures-transact-sql.md)   
 [sp_validate_redirected_publisher &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-validate-redirected-publisher-transact-sql.md)   
 [sp_get_redirected_publisher &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-get-redirected-publisher-transact-sql.md)   
 [sp_validate_replica_hosts_as_publishers &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-validate-replica-hosts-as-publishers-transact-sql.md)  
  
  
