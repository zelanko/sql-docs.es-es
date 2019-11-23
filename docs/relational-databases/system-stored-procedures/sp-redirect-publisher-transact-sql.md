---
title: sp_redirect_publisher (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/15/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_redirect_publisher_TSQL
- sp_redirect_publisher
helpviewer_keywords:
- sp_redirect_publisher
ms.assetid: af45e2b2-57fb-4bcd-a58b-e61401fb3b26
author: stevestein
ms.author: sstein
ms.openlocfilehash: 6062522ca6c5c3a311ba2f2c796f791c47e874ab
ms.sourcegitcommit: c426c7ef99ffaa9e91a93ef653cd6bf3bfd42132
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/10/2019
ms.locfileid: "72252118"
---
# <a name="sp_redirect_publisher-transact-sql"></a>sp_redirect_publisher (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  Especifica un publicador redirigido para un par de publicador y base de datos. Si la base de datos del publicador pertenece a un grupo de disponibilidad de Always On, el publicador Redirigido es el nombre del agente de escucha del grupo de disponibilidad asociado al grupo de disponibilidad.  
  
 ![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
sp_redirect_publisher   
    [ @original_publisher = ] 'original_publisher',  
    [ @publisher_db = ] 'database_name'   
    [ , [ @redirected_publisher = ] 'new_publisher' ]  
```  
  
## <a name="arguments"></a>Argumentos  
`[ @original_publisher = ] 'original_publisher'` el nombre de la instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] que publicó originalmente la base de datos. *original_publisher* es de **tipo sysname**y no tiene ningún valor predeterminado.  
  
`[ @publisher_db = ] 'publisher_db'` el nombre de la base de datos que se está publicando. *publisher_db* es de **tipo sysname**y no tiene ningún valor predeterminado.  
  
`[ @redirected_publisher = ] 'redirected_publisher'` el nombre del agente de escucha del grupo de disponibilidad asociado al grupo de disponibilidad que será el nuevo publicador. *redirected_publisher* es de **tipo sysname**y no tiene ningún valor predeterminado. Cuando el agente de escucha de grupo de disponibilidad está configurado en un puerto que no es el predeterminado, especifique el número de puerto junto con el nombre del agente de escucha, como `'Listenername,51433'`  
  
## <a name="return-code-values"></a>Valores de código de retorno  
 **0** (correcto) o **1** (error)  
  
## <a name="result-sets"></a>Conjuntos de resultados  
 Ninguno  
  
## <a name="remarks"></a>Remarks  
 **sp_redirect_publisher** se usa para permitir que un publicador de replicación se redirija a la réplica principal actual de un grupo de disponibilidad de Always on mediante la Asociación del par de publicador y base de datos con el agente de escucha de un grupo de disponibilidad. Ejecute **sp_redirect_publisher** después de configurar el agente de escucha del AG para el grupo de disponibilidad que contiene la base de datos publicada.  
  
 Si la base de datos de publicación del publicador original se quita de un grupo de disponibilidad en la réplica principal, ejecute **sp_redirect_publisher** sin especificar un valor para el parámetro *\@redirected_publisher* para quitar el redireccionamiento del par de publicador y base de datos. Para obtener más información sobre cómo redirigir el publicador cuando, vea [mantener una base de &#40;datos&#41;de publicación AlwaysOn SQL Server](../../database-engine/availability-groups/windows/maintaining-an-always-on-publication-database-sql-server.md).  
  
## <a name="permissions"></a>Permisos  
 El autor de la llamada debe ser miembro del rol fijo de servidor **sysadmin** , el rol fijo de base de datos **db_owner** para la base de datos de distribución, o un miembro de una lista de acceso a la publicación para una publicación definida asociada a la base de datos del publicador.  
  
## <a name="see-also"></a>Vea también  
 [Procedimientos almacenados de replicación &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/replication-stored-procedures-transact-sql.md)   
 [sp_validate_redirected_publisher &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-validate-redirected-publisher-transact-sql.md)   
 [sp_get_redirected_publisher &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-get-redirected-publisher-transact-sql.md)   
 [sp_validate_replica_hosts_as_publishers &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-validate-replica-hosts-as-publishers-transact-sql.md)  
  
  
