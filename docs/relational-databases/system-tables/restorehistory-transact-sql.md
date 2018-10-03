---
title: RestoreHistory (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/03/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- restorehistory
- restorehistory_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- restorehistory system table
ms.assetid: 9140ecc1-d912-4d76-ae70-e2a857da6d44
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 4b5b6861d1dcd4a9e516fbbf9d1ef22af7ea881d
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/01/2018
ms.locfileid: "47698113"
---
# <a name="restorehistory-transact-sql"></a>restorehistory (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Contiene una fila por cada operación de restauración. Esta tabla se almacena en el **msdb** base de datos.  
  
|Nombre de columna|Tipo de datos|Descripción|  
|-----------------|---------------|-----------------|  
|**restore_history_id**|**int**|Número de identificación único que identifica cada operación de restauración. Clave principal de identidad.|  
|**restore_date**|**datetime**|Fecha y hora de finalización de la operación de restauración. Puede ser NULL.|  
|**destination_database_name**|**nvarchar(128)**|Nombre de la base de datos de destino de la operación de restauración. Puede ser NULL.|  
|**user_name**|**nvarchar(128)**|Nombre del usuario que realizó la operación de restauración. Puede ser NULL.|  
|**backup_set_id**|**int**|Número de identificación único que identifica el conjunto de copia de seguridad que se restaura. Referencias **backupset (backup_set_id)**.|  
|**restore_type**|**char(1)**|Tipo de operación de restauración:<br /><br /> D = Base de datos<br /><br /> F = Archivo <br /><br /> G = Grupo de archivos <br /><br /> I = Diferencial <br /><br /> L = Registro<br /><br /> V = Solo comprobar <br /><br /> Puede ser NULL.|  
|**Reemplazar**|**bit**|Indica si la operación de restauración especificó la opción REPLACE:<br /><br /> 1 = Especificada<br /><br /> 0 = No especificada<br /><br /> Puede ser NULL.<br /><br /> Si se revierte una base de datos a una instantánea de base de datos, 0 es la única opción.|  
|**recovery**|**bit**|Indica si la operación de restauración especificó la opción RECOVERY o NORECOVERY:<br /><br /> 1 = RECOVERY <br /><br /> Puede ser NULL.<br /><br /> Cuando se revierte una base de datos a una instantánea de base de datos, 1 es la única opción.<br /><br /> 0 = NORECOVERY|  
|**Reiniciar**|**bit**|Indica si la operación de restauración especificó la opción RESTART:<br /><br /> 1 = Especificada<br /><br /> 0 = No especificada<br /><br /> Puede ser NULL.<br /><br /> Si se revierte una base de datos a una instantánea de base de datos, 0 es la única opción.|  
|**stop_at**|**datetime**|Indica el momento hasta el cual se recuperó la base de datos. Puede ser NULL.|  
|**device_count**|**tinyint**|Número de dispositivos implicados en la operación de restauración. Este número puede ser inferior al número de tipos de medios utilizados para la copia de seguridad. Puede ser NULL.<br /><br /> Si se revierte una base de datos a una instantánea de base de datos, el número es siempre 1.|  
|**stop_at_mark_name**|**nvarchar(128)**|Indica la recuperación de la transacción que contiene la marca con nombre. Puede ser NULL.<br /><br /> Si se revierte una base de datos a una instantánea de base de datos, este valor es NULL.|  
|**stop_before**|**bit**|Indica si la transacción que contiene la marca con nombre se incluye en la recuperación:<br /><br /> 0 = Recuperación detenida antes de la transacción marcada.<br /><br /> 1 = La recuperación incluye la transacción marcada.<br /><br /> Puede ser NULL.<br /><br /> Si se revierte una base de datos a una instantánea de base de datos, este valor es NULL.|  
  
## <a name="remarks"></a>Comentarios  
 Para reducir el número de filas en esta tabla y de otras tablas de copia de seguridad y el historial, ejecute el [sp_delete_backuphistory](../../relational-databases/system-stored-procedures/sp-delete-backuphistory-transact-sql.md) procedimiento almacenado.  
  
## <a name="see-also"></a>Vea también  
 [Copia de seguridad y restaurar tablas &#40;Transact-SQL&#41;](../../relational-databases/system-tables/backup-and-restore-tables-transact-sql.md)   
 [restorefile &#40;Transact-SQL&#41;](../../relational-databases/system-tables/restorefile-transact-sql.md)   
 [restorefilegroup &#40;Transact-SQL&#41;](../../relational-databases/system-tables/restorefilegroup-transact-sql.md)   
 [Tablas del sistema &#40;Transact-SQL&#41;](../../relational-databases/system-tables/system-tables-transact-sql.md)  
  
  
