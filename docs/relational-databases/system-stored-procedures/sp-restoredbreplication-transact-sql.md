---
title: sp_restoredbreplication (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_restoredbreplication
- sp_restoredbreplication_TSQL
helpviewer_keywords:
- sp_restoredbreplication
ms.assetid: a2c5ee32-e6d9-46e9-8031-8ff13c20acf7
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: 78cd6788820af2c8803f6688e0703878fe165df1
ms.sourcegitcommit: 4d3896882c5930248a6e441937c50e8e027d29fd
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/05/2020
ms.locfileid: "82817069"
---
# <a name="sp_restoredbreplication-transact-sql"></a>sp_restoredbreplication (Transact-SQL)
[!INCLUDE[appliesto-ss-asdbmi-xxxx-xxx-md](../../includes/appliesto-ss-asdbmi-xxxx-xxx-md.md)]

  Quita la configuración de replicación si se restaura una base de datos al servidor, base de datos o sistema que no la ha originado y que, por tanto, no es capaz de ejecutar procesos de replicación. Cuando se restaura una base de datos replicada a un servidor o base de datos que no es donde se creó la copia de seguridad, no es posible conservar la configuración de replicación. En la restauración, el servidor llama a **sp_restoredbreplication** directamente para quitar automáticamente los metadatos de replicación de la base de datos restaurada.  
  
 ![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
sp_restoredbreplication [ @srv_orig = ] 'original_server_name'  
        , [ @db_orig = ] 'original_database_name'  
    [ , [ @keep_replication = ] keep_replication ]  
    [ , [ @perform_upgrade = ] perform_upgrade ]  
```  
  
## <a name="arguments"></a>Argumentos  
`[ @srv_orig = ] 'original_server_name'`  
 El nombre del servidor donde se creó la copia de seguridad. *original_server_name* es de **tipo sysname**y no tiene ningún valor predeterminado.  
  
`[ @db_orig = ] 'original_database_name'`  
 Nombre de la base de datos de la que se realizó la copia de seguridad. *original_database_name* es de **tipo sysname**y no tiene ningún valor predeterminado.  
  
`[ @keep_replication = ] keep_replication`  
 [!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]  
  
`[ @perform_upgrade = ] perform_upgrade`  
 [!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]  
  
## <a name="return-code-values"></a>Valores de código de retorno  
 **0** (correcto) o **1** (error)  
  
## <a name="remarks"></a>Observaciones  
 **sp_restoredbreplication** se utiliza en todos los tipos de replicación.  
  
## <a name="permissions"></a>Permisos  
 Solo los miembros del rol fijo de servidor **sysadmin** o **dbcreator** o del esquema de la base de datos **DBO** pueden ejecutar **sp_restoredbreplication**.  
  
## <a name="see-also"></a>Consulte también  
 [Procedimientos almacenados de replicación &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/replication-stored-procedures-transact-sql.md)  
  
  
