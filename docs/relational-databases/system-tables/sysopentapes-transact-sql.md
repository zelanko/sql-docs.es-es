---
title: sysopentapes (Transact-SQL) | Documentos de Microsoft
ms.custom: 
ms.date: 06/10/2016
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: system-tables
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- sysopentapes
- sysopentapes_TSQL
dev_langs: TSQL
helpviewer_keywords:
- backup media [SQL Server], sysopentapes system table
- sysopentapes system table
ms.assetid: c066ca9b-9cfd-46b1-90a3-5c8dc9e7b6ae
caps.latest.revision: "37"
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: bb39670ced045b6ae5f14b9225d1b46d35aef792
ms.sourcegitcommit: 66bef6981f613b454db465e190b489031c4fb8d3
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/17/2017
---
# <a name="sysopentapes-transact-sql"></a>sysopentapes (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Contiene una fila por cada dispositivo de cinta abierto. Esta vista se almacena en la **maestro** base de datos.  
  
> [!IMPORTANT]  
>  Esta tabla del sistema se incluye como una vista para la compatibilidad con versiones anteriores. En su lugar, use la [sys.dm_io_backup_tapes &#40; Transact-SQL &#41; ](../../relational-databases/system-dynamic-management-views/sys-dm-io-backup-tapes-transact-sql.md) vista de administración dinámica.  
  
> [!NOTE]  
>  No se puede quitar el **sysopentapes** vista.  

  
|Nombre de columna|Tipo de datos|Description|  
|-----------------|---------------|-----------------|  
|**ocurra**|**nvarchar(64)**|Nombre de archivo físico del dispositivo de cinta abierto. Para obtener más información sobre la apertura y liberación de dispositivos de cinta, consulte [copia de seguridad &#40; Transact-SQL &#41; ](../../t-sql/statements/backup-transact-sql.md) y [restauración &#40; Transact-SQL &#41; ](../../t-sql/statements/restore-statements-transact-sql.md).|  
  
## <a name="permissions"></a>Permissions  
 El usuario necesita tener el permiso VIEW SERVER STATE en el servidor.  
  
  
