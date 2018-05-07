---
title: Sys.database_recovery_status (Transact-SQL) | Documentos de Microsoft
ms.custom: ''
ms.date: 08/12/2016
ms.prod: sql
ms.prod_service: database-engine
ms.component: system-catalog-views
ms.reviewer: ''
ms.suite: sql
ms.technology: system-objects
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- database_recovery_status_TSQL
- database_recovery_status
- sys.database_recovery_status
- sys.database_recovery_status_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.database_recovery_status catalog view
ms.assetid: 46fab234-1542-49be-8edf-aa101e728acf
caps.latest.revision: 31
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 2cdefec3d2f5ffd6a8ce326c4d3afd78df47de44
ms.sourcegitcommit: f1caaa156db2b16e817e0a3884394e7b30fb642f
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/04/2018
---
# <a name="sysdatabaserecoverystatus-transact-sql"></a>sys.database_recovery_status (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Contiene una fila por base de datos. Si la base de datos no está abierta, el [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] intenta iniciarla.  
  
 Para ver la fila de una base de datos distinto de **maestro** o **tempdb**, debe aplicar uno de los siguientes:  
  
-   Ser el propietario de la base de datos.  
  
-   Tener los permisos de servidor ALTER ANY DATABASE o VIEW ANY DATABASE.  
  
-   Tener el permiso CREATE DATABASE en la **maestro** base de datos.    
  
|Nombre de columna|Tipo de datos|Description|  
|-----------------|---------------|-----------------|  
|**database_id**|**int**|Id. de la base de datos, único en una instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].|  
|**database_guid**|**uniqueidentifier**|Se utiliza para relacionar entre sí todos los archivos de una base de datos. Para que la base de datos se inicie de la forma esperada, todos los archivos deben tener este GUID en la página de encabezado. Solo una base de datos puede tener este GUID, aunque se pueden crear duplicados al copiar y adjuntar bases de datos. RESTORE siempre genera un nuevo GUID cuando se restaura una base de datos que todavía no existe.<br /><br /> NULL= La base de datos está sin conexión o no se va a iniciar.|  
|**family_guid**|**uniqueidentifier**|Identificador de la familia de copias de seguridad de la base de datos para detectar estados de restauración coincidentes.<br /><br /> NULL = no se iniciará la base de datos o base de datos está sin conexión.|  
|**last_log_backup_lsn**|**numeric(25,0)**|El número de secuencia de registro inicial de la siguiente copia de seguridad de registro.<br /><br /> Si es NULL, un registro de transacciones atrás hasta no se puede realizar porque la base de datos está en recuperación SIMPLE o no hay ninguna copia de seguridad de base de datos actual.|  
|**recovery_fork_guid**|**uniqueidentifier**|Identifica la bifurcación de recuperación actual en la que está activa la base de datos.<br /><br /> NULL= La base de datos está sin conexión o no se va a iniciar.|  
|**first_recovery_fork_guid**|**uniqueidentifier**|Identificador de la bifurcación de recuperación inicial.<br /><br /> NULL= La base de datos está sin conexión o no se va a iniciar.|  
|**fork_point_lsn**|**numeric(25,0)**|Si **first_recovery_fork_guid** no es igual (! =) para **recovery_fork_guid**, **fork_point_lsn** es el número de secuencia de registro de punto de bifurcación actual. En caso contrario, el valor es NULL.|  
  
## <a name="permissions"></a>Permissions  
 [!INCLUDE[ssCatViewPerm](../../includes/sscatviewperm-md.md)] Para obtener más información, consulte [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md).  
  
## <a name="see-also"></a>Vea también  
 [Vistas de catálogo &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/catalog-views-transact-sql.md)   
 [Vistas de catálogo de archivos y bases de datos &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/databases-and-files-catalog-views-transact-sql.md)   
 [RESTORE HEADERONLY &#40;Transact-SQL&#41;](../../t-sql/statements/restore-statements-headeronly-transact-sql.md)   
 [Preguntas frecuentes sobre consultas del catálogo de sistema de SQL Server](../../relational-databases/system-catalog-views/querying-the-sql-server-system-catalog-faq.md)  
  
  
