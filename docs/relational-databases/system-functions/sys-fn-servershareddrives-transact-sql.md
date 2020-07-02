---
title: Sys. fn_servershareddrives (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- fn_servershareddrives
- fn_servershareddrives_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- fn_servershareddrives function
- shared drives [SQL Server]
- names [SQL Server], shared drives
- sys.fn_serversharedrives function
ms.assetid: ff01eff7-8cb6-460c-ba7a-6a52bda6d471
author: rothja
ms.author: jroth
ms.openlocfilehash: ce7301325f8cf6ec782b9c9850399617171146f7
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/01/2020
ms.locfileid: "85652007"
---
# <a name="sysfn_servershareddrives-transact-sql"></a>sys.fn_servershareddrives (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/applies-to-version/sqlserver.md)]

  Devuelve los nombres de las unidades compartidas utilizadas por el servidor en clúster.  
  
> [!IMPORTANT]  
>  Esta función del sistema de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] se incluye por compatibilidad con versiones anteriores. En su lugar, se recomienda usar [Sys. dm_io_cluster_valid_path_names &#40;&#41;de Transact-SQL](../../relational-databases/system-dynamic-management-views/sys-dm-io-cluster-valid-path-names-transact-sql.md) .  
  
 ![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
fn_servershareddrives()  
```  
  
## <a name="tables-returned"></a>Tablas devueltas  
 Si el servidor actual es un servidor en clúster, **fn_servershareddrives** devuelve el nombre de unidad de las unidades compartidas.  
  
 Si la instancia del servidor actual no es un servidor en clúster, **fn_servershareddrives** devuelve un conjunto de filas vacío.  
  
## <a name="remarks"></a>Comentarios  
 `fn_servershareddrives` devuelve una lista de unidades compartidas que utiliza este servidor en clúster. Estas unidades compartidas pertenecen al mismo grupo de clúster que el [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] recurso. Además, el recurso de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] depende de estas unidades.  
  
 Esta función resulta útil para identificar las unidades disponibles para los usuarios.  
  
## <a name="permissions"></a>Permisos  
 El usuario debe tener permiso VIEW SERVER STATE para la instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
## <a name="examples"></a>Ejemplos  
 En el siguiente ejemplo se utiliza `fn_servershareddrives` para realizar una consulta en una instancia de servidor en clúster:  
  
```  
SELECT * FROM fn_servershareddrives();  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
 DriveName  
  
 -------\-  
  
 m  
  
 n  
  
## <a name="see-also"></a>Consulte también  
 [Sys. dm_io_cluster_valid_path_names &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-io-cluster-valid-path-names-transact-sql.md)   
 [Sys. dm_io_cluster_shared_drives &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-io-cluster-shared-drives-transact-sql.md)   
 [Sys. fn_virtualservernodes &#40;Transact-SQL&#41;](../../relational-databases/system-functions/sys-fn-virtualservernodes-transact-sql.md)  
  
  
