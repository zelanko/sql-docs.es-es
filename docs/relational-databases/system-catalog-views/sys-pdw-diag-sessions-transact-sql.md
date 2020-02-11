---
title: Sys. pdw_diag_sessions (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/03/2017
ms.prod: sql
ms.technology: system-objects
ms.topic: language-reference
dev_langs:
- TSQL
ms.assetid: 4d23688a-cddb-4eed-8231-ecde2a0b0e65
author: ronortloff
ms.author: rortloff
monikerRange: '>= aps-pdw-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: fa06005679e31381f723b30b9f68e5ce0d89ae1e
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/08/2020
ms.locfileid: "68127686"
---
# <a name="syspdw_diag_sessions-transact-sql"></a>Sys. pdw_diag_sessions (Transact-SQL)
[!INCLUDE[tsql-appliesto-xxxxxx-xxxx-xxxx-pdw-md](../../includes/tsql-appliesto-xxxxxx-xxxx-xxxx-pdw-md.md)]

  Contiene información relacionada con las distintas sesiones de diagnóstico que se han creado en el sistema.  
  
|Nombre de columna|Tipo de datos|Descripción|Intervalo|  
|-----------------|---------------|-----------------|-----------|  
|**Name**|**nvarchar(255)**|Nombre de la sesión de diagnóstico.<br /><br /> Clave para esta vista.||  
|**xml_data**|**nvarchar(4000)**|Carga XML que describe la sesión.||  
|**is_active**|**bit**|Marca que indica si la marca está activa.||  
|**host_address**|**nvarchar(255)**|Dirección de la máquina que hospeda la definición de sesión (nodo de control).||  
|**principal_id**|**int**|IDENTIFICADOR del usuario que creó la sesión en el nivel de base de datos.||  
|**database_id**|**int**|IDENTIFICADOR de la base de datos que constituye el ámbito de la sesión de diagnóstico.|  
  
## <a name="see-also"></a>Consulte también  
 [SQL Data Warehouse y vistas de catálogo de almacenamiento de datos paralelos](../../relational-databases/system-catalog-views/sql-data-warehouse-and-parallel-data-warehouse-catalog-views.md)  
  
  
