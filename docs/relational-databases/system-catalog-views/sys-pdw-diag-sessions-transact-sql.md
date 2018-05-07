---
title: Sys.pdw_diag_sessions (Transact-SQL) | Documentos de Microsoft
ms.custom: ''
ms.date: 03/03/2017
ms.prod: sql
ms.prod_service: pdw
ms.component: system-catalog-views
ms.reviewer: ''
ms.suite: sql
ms.technology: system-objects
ms.tgt_pltfrm: ''
ms.topic: language-reference
dev_langs:
- TSQL
ms.assetid: 4d23688a-cddb-4eed-8231-ecde2a0b0e65
caps.latest.revision: 7
author: barbkess
ms.author: barbkess
manager: craigg
monikerRange: '>= aps-pdw-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: d515c217b6405061605f6191d0a3eaf8b72eadd8
ms.sourcegitcommit: f1caaa156db2b16e817e0a3884394e7b30fb642f
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 05/04/2018
---
# <a name="syspdwdiagsessions-transact-sql"></a>Sys.pdw_diag_sessions (Transact-SQL)
[!INCLUDE[tsql-appliesto-xxxxxx-xxxx-xxxx-pdw-md](../../includes/tsql-appliesto-xxxxxx-xxxx-xxxx-pdw-md.md)]

  Contiene información sobre las distintas sesiones de diagnóstico que se han creado en el sistema.  
  
|Nombre de la columna|Tipo de datos|Description|Intervalo|  
|-----------------|---------------|-----------------|-----------|  
|**Nombre**|**nvarchar(255)**|Nombre de la sesión de diagnóstico.<br /><br /> Clave para esta vista.||  
|**xml_data**|**nvarchar(4000)**|Carga XML que describe la sesión.||  
|**is_active**|**bit**|Marca que indica si el indicador está activo.||  
|**host_address**|**nvarchar(255)**|Dirección de la máquina que hospeda la definición de la sesión (nodo de Control).||  
|**principal_id**|**int**|Id. del usuario que creó la sesión en el nivel de base de datos.||  
|**database_id**|**int**|Id. de la base de datos que es el ámbito de la sesión de diagnóstico.|  
  
## <a name="see-also"></a>Vea también  
 [Almacenamiento de datos SQL y vistas de catálogo del almacén de datos en paralelo](../../relational-databases/system-catalog-views/sql-data-warehouse-and-parallel-data-warehouse-catalog-views.md)  
  
  
