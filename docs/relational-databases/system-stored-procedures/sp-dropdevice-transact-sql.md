---
title: sp_dropdevice (Transact-SQL) | Documentos de Microsoft
ms.custom: 
ms.date: 08/09/2016
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: system-stored-procedures
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- sp_dropdevice_TSQL
- sp_dropdevice
dev_langs: TSQL
helpviewer_keywords:
- backup devices [SQL Server], deleting
- sp_dropdevice
ms.assetid: c8b07189-7c35-414b-acc1-45bd6e7e17c3
caps.latest.revision: "37"
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: dbc7324d26e19d03472d759db8845035ea5a4dd8
ms.sourcegitcommit: 66bef6981f613b454db465e190b489031c4fb8d3
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/17/2017
---
# <a name="spdropdevice-transact-sql"></a>sp_dropdevice (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Quita un dispositivo de base de datos o un dispositivo de copia de seguridad de una instancia de la [!INCLUDE[ssDEversion2005](../../includes/ssdeversion2005-md.md)], elimina la entrada de **master.dbo.sysdevices**.  
   
 ![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
sp_dropdevice [ @logicalname = ] 'device'   
    [ , [ @delfile = ] 'delfile' ]  
```  
  
## <a name="arguments"></a>Argumentos  
 [  **@logicalname=** ] **'***dispositivo***'**  
 Es el nombre lógico del dispositivo de base de datos o el dispositivo de copia de seguridad, como se muestra en **master.dbo.sysdevices.name**. *dispositivo* es **sysname**, no tiene ningún valor predeterminado.  
  
 [  **@delfile=** ] **'***delfile***'**  
 Especifica si se debe eliminar el archivo de dispositivo de copia de seguridad físico. *delfile* es **varchar(7)**. Si se especifica como **DELFILE**, se elimina el archivo de disco de dispositivo de copia de seguridad físico.  
  
## <a name="return-code-values"></a>Valores de código de retorno  
 0 (correcto) o 1 (error)  
  
## <a name="result-sets"></a>Conjuntos de resultados  
 Ninguno  
  
## <a name="remarks"></a>Comentarios  
 **sp_dropdevice** no se puede usar dentro de una transacción.  
  
## <a name="permissions"></a>Permissions  
 Debe pertenecer al rol fijo de servidor **diskadmin** .  
  
## <a name="examples"></a>Ejemplos  
 En el ejemplo siguiente se muestra cómo quitar el dispositivo de volcado de cinta `tapedump1` del [!INCLUDE[ssDE](../../includes/ssde-md.md)].  
  
```  
EXEC sp_dropdevice 'tapedump1';  
```  
  
## <a name="see-also"></a>Vea también  
 [Dispositivos de copia de seguridad &#40;SQL Server&#41;](../../relational-databases/backup-restore/backup-devices-sql-server.md)   
 [Eliminar un dispositivo de copia de seguridad &#40; SQL Server &#41;](../../relational-databases/backup-restore/delete-a-backup-device-sql-server.md)   
 [sp_addumpdevice &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addumpdevice-transact-sql.md)   
 [sp_helpdb &#40; Transact-SQL &#41;](../../relational-databases/system-stored-procedures/sp-helpdb-transact-sql.md)   
 [sp_helpdevice &#40; Transact-SQL &#41;](../../relational-databases/system-stored-procedures/sp-helpdevice-transact-sql.md)   
 [Procedimientos almacenados del sistema &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
