---
title: sp_replicationdboption (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/07/2017
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
- sp_replicationdboption_TSQL
- sp_replicationdboption
helpviewer_keywords:
- sp_replicationdboption
ms.assetid: d021864e-3f21-4d1a-89df-6c1086f753bf
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: b577600e5757ee630795724d965603f3478391ce
ms.sourcegitcommit: 182b8f68bfb345e9e69547b6d507840ec8ddfd8b
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/27/2018
ms.locfileid: "43024454"
---
# <a name="spreplicationdboption-transact-sql"></a>sp_replicationdboption (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

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
 [**@dbname=**] **'***dbname***'**  
 Es la base de datos para la que se establece la opción de base de datos de replicación. *db_name* es **sysname**, no tiene ningún valor predeterminado.  
  
 [**@optname=**] **'***optname***'**  
 Es la opción de base de datos de replicación que se puede habilitar o deshabilitar. *optname* es **sysname**, y puede tener uno de estos valores.  
  
|Valor|Descripción|  
|-----------|-----------------|  
|**publicación de mezcla**|Se puede utilizar la base de datos para publicaciones de combinación.|  
|**publicar**|Se puede utilizar la base de datos para otros tipos de publicaciones.|  
|**suscribirse**|La base de datos es una base de datos de suscripciones.|  
|**sincronizar con la copia de seguridad**|La base de datos está habilitada para una copia de seguridad coordinada. Para obtener más información, consulte [habilitar copias de seguridad coordinadas para la replicación transaccional &#40;Replication Transact-SQL Programming&#41;](../../relational-databases/replication/administration/enable-coordinated-backups-for-transactional-replication.md).|  
  
 [  **@value=**] **'***valor***'**  
 Indica si se va a habilitar o deshabilitar la opción de base de datos de replicación dada. *valor* es **sysname**y puede ser **true** o **false**. Cuando este valor es **false** y *optname* es **publicación de mezcla**, también se quitan las suscripciones a la base de datos publicada de mezcla.  
  
 [  **@ignore_distributor=**] *ignore_distributor*  
 Indica si este procedimiento almacenado se ejecuta sin conectarse al distribuidor. *ignore_distributor* es **bit**, su valor predeterminado es **0**, lo que significa que el distribuidor debe se conectará y se actualiza con el nuevo estado de la base de datos de publicación. El valor **1** solamente se debe especificar si el distribuidor es inaccesible y **sp_replicationdboption** se usa para deshabilitar la publicación.  
  
 [  **@from_scripting=**] *from_scripting*  
 [!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]  
  
## <a name="return-code-values"></a>Valores de código de retorno  
 **0** (correcto) o **1** (error)  
  
## <a name="remarks"></a>Notas  
 **sp_replicationdboption** se utiliza en la replicación de instantáneas, transaccional y de mezcla.  
  
 Este procedimiento crea o quita tablas específicas del sistema de replicación, cuentas de seguridad, etc., según las opciones proporcionadas. Conjuntos de bits de la categoría correspondiente en el **master.sysdatabases** tabla del sistema y crea las tablas del sistema necesarias.  
  
 Para deshabilitar la publicación, la base de datos de publicaciones debe estar en línea. Si existe una instantánea de base de datos para la base de datos de publicaciones, se debe quitar la instantánea antes de deshabilitar la publicación. Las instantáneas de base de datos son copias de solo lectura y sin conexión de bases de datos, y no están relacionadas con una instantánea de replicación. Para más información, vea [Instantáneas de base de datos &#40;SQL Server&#41;](../../relational-databases/databases/database-snapshots-sql-server.md).  
  
## <a name="permissions"></a>Permisos  
 Solo los miembros de la **sysadmin** rol fijo de servidor puede ejecutar **sp_replicationdboption**.  
  
## <a name="see-also"></a>Vea también  
 [Configurar la publicación y la distribución](../../relational-databases/replication/configure-publishing-and-distribution.md)   
 [Create a Publication](../../relational-databases/replication/publish/create-a-publication.md)   
 [Eliminar una publicación](../../relational-databases/replication/publish/delete-a-publication.md)   
 [Disable Publishing and Distribution](../../relational-databases/replication/disable-publishing-and-distribution.md)  (Deshabilitar la publicación y la distribución)  
 [Sys.sysdatabases &#40;Transact-SQL&#41;](../../relational-databases/system-compatibility-views/sys-sysdatabases-transact-sql.md)   
 [Procedimientos almacenados de replicación &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/replication-stored-procedures-transact-sql.md)  
  
  
