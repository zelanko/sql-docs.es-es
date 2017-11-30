---
title: Sys.sysfiles (Transact-SQL) | Documentos de Microsoft
ms.custom: 
ms.date: 03/15/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: system-compatibility-views
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- sysfiles
- sys.sysfiles_TSQL
- sys.sysfiles
- sysfiles_TSQL
dev_langs: TSQL
helpviewer_keywords:
- sysfiles system table
- sys.sysfiles compatibility view
ms.assetid: 3b47f38d-1cff-404d-89d3-9342c451c802
caps.latest.revision: "40"
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 7190a2389fc1504cb8068eb5ea9b6ffd7ed127fb
ms.sourcegitcommit: 9fbe5403e902eb996bab0b1285cdade281c1cb16
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/27/2017
---
# <a name="syssysfiles-transact-sql"></a>sys.sysfiles (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Contiene una fila por cada archivo de una base de datos.  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssnoteCompView](../../includes/ssnotecompview-md.md)]  
  
|Nombre de columna|Tipo de datos|Description|  
|-----------------|---------------|-----------------|  
|**FileID**|**smallint**|Número de identificación del archivo, único para cada base de datos.|  
|**Id. de grupo**|**smallint**|Número de identificación del grupo de archivos.|  
|**tamaño**|**int**|Tamaño de archivo, en páginas de 8 KB.|  
|**MaxSize**|**int**|Tamaño máximo de archivo, en páginas de 8 KB.<br /><br /> 0 = Sin aumento de tamaño.<br /><br /> -1 = El archivo crece hasta que el disco esté lleno.<br /><br /> 268435456 = El archivo de registro aumentará de tamaño hasta un tamaño máximo de 2 TB.<br /><br /> Nota: Las bases de datos que se actualizan con un tamaño de archivo ilimitado del registro indican -1 para el tamaño máximo del archivo de registro.|  
|**crecimiento**|**int**|Tamaño de aumento de la base de datos. Puede ser el número de páginas o el porcentaje del tamaño del archivo, según el valor de **estado**.<br /><br /> 0 = Sin aumento de tamaño.|  
|**status**|**int**|Bits de estado para la **crecimiento** valor en megabytes (MB) o kilobytes (KB).<br /><br /> 0x2 = Archivo de disco.<br /><br /> 0x40 = Archivo de registro.<br /><br /> 0x100000 = Crecimiento. Este valor es un porcentaje y no el número de páginas.|  
|**rendimiento**|**int**|Reservado.|  
|**Nombre**|**sysname**|Nombre lógico del archivo.|  
|**nombre de archivo**|**nvarchar (260)**|Nombre del dispositivo físico. Incluye la ruta de acceso completa al archivo.|  
  
## <a name="see-also"></a>Vea también  
 [Asignar tablas del sistema a vistas del sistema &#40; Transact-SQL &#41;](../../relational-databases/system-tables/mapping-system-tables-to-system-views-transact-sql.md)   
 [Vistas de compatibilidad &#40;Transact-SQL&#41;](~/relational-databases/system-compatibility-views/system-compatibility-views-transact-sql.md)  
  
  
