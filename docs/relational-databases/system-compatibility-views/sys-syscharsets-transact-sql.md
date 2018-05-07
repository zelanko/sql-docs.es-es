---
title: Sys.syscharsets (Transact-SQL) | Documentos de Microsoft
ms.custom: ''
ms.date: 03/15/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.component: system-compatibility-views
ms.reviewer: ''
ms.suite: sql
ms.technology: system-objects
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- sys.syscharsets
- syscharsets
- sys.syscharsets_TSQL
- syscharsets_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- syscharsets system table
- sys.syscharsets compatibility view
ms.assetid: f16d987c-bd19-4668-9ef7-785b8fb9ff5b
caps.latest.revision: 42
author: rothja
ms.author: jroth
manager: craigg
monikerRange: '>= aps-pdw-2016 || = azuresqldb-current || = azure-sqldw-latest || >= sql-server-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: 05812269c42b4d20a694d8a51362a376ea62d527
ms.sourcegitcommit: f1caaa156db2b16e817e0a3884394e7b30fb642f
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/04/2018
---
# <a name="syssyscharsets-transact-sql"></a>sys.syscharsets (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  Contiene una fila para cada juego de caracteres y criterio de ordenación definido para su uso por el [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]. Uno de los criterios de ordenación se marcará en **sysconfigures** como el criterio de ordenación predeterminado. Es el único que se utiliza en realidad.  
  
|Nombre de columna|Tipo de datos|Description|  
|-----------------|---------------|-----------------|  
|**Tipo**|**smallint**|Tipo de entidad que representa esta fila:<br /><br /> 1001 = juego de caracteres.<br /><br /> 2001 = Criterio de ordenación.|  
|**id**|**tinyint**|Id. único del orden o juego de caracteres. Observe que los órdenes y los juegos de caracteres no pueden compartir el mismo número de Id. El intervalo de identificadores entre 1 y 240 está reservado para uso del [!INCLUDE[ssDE](../../includes/ssde-md.md)].|  
|**CSID**|**tinyint**|Si la fila representa un juego de caracteres, este campo no se usa. Si la fila representa un orden, este campo es el Id. del juego de caracteres sobre el que se basa el orden. Se supone que existe en la tabla una fila con este Id. de juego de caracteres.|  
|**status**|**smallint**|Bits de información del estado interno del sistema.|  
|**Nombre**|**sysname**|Nombre único para el orden o juego de caracteres. Este campo solo debe contener las letras A-Z o a-z, números 0 - 9 y caracteres de subrayado (_) y debe empezar por una letra.|  
|**Descripción**|**nvarchar(255)**|Descripción opcional de las características del orden o juego de caracteres.|  
|**binarydefinition**|**varbinary(6000)**|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|**Definición**|**imagen**|Definición interna del orden o juego de caracteres. La estructura de los datos de este campo depende del tipo.|  
  
## <a name="see-also"></a>Vea también  
 [Asignar tablas del sistema a vistas del sistema &#40;Transact-SQL&#41;](../../relational-databases/system-tables/mapping-system-tables-to-system-views-transact-sql.md)   
 [Vistas de compatibilidad &#40;Transact-SQL&#41;](~/relational-databases/system-compatibility-views/system-compatibility-views-transact-sql.md)  
  
  
