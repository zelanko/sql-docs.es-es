---
title: Sys.pdw_health_alerts (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/03/2017
ms.prod: sql
ms.prod_service: pdw
ms.reviewer: ''
ms.technology: system-objects
ms.topic: conceptual
ms.assetid: 49c01e5f-ee47-41a0-871d-35a759f50851
author: ronortloff
ms.author: rortloff
manager: craigg
monikerRange: '>= aps-pdw-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: d26b8d9b19b29a92481c3dccf9d4809e74691a44
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/01/2018
ms.locfileid: "47794473"
---
# <a name="syspdwhealthalerts-transact-sql"></a>Sys.pdw_health_alerts (Transact-SQL)
[!INCLUDE[tsql-appliesto-xxxxxx-xxxx-xxxx-pdw-md](../../includes/tsql-appliesto-xxxxxx-xxxx-xxxx-pdw-md.md)]

  Almacena las propiedades de las diferentes alertas que se pueden producir en el sistema; se trata de una tabla de catálogo para las alertas.  
  
|Nombre de la columna|Tipo de datos|Descripción|Intervalo|  
|-----------------|---------------|-----------------|-----------|  
|alert_id|**int**|Identificador único de la alerta.<br /><br /> Clave para esta vista.|NOT NULL|  
|IdComponente|**int**|Identificador del componente al que se aplica esta alerta. El componente es un identificador de componente generales, como "Alimentación" y no es específico para una instalación. Consulte [sys.pdw_health_components &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-pdw-health-components-transact-sql.md).|NOT NULL|  
|alert_name|**nvarchar(255)**|Nombre de la alerta.|NOT NULL|  
|state|**nvarchar(32)**|Estado de la alerta.|NOT NULL<br /><br /> Valores posibles:<br /><br /> 'Operational'<br /><br /> 'No operativa'<br /><br /> Está "Degradado"<br /><br /> 'Error'|  
|severity|**nvarchar(32)**|Gravedad de la alerta.|NOT NULL<br /><br /> Valores posibles:<br /><br /> "Informativo"<br /><br /> "Advertencia"<br /><br /> 'Error'|  
|Tipo|**nvarchar(32)**|Tipo de alerta.|NOT NULL<br /><br /> Valores posibles:<br /><br /> StatusChange - ha cambiado el estado del dispositivo.<br /><br /> Umbral - un valor ha superado el valor de umbral.|  
|description|**nvarchar(4000)**|Descripción de la alerta.|NOT NULL|  
|condición|**nvarchar(255)**|Se utiliza cuando escriba = umbral. Define cómo se calcula el umbral de alerta.|NULL|  
|status|**nvarchar(32)**|Estado de alerta|NULL|  
|condition_value|**bit**|Indica si la alerta puede producirse durante la operación del sistema.|NULL<br /><br /> Valores posibles<br /><br /> 0 - no se generará la alerta.<br /><br /> 1 - la alerta se genera.|  
  
## <a name="see-also"></a>Vea también  
 [SQL Data Warehouse y vistas de catálogo del almacén de datos en paralelo](../../relational-databases/system-catalog-views/sql-data-warehouse-and-parallel-data-warehouse-catalog-views.md)  
  
  
