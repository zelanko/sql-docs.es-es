---
title: sp_validate_replica_hosts_as_publishers (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_validate_replica_hosts_as_publishers_TSQL
- sp_validate_replica_hosts_as_publishers
helpviewer_keywords:
- sp_validate_replica_hosts_as_publishers
ms.assetid: 45001fc9-2dbd-463c-af1d-aa8982d8c813
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 8df9c4fcc88f568c920f0a5959338f195d79d925
ms.sourcegitcommit: c426c7ef99ffaa9e91a93ef653cd6bf3bfd42132
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/10/2019
ms.locfileid: "72252110"
---
# <a name="sp_validate_replica_hosts_as_publishers-transact-sql"></a>sp_validate_replica_hosts_as_publishers (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  **sp_validate_replica_hosts_as_publishers** es una extensión de **sp_validate_redirected_publisher** que permite validar todas las réplicas secundarias, en lugar de simplemente la réplica principal actual. **sp_validate_replicat_hosts_as_publisher** valida una topología de replicación de Always on completa. **sp_validate_replica_hosts_as_publishers** se debe ejecutar directamente en el distribuidor mediante una sesión de escritorio remoto para evitar un error de seguridad de doble salto (21892).  
  
 ![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
sp_validate_replica_hosts_as_publishers   
    [ @original_publisher = ] 'original_publisher',  
    [ @publisher_db = ] 'database_name',   
    [ @redirected_publisher = ] 'new_publisher' output  
```  
  
## <a name="arguments"></a>Argumentos  
`[ @original_publisher = ] 'original_publisher'` el nombre de la instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] que publicó originalmente la base de datos. *original_publisher* es de **tipo sysname**y no tiene ningún valor predeterminado.  
  
`[ @publisher_db = ] 'publisher_db'` el nombre de la base de datos que se está publicando. *publisher_db* es de **tipo sysname**y no tiene ningún valor predeterminado.  
  
`[ @redirected_publisher = ] 'redirected_publisher'` el destino de la redirección cuando se llamó a **sp_redirect_publisher** para el par publicador original y base de datos publicada. *redirected_publisher* es de **tipo sysname**y no tiene ningún valor predeterminado.  
  
## <a name="return-code-values"></a>Valores de código de retorno  
 **0** (correcto) o **1** (error)  
  
## <a name="result-sets"></a>Conjuntos de resultados  
 Ninguno.  
  
## <a name="remarks"></a>Remarks  
 Si no existe ninguna entrada para el publicador y la base de datos de publicación, **sp_validate_redirected_publisher** devuelve null para el parámetro de salida *\@redirected_publisher*. En caso contrario, se devuelve el publicador redirigido asociado, independientemente de si el resultado es correcto o error.  
  
 Si la validación se realiza correctamente, **sp_validate_redirected_publisher** devuelve una indicación de éxito.  
  
 Si la validación no se realiza correctamente, se producen los errores correspondientes.  **sp_validate_redirected_publisher** realiza el mejor esfuerzo para generar todos los problemas y no solo el primero encontrado.  
  
> [!NOTE]  
>  **sp_validate_replica_hosts_as_publishers** producirá el error siguiente al validar los hosts de réplica secundaria que no permiten el acceso de lectura o requieren que se especifique la intención de lectura.  
>   
>  Mensaje 21899, Nivel 11, Estado 1, Procedimiento **sp_hadr_verify_subscribers_at_publisher**, Línea 109  
>   
>  Error '976' en la consulta en el publicador redirigido 'MyReplicaHostName' para determinar si hubiera entradas de sysserver para suscriptores del publicador original 'MyOriginalPublisher', mensaje de error 'Error 976, nivel 14, estado 1, mensaje: La base de datos de destino 'MyPublishedDB', participa en un grupo de disponibilidad y no se encuentra accesible en este momento para consultas. El movimiento de datos se ha suspendido o la réplica de disponibilidad no está habilitada para el acceso de lectura. Para permitir el acceso de solo lectura a esta y a otras bases de datos del grupo de disponibilidad, habilite el acceso de lectura en una o varias réplicas de disponibilidad secundarias del grupo.  Para obtener más información, consulte la instrucción **ALTER AVAILABILITY GROUP** en los Libros en pantalla de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
>   
>  Se encontraron uno o varios errores de validación del publicador para el host de réplica 'MyReplicaHostName'.  
  
## <a name="permissions"></a>Permisos  
 El autor de la llamada debe ser miembro del rol fijo de servidor **sysadmin** , el rol fijo de base de datos **db_owner** para la base de datos de distribución, o un miembro de una lista de acceso a la publicación para una publicación definida asociada a la base de datos del publicador.  
  
## <a name="see-also"></a>Vea también  
 [Procedimientos almacenados de replicación &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/replication-stored-procedures-transact-sql.md)   
 [sp_get_redirected_publisher &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-get-redirected-publisher-transact-sql.md)   
 [sp_redirect_publisher &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-redirect-publisher-transact-sql.md)   
 [sp_validate_redirected_publisher &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-validate-redirected-publisher-transact-sql.md)  
  
  
