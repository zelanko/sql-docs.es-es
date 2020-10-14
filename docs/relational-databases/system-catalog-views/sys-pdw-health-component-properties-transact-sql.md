---
description: sys.pdw_health_component_properties (Transact-SQL)
title: sys.pdw_health_component_properties (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: system-objects
ms.topic: conceptual
ms.assetid: 66999c0c-dc43-4327-99fb-8366f465e69d
author: ronortloff
ms.author: rortloff
monikerRange: '>= aps-pdw-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: 966c544a42ea97ed6f7233bba1a57979a87ba5ac
ms.sourcegitcommit: 22dacedeb6e8721e7cdb6279a946d4002cfb5da3
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/14/2020
ms.locfileid: "92037002"
---
# <a name="syspdw_health_component_properties-transact-sql"></a>sys.pdw_health_component_properties (Transact-SQL)
[!INCLUDE [pdw](../../includes/applies-to-version/pdw.md)]

  Almacena las propiedades que describen un dispositivo. Algunas propiedades muestran el estado del dispositivo y algunas propiedades describen el propio dispositivo.  
  
|Nombre de columna|Tipo de datos|Descripción|Intervalo|  
|-----------------|---------------|-----------------|-----------|  
|property_id|**int**|Identificador único de la propiedad de un componente.<br /><br /> property_id y component_id forman la clave de esta vista.|NOT NULL|  
|component_id|**int**|IDENTIFICADOR del componente. Vea [sys.pdw_health_components &#40;&#41;de Transact-SQL ](../../relational-databases/system-catalog-views/sys-pdw-health-components-transact-sql.md).<br /><br /> property_id y component_id forman la clave de esta vista.|NOT NULL|  
|property_name|**nvarchar(255)**|Nombre de la propiedad.|NOT NULL|  
|physical_name|**nvarchar(32)**|Nombre de propiedad definido por el fabricante.|NOT NULL|  
|is_key|**bit**|Determina si la instancia del dispositivo es única o no única.|NOT NULL<br /><br /> 0: la instancia del dispositivo es única.<br /><br /> 1: la instancia del dispositivo no es única.|  
  
## <a name="see-also"></a>Consulte también  
 [Vistas de catálogo de Azure Synapse Analytics y Almacenamiento de datos paralelos](../../relational-databases/system-catalog-views/sql-data-warehouse-and-parallel-data-warehouse-catalog-views.md)  
  
  
