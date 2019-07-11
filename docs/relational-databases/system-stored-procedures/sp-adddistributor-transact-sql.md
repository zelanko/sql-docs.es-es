---
title: sp_adddistributor (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_adddistributor
- sp_adddistributor_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_adddistributor
ms.assetid: 35415502-68d0-40f6-993c-180e50004f1e
author: mashamsft
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 8cf36a02d81b8732d80beb7c97d025a74138cd43
ms.sourcegitcommit: aeb2273d779930e76b3e907ec03397eab0866494
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/10/2019
ms.locfileid: "67716725"
---
# <a name="spadddistributor-transact-sql"></a>sp_adddistributor (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Crea una entrada en el [sys.sysservers](../../relational-databases/system-compatibility-views/sys-sysservers-transact-sql.md) tabla (si no hay uno), marca la entrada del servidor como distribuidor y almacena la información de propiedad. Este procedimiento almacenado se ejecuta en el distribuidor de la base de datos maestra para registrar y marcar el servidor como un distribuidor. En el caso de un distribuidor remoto, se ejecuta también en el publicador desde la base de datos maestra para registrar el distribuidor remoto.  
  
 ![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
sp_adddistributor [ @distributor= ] 'distributor'   
    [ , [ @heartbeat_interval= ] heartbeat_interval ]   
    [ , [ @password= ] 'password' ]   
    [ , [ @from_scripting= ] from_scripting ]  
```  
  
## <a name="arguments"></a>Argumentos  
`[ @distributor = ] 'distributor'` Es el nombre del servidor de distribución. *distribuidor* es **sysname**, no tiene ningún valor predeterminado. Este parámetro se utiliza únicamente si se está configurando un distribuidor remoto. Agrega entradas para las propiedades del distribuidor en el **msdb.. MSdistributor** tabla.  
  
`[ @heartbeat_interval = ] heartbeat_interval` Es el número máximo de minutos que un agente puede ejecutarse sin registrar un mensaje de progreso. *heartbeat_interval* es **int**, su valor predeterminado es de 10 minutos. Se crea un trabajo del Agente SQL Server que se ejecuta en este intervalo para comprobar el estado de los agentes de replicación que se están ejecutando.  
  
`[ @password = ] 'password']` Es la contraseña de la **distributor_admin** inicio de sesión. *contraseña* es **sysname**, su valor predeterminado es null. Si es NULL o una cadena vacía, la contraseña se restablece a un valor aleatorio. La contraseña debe configurarse cuando se agrega el primer distribuidor remoto. **distributor_admin** inicio de sesión y *contraseña* se almacenan para las entradas de servidor vinculado utilizadas para una *distribuidor* conexión RPC, incluidas las conexiones locales. Si *distribuidor* es local, la contraseña de **distributor_admin** se establece en un nuevo valor. Para los publicadores con un distribuidor remoto, el mismo valor para *contraseña* debe especificarse cuando se ejecuta **sp_adddistributor** en el publicador y el distribuidor. [sp_changedistributor_password](../../relational-databases/system-stored-procedures/sp-changedistributor-password-transact-sql.md) puede usarse para cambiar la contraseña del distribuidor.  
  
> [!IMPORTANT]  
>  Cuando sea posible, pida a los usuarios que proporcionen credenciales de seguridad en tiempo de ejecución. Si debe almacenar las credenciales en un archivo de script, proteja el archivo para evitar el acceso no autorizado.  
  
`[ @from_scripting = ] from_scripting` [!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]  
  
## <a name="return-code-values"></a>Valores de código de retorno  
 0 (correcto) o 1 (error)  
  
## <a name="remarks"></a>Comentarios  
 **sp_adddistributor** se utiliza en la replicación de instantáneas, transaccional y de mezcla.  
  
## <a name="example"></a>Ejemplo  
 [!code-sql[HowTo#AddDistPub](../../relational-databases/replication/codesnippet/tsql/sp-adddistributor-transa_1.sql)]  
  
## <a name="permissions"></a>Permisos  
 Solo los miembros de la **sysadmin** rol fijo de servidor puede ejecutar **sp_adddistributor**.  
  
## <a name="see-also"></a>Vea también  
 [Configurar la publicación y la distribución](../../relational-databases/replication/configure-publishing-and-distribution.md)   
 [sp_changedistributor_property &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-changedistributor-property-transact-sql.md)   
 [sp_dropdistributor &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-dropdistributor-transact-sql.md)   
 [sp_helpdistributor &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-helpdistributor-transact-sql.md)   
 [Procedimientos almacenados del sistema &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)   
 [Configurar distribución](../../relational-databases/replication/configure-distribution.md)  
  
  
