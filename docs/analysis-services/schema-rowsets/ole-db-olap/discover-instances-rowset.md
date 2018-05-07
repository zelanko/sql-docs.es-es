---
title: Conjunto de filas DISCOVER_INSTANCES | Documentos de Microsoft
ms.date: 05/03/2018
ms.prod: sql
ms.technology: analysis-services
ms.component: schema-rowsets
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 4143aa33cc4c09914ffb05aaccbb12f2fe64d440
ms.sourcegitcommit: f1caaa156db2b16e817e0a3884394e7b30fb642f
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/04/2018
---
# <a name="discoverinstances-rowset"></a>Conjunto de filas DISCOVER_INSTANCES
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]
  Describe las instancias en el servidor.  
  
## <a name="rowset-columns"></a>Columnas del conjunto de filas  
 El conjunto de filas **DISCOVER_INSTANCES** contiene las siguientes columnas.  
  
|Nombre de columna|Indicador de tipo|Longitud|Description|  
|-----------------|--------------------|------------|-----------------|  
|**INSTANCE_NAME**|**DBTYPE_WSTR**||Nombre de la instancia.|  
|**INSTANCE_PORT_NUMBER**|**DBTYPE_I4**||El número de puerto en que escucha la instancia.|  
|**INSTANCE_STATE**|**DBTYPE_I4**||Estado de instancia del servidor:<br /><br /> **Se inició**<br /><br /> **Detenido**<br /><br /> **A partir de**<br /><br /> **Detener**<br /><br /> **En pausa**|  
  
 Este conjunto de filas de esquema no está ordenado.  
  
## <a name="restriction-columns"></a>Columnas de restricción  
 El conjunto de filas **DISCOVER_INSTANCES** puede tener restricciones en las columnas que se muestran en la tabla siguiente.  
  
|Nombre de columna|Indicador de tipo|Estado de restricción|  
|-----------------|--------------------|-----------------------|  
|**INSTANCE_NAME**|**DBTYPE_WSTR**|Opcional.|  
  
## <a name="see-also"></a>Vea también  
 [OLE DB para OLAP Schema Rowsets](../../../analysis-services/schema-rowsets/ole-db-olap/ole-db-for-olap-schema-rowsets.md)  
  
  
