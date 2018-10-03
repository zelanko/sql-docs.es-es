---
title: sp_replcmds (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology:
- replication
ms.topic: language-reference
f1_keywords:
- sp_replcmds_TSQL
- sp_replcmds
helpviewer_keywords:
- sp_replcmds
ms.assetid: 7e932f80-cc6e-4109-8db4-2b7c8828df73
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 00fec83a709b1c3bfba352663784b5018134769d
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/01/2018
ms.locfileid: "47783500"
---
# <a name="spreplcmds-transact-sql"></a>sp_replcmds (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Devuelve los comandos de las transacciones marcadas para replicación. Este procedimiento almacenado se ejecuta en el publicador de la base de datos de publicación.  
  
> [!IMPORTANT]  
>  El **sp_replcmds** procedimiento se debe ejecutar solo para solucionar problemas de replicación.  
  
 ![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
sp_replcmds [ @maxtrans = ] maxtrans  
```  
  
## <a name="arguments"></a>Argumentos  
 [  **@maxtrans=**] *maxtrans*  
 Es el número de transacciones para devolver información acerca de. *maxtrans* es **int**, su valor predeterminado es **1**, que especifica la siguiente transacción en espera para la distribución.  
  
## <a name="result-sets"></a>Conjuntos de resultados  
  
|Nombre de columna|Tipo de datos|Descripción|  
|-----------------|---------------|-----------------|  
|**Id. de artículo**|**int**|Id. del artículo.|  
|**partial_command**|**bit**|Indica si se trata de un comando parcial o no.|  
|**command**|**varbinary(1024)**|El valor del comando.|  
|**xactid**|**binary(10)**|Id. de la transacción.|  
|**xact_seqno**|**varbinary (16)**|El número de secuencia.|  
|**publication_id**|**int**|Id. de la publicación.|  
|**$command_id**|**int**|Identificador del comando en [MSrepl_commands](../../relational-databases/system-tables/msrepl-commands-transact-sql.md).|  
|**command_type**|**int**|Tipo de comando.|  
|**originator_srvname**|**sysname**|Servidor en el que se originó la transacción.|  
|**originator_db**|**sysname**|Base de datos en la que se originó la transacción.|  
|**pkHash**|**int**|Exclusivamente para uso interno.|  
|**originator_publication_id**|**int**|Id. de la publicación en la que se originó la transacción.|  
|**originator_db_version**|**int**|Versión de la base de datos en la que se originó la transacción.|  
|**originator_lsn**|**varbinary (16)**|Identifica el número de flujo de registro (LSN) para el comando de la publicación en la que se origina.|  
  
## <a name="remarks"></a>Comentarios  
 **sp_replcmds** utilizado por el proceso del lector de registro en la replicación transaccional.  
  
 Replicación trata el primer cliente que ejecuta **sp_replcmds** dentro de una base de datos como el registro del log.  
  
 Este procedimiento puede generar comandos para tablas calificadas por el propietario o no calificar el nombre de la tabla (valor predeterminado). Agregar nombres de tabla calificados permite replicar datos de tablas que pertenecen a un usuario específico de una base de datos a tablas que pertenecen al mismo usuario en otra base de datos.  
  
> [!NOTE]  
>  Debido a que el nombre de tabla en la base de datos de origen está calificado mediante el nombre del propietario, el propietario de la tabla en la base de datos de destino deberá tener ese mismo nombre.  
  
 Los clientes que intentan ejecutar **sp_replcmds** dentro de la misma base de datos reciben el error 18752 hasta que el primer cliente desconecta. Después de que el primer cliente se desconecta, se puede ejecutar otro cliente **sp_replcmds**, y se convierte en el nuevo registro del log.  
  
 Se agrega un mensaje de advertencia número 18759 tanto el [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] registro de errores y la [!INCLUDE[msCoName](../../includes/msconame-md.md)] registro de la aplicación de Windows si **sp_replcmds** no puede replicar un comando de texto porque no es el puntero de texto recuperar en la misma transacción.  
  
## <a name="permissions"></a>Permisos  
 Solo los miembros de la **sysadmin** rol fijo de servidor o el **db_owner** rol fijo de base de datos se puede ejecutar **sp_replcmds**.  
  
## <a name="see-also"></a>Vea también  
 [Mensajes de error](../../relational-databases/native-client-odbc-error-messages/error-messages.md)   
 [sp_repldone &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-repldone-transact-sql.md)   
 [sp_replflush &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-replflush-transact-sql.md)   
 [sp_repltrans &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-repltrans-transact-sql.md)   
 [Procedimientos almacenados del sistema &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
