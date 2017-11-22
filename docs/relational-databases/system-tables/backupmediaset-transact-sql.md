---
title: backupmediaset (Transact-SQL) | Documentos de Microsoft
ms.custom: 
ms.date: 08/09/2016
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
- backupmediaset
- backupmediaset_TSQL
dev_langs: TSQL
helpviewer_keywords:
- backup media [SQL Server], backupmediaset system table
- backupmediaset system table
ms.assetid: d9c18a93-cab9-4db8-ae09-c6bd8145ab8f
caps.latest.revision: "39"
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 4e86380a170009fbfd8ee7fd2f891dc210cab856
ms.sourcegitcommit: 66bef6981f613b454db465e190b489031c4fb8d3
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/17/2017
---
# <a name="backupmediaset-transact-sql"></a>backupmediaset (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Contiene una fila por cada conjunto de medios de copia de seguridad. Esta tabla se almacena en la **msdb** base de datos.  
 
  
|Nombre de columna|Tipo de datos|Description|  
|-----------------|---------------|-----------------|  
|**media_set_id**|**int**|Número exclusivo de identificación del conjunto de medios. Clave principal de identidad.|  
|**media_uuid**|**uniqueidentifier**|UUID del conjunto de medios. Todos los [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] conjuntos de medios tienen un UUID.<br /><br /> En versiones anteriores de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], sin embargo, si un conjunto de medios contiene solo una familia de medios, el **media_uuid** columna podría ser NULL (**media_family_count** es 1).|  
|**media_family_count**|**tinyint**|Número de familias de medios en el conjunto de medios. Puede ser NULL.|  
|**Nombre**|**nvarchar (128)**|Nombre del conjunto de medios. Puede ser NULL.<br /><br /> Para obtener más información, consulte MEDIANAME y MEDIADESCRIPTION en [copia de seguridad &#40; Transact-SQL &#41; ](../../t-sql/statements/backup-transact-sql.md).|  
|**Descripción**|**nvarchar(255)**|Texto de descripción del conjunto de medios. Puede ser NULL.<br /><br /> Para obtener más información, consulte MEDIANAME y MEDIADESCRIPTION en [copia de seguridad &#40; Transact-SQL &#41; ](../../t-sql/statements/backup-transact-sql.md).|  
|**nombre_software**|**nvarchar (128)**|Nombre del software de copia de seguridad que escribió la etiqueta del medio. Puede ser NULL.|  
|**software_vendor_id**|**int**|Número de identificación del proveedor de software que escribió la etiqueta del medio de copia de seguridad. Puede ser NULL.<br /><br /> El valor de [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] es el hexadecimal 0 x 1200.|  
|**MTF_major_version**|**tinyint**|Número principal de la versión de formato de cinta de [!INCLUDE[msCoName](../../includes/msconame-md.md)] utilizada para generar este conjunto de medios. Puede ser NULL.|  
|**mirror_count**|**tinyint**|Número de reflejos en el conjunto de medios.|  
|**is_password_protected**|**bit**|Indica si el conjunto de medios está protegido con contraseña:<br /><br /> 0 = Sin protección <br /><br /> 1 = Protegido|  
|**llamada is_compressed**|**bit**|Si la copia de seguridad está comprimida:<br /><br /> 0 = no comprimida<br /><br /> 1 = comprimida<br /><br /> Durante una **msdb** actualización, este valor se establece en NULL. lo que indica que la copia de seguridad no está comprimida.|  
|**is_encrypted**|**Bits**|Si la copia de seguridad está cifrada:<br /><br /> 0 = No cifrado<br /><br /> 1 = Cifrada|  
  
## <a name="remarks"></a>Comentarios  
 RESTORE VERIFYONLY FROM *backup_device* WITH LOADHISTORY rellena las columnas de la **backupmediaset** tabla con los valores apropiados del encabezado del conjunto de medios.  
  
 Para reducir el número de filas en esta tabla y en otras tablas de historial y de copia de seguridad, ejecute el [sp_delete_backuphistory](../../relational-databases/system-stored-procedures/sp-delete-backuphistory-transact-sql.md) procedimiento almacenado.  
  
## <a name="see-also"></a>Vea también  
 [Copia de seguridad y restauración tablas &#40; Transact-SQL &#41;](../../relational-databases/system-tables/backup-and-restore-tables-transact-sql.md)   
 [backupfile &#40;Transact-SQL&#41;](../../relational-databases/system-tables/backupfile-transact-sql.md)   
 [backupfilegroup &#40;Transact-SQL&#41;](../../relational-databases/system-tables/backupfilegroup-transact-sql.md)   
 [backupmediafamily &#40;Transact-SQL&#41;](../../relational-databases/system-tables/backupmediafamily-transact-sql.md)   
 [backupset &#40;Transact-SQL&#41;](../../relational-databases/system-tables/backupset-transact-sql.md)   
 [Tablas del sistema &#40; Transact-SQL &#41;](../../relational-databases/system-tables/system-tables-transact-sql.md)  
  
  
