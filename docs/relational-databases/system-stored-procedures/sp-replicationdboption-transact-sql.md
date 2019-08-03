---
title: sp_replicationdboption (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/07/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_replicationdboption_TSQL
- sp_replicationdboption
helpviewer_keywords:
- sp_replicationdboption
ms.assetid: d021864e-3f21-4d1a-89df-6c1086f753bf
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: ac51409db23f4b8eefb3616d5daf5ca43b3ab0f6
ms.sourcegitcommit: 728a4fa5a3022c237b68b31724fce441c4e4d0ab
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/03/2019
ms.locfileid: "68771253"
---
# <a name="spreplicationdboption-transact-sql"></a>sp_replicationdboption (Transact-SQL)
[!INCLUDE[appliesto-ss-asdbmi-xxxx-xxx-md](../../includes/appliesto-ss-asdbmi-xxxx-xxx-md.md)]

  Establece una opción de base de datos de replicación para la base de datos especificada. Este procedimiento almacenado se ejecuta en el publicador o el suscriptor de cualquier base de datos.  
  
 ![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
sp_replicationdboption [ @dbname= ] 'db_name'   
        , [ @optname= ] 'optname'   
        , [ @value= ] 'value'   
    [ , [ @ignore_distributor= ] ignore_distributor ]  
    [ , [ @from_scripting = ] from_scripting ]  
```  
  
## <a name="arguments"></a>Argumentos  
 **[@dbname=** ] **'***dbname***'**  
 Es la base de datos para la que se establece la opción de base de datos de replicación. *db_name* es de **tipo sysname**y no tiene ningún valor predeterminado.  
  
 **[@optname=** ] **'***optname***'**  
 Es la opción de base de datos de replicación que se puede habilitar o deshabilitar. *optname* es de **tipo sysname**y puede tener uno de estos valores.  
  
|Valor|Descripción|  
|-----------|-----------------|  
|**publicación de combinación**|Se puede utilizar la base de datos para publicaciones de combinación.|  
|**publish**|Se puede utilizar la base de datos para otros tipos de publicaciones.|  
|**ID**|La base de datos es una base de datos de suscripciones.|  
|**sincronizar con copia de seguridad**|La base de datos está habilitada para una copia de seguridad coordinada. Para obtener más información, vea [Habilitar copias de seguridad coordinadas para la &#40;replicación transaccional programación&#41;de Transact-SQL](../../relational-databases/replication/administration/enable-coordinated-backups-for-transactional-replication.md).|  
  
`[ @value = ] 'value'`Indica si se debe habilitar o deshabilitar la opción de base de datos de replicación dada. *Value* es de **tipo sysname**y puede ser **true** o **false**. Cuando este valor es **false** y *optname* es **Merge Publish**, también se quitan las suscripciones a la base de datos publicada de mezcla.  
  
`[ @ignore_distributor = ] ignore_distributor`Indica si este procedimiento almacenado se ejecuta sin conectarse al distribuidor. *ignore_distributor* es de **bit**, con un valor predeterminado de **0**, lo que significa que el distribuidor debe estar conectado y actualizado con el nuevo estado de la base de datos de publicación. Solo se debe especificar el valor **1** si no se puede obtener acceso al distribuidor y se utiliza **sp_replicationdboption** para deshabilitar la publicación.  
  
`[ @from_scripting = ] from_scripting` [!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]  
  
## <a name="return-code-values"></a>Valores de código de retorno  
 **0** (correcto) o **1** (error)  
  
## <a name="remarks"></a>Comentarios  
 **sp_replicationdboption** se utiliza en la replicación de instantáneas, la replicación transaccional y la replicación de mezcla.  
  
 Este procedimiento crea o quita tablas específicas del sistema de replicación, cuentas de seguridad, etc., según las opciones proporcionadas. Establece el bit de categoría correspondiente en la tabla del sistema **Master. sysdatabases** y crea las tablas del sistema necesarias.  
  
 Para deshabilitar la publicación, la base de datos de publicaciones debe estar en línea. Si existe una instantánea de base de datos para la base de datos de publicaciones, se debe quitar la instantánea antes de deshabilitar la publicación. Las instantáneas de base de datos son copias de solo lectura y sin conexión de bases de datos, y no están relacionadas con una instantánea de replicación. Para más información, vea [Instantáneas de base de datos &#40;SQL Server&#41;](../../relational-databases/databases/database-snapshots-sql-server.md).  
  
## <a name="permissions"></a>Permisos  
 Solo los miembros del rol fijo de servidor **sysadmin** pueden ejecutar **sp_replicationdboption**.  
  
## <a name="see-also"></a>Vea también  
 [Configurar la publicación y la distribución](../../relational-databases/replication/configure-publishing-and-distribution.md)   
 [Create a Publication](../../relational-databases/replication/publish/create-a-publication.md)   
 [Eliminar una publicación](../../relational-databases/replication/publish/delete-a-publication.md)   
 [Disable Publishing and Distribution](../../relational-databases/replication/disable-publishing-and-distribution.md)  (Deshabilitar la publicación y la distribución)  
 [sys.sysdatabases &#40;Transact-SQL&#41;](../../relational-databases/system-compatibility-views/sys-sysdatabases-transact-sql.md)   
 [Procedimientos almacenados de replicación &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/replication-stored-procedures-transact-sql.md)  
  
  
