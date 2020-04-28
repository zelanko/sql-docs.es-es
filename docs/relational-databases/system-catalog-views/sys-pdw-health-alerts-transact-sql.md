---
title: Sys. pdw_health_alerts (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/03/2017
ms.prod: sql
ms.technology: system-objects
ms.reviewer: ''
ms.topic: conceptual
ms.assetid: 49c01e5f-ee47-41a0-871d-35a759f50851
author: ronortloff
ms.author: rortloff
monikerRange: '>= aps-pdw-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: c47bcc342bf8a052aed93649ca0ad8475d937608
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/27/2020
ms.locfileid: "68127539"
---
# <a name="syspdw_health_alerts-transact-sql"></a>Sys. pdw_health_alerts (Transact-SQL)
[!INCLUDE[tsql-appliesto-xxxxxx-xxxx-xxxx-pdw-md](../../includes/tsql-appliesto-xxxxxx-xxxx-xxxx-pdw-md.md)]

  Almacena las propiedades de las distintas alertas que se pueden producir en el sistema; se trata de una tabla de catálogo para las alertas.  
  
|Nombre de columna|Tipo de datos|Descripción|Intervalo|  
|-----------------|---------------|-----------------|-----------|  
|alert_id|**int**|Identificador único de la alerta.<br /><br /> Clave para esta vista.|NOT NULL|  
|component_id|**int**|IDENTIFICADOR del componente al que se aplica esta alerta. El componente es un identificador de componente general, como "fuente de alimentación", y no es específico de una instalación de. Vea [Sys. pdw_health_components &#40;&#41;de Transact-SQL ](../../relational-databases/system-catalog-views/sys-pdw-health-components-transact-sql.md).|NOT NULL|  
|alert_name|**nvarchar(255)**|Nombre de la alerta|NOT NULL|  
|state|**nvarchar(32)**|Estado de la alerta.|NOT NULL<br /><br /> Valores posibles:<br /><br /> Explotación<br /><br /> ' No operativo '<br /><br /> Degradado<br /><br /> Erróneo|  
|severity|**nvarchar(32)**|Gravedad de la alerta.|NOT NULL<br /><br /> Valores posibles:<br /><br /> Informativo<br /><br /> Atención<br /><br /> Error|  
|type|**nvarchar(32)**|Tipo de alerta.|NOT NULL<br /><br /> Valores posibles:<br /><br /> StatusChange: el estado del dispositivo ha cambiado.<br /><br /> Umbral: un valor ha superado el valor de umbral.|  
|description|**nvarchar(4000)**|Descripción de la alerta|NOT NULL|  
|condición|**nvarchar(255)**|Se usa cuando Type = THRESHOLD. Define cómo se calcula el umbral de alerta.|NULL|  
|status|**nvarchar(32)**|Estado de alerta|NULL|  
|condition_value|**bit**|Indica si la alerta puede producirse durante el funcionamiento del sistema.|NULL<br /><br /> Valores posibles<br /><br /> 0: no se genera la alerta.<br /><br /> 1: se genera la alerta.|  
  
## <a name="see-also"></a>Consulte también  
 [Vistas de catálogo de SQL Data Warehouse y Almacenamiento de datos paralelos](../../relational-databases/system-catalog-views/sql-data-warehouse-and-parallel-data-warehouse-catalog-views.md)  
  
  
