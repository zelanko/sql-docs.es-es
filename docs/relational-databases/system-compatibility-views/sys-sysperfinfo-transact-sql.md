---
title: Sys.sysperfinfo (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/15/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sysperfinfo_TSQL
- sys.sysperfinfo_TSQL
- sys.sysperfinfo
- sysperfinfo
dev_langs:
- TSQL
helpviewer_keywords:
- sys.sysperfinfo compatibility view
- sysperfinfo system table
ms.assetid: e22a81cd-27de-4690-9443-6aad6393bd3c
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: 954ad81a9bbc2c2a76e825a944a292b00e478218
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/01/2018
ms.locfileid: "47596704"
---
# <a name="syssysperfinfo-transact-sql"></a>sys.sysperfinfo (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Contiene un [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] representación de los contadores de rendimiento interno que se pueden mostrar a través del Monitor de sistema de Windows.  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssnoteCompView](../../includes/ssnotecompview-md.md)]  
  
|Nombre de columna|Tipo de datos|Descripción|  
|-----------------|---------------|-----------------|  
|**object_name**|**nchar(128)**|Nombre de objeto de rendimiento, como **SQLServer:LockManager** o **SQLServer:BufferManager**.|  
|**counter_name**|**nchar(128)**|Nombre del contador de rendimiento dentro del objeto, como **solicitudes de página** o **bloqueos solicitados**.|  
|**instance_name**|**nchar(128)**|Instancia con nombre del contador. Por ejemplo, existen contadores que se mantienen para cada tipo de bloqueo, como **tabla**, **página**, **clave**, y así sucesivamente. El nombre de instancia permite distinguir entre contadores similares.|  
|**cntr_value**|**bigint**|Valor del contador. Con frecuencia, será un nivel o un contador que se incrementa continuamente y que cuenta las veces que se produce el evento de la instancia.|  
|**cntr_type**|**int**|Tipo de contador definido en la arquitectura de rendimiento de Windows.|  
  
## <a name="see-also"></a>Vea también  
 [Asignar tablas del sistema a vistas del sistema &#40;Transact-SQL&#41;](../../relational-databases/system-tables/mapping-system-tables-to-system-views-transact-sql.md)   
 [Vistas de compatibilidad &#40;Transact-SQL&#41;](~/relational-databases/system-compatibility-views/system-compatibility-views-transact-sql.md)  
  
  
