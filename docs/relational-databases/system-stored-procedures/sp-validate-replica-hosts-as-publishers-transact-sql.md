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
manager: craigg
ms.openlocfilehash: cdbfcad1bb03e88d335c8acddc1ff7eb8c75b2eb
ms.sourcegitcommit: ceb7e1b9e29e02bb0c6ca400a36e0fa9cf010fca
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 12/03/2018
ms.locfileid: "52791587"
---
# <a name="spvalidatereplicahostsaspublishers-transact-sql"></a>sp_validate_replica_hosts_as_publishers (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  **sp_validate_replica_hosts_as_publishers** es una extensión de **sp_validate_redirected_publisher** que permite que todas las réplicas secundarias que se valida, en lugar de simplemente la réplica principal actual. **sp_validate_replicat_hosts_as_publisher** valida una topología de replicación completa de Always On. **sp_validate_replica_hosts_as_publishers** debe ejecutarse directamente en el distribuidor mediante el uso de una sesión de escritorio remoto para evitar un error de seguridad de dos saltos (21892).  
  
 ![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
sp_validate_replica_hosts_as_publishers   
    [ @original_publisher = ] 'original_publisher',  
    [ @publisher_db = ] 'database_name',   
    [ @redirected_publisher = ] 'new_publisher' output  
```  
  
## <a name="arguments"></a>Argumentos  
 [ **@original_publisher** =] **'***original_publisher***'**  
 El nombre de la instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] que publicó originalmente la base de datos. *original_publisher* es **sysname**, no tiene ningún valor predeterminado.  
  
 [ **@publisher_db** = ] **'***publisher_db***'**  
 El nombre de la base de datos que se va a publicar. *publisher_db* es **sysname**, no tiene ningún valor predeterminado.  
  
 [ **@redirected_publisher** =] **'***redirected_publisher***'**  
 El destino de la redirección cuando **sp_redirect_publisher** llamó para el publicador y publicado original par de base de datos. *redirected_publisher* es **sysname**, no tiene ningún valor predeterminado.  
  
## <a name="return-code-values"></a>Valores de código de retorno  
 **0** (correcto) o **1** (error)  
  
## <a name="result-sets"></a>Conjuntos de resultados  
 Ninguno.  
  
## <a name="remarks"></a>Comentarios  
 Si no existe ninguna entrada para el publicador y la base de datos de publicación, **sp_validate_redirected_publisher** devuelve null para el parámetro de salida *@redirected_publisher*. En caso contrario, se devuelve el publicador redirigido asociado, independientemente de si el resultado es correcto o error.  
  
 Si la validación es correcta, **sp_validate_redirected_publisher** devuelve una indicación de éxito.  
  
 Si la validación no se realiza correctamente, se producen los errores correspondientes.  **sp_validate_redirected_publisher** facilita un mayor esfuerzo para generar todos los problemas y no solo el primero encontrado.  
  
> [!NOTE]  
>  **sp_validate_replica_hosts_as_publishers** producirá el error siguiente al validar los hosts de réplica secundaria que no permiten el acceso de lectura o requieren que se especifique la intención de lectura.  
>   
>  Mensaje 21899, Nivel 11, Estado 1, Procedimiento **sp_hadr_verify_subscribers_at_publisher**, Línea 109  
>   
>  Error en la consulta en el publicador redirigido 'MyReplicaHostName' para determinar si hay entradas de sysserver para los suscriptores del publicador original 'MyOriginalPublisher' Error '976', mensaje de error ' Error 976, nivel 14, estado 1, mensaje: La base de datos de destino 'MyPublishedDB', participa en un grupo de disponibilidad y actualmente no es accesible para las consultas. El movimiento de datos se ha suspendido o la réplica de disponibilidad no está habilitada para el acceso de lectura. Para permitir el acceso de solo lectura a esta y a otras bases de datos del grupo de disponibilidad, habilite el acceso de lectura en una o varias réplicas de disponibilidad secundarias del grupo.  Para obtener más información, consulte la instrucción **ALTER AVAILABILITY GROUP** en los Libros en pantalla de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
>   
>  Se encontraron uno o varios errores de validación del publicador para el host de réplica 'MyReplicaHostName'.  
  
## <a name="permissions"></a>Permisos  
 Autor de la llamada debe ser un miembro de la **sysadmin** rol fijo de servidor, el **db_owner** rol fijo de base de datos para la base de datos de distribución o un miembro de una lista de acceso de publicación para una publicación definida asociado a la base de datos del publicador.  
  
## <a name="see-also"></a>Vea también  
 [Procedimientos almacenados de replicación &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/replication-stored-procedures-transact-sql.md)   
 [sp_get_redirected_publisher &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-get-redirected-publisher-transact-sql.md)   
 [sp_redirect_publisher &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-redirect-publisher-transact-sql.md)   
 [sp_validate_redirected_publisher &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-validate-redirected-publisher-transact-sql.md)  
  
  
