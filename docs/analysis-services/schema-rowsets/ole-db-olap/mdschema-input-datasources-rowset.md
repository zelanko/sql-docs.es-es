---
title: Conjunto de filas MDSCHEMA_INPUT_DATASOURCES | Documentos de Microsoft
ms.date: 05/03/2018
ms.prod: sql
ms.technology: analysis-services
ms.component: schema-rowsets
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 6efa6baf40c41db7de09ebcb4e5c44990ff7e6ed
ms.sourcegitcommit: f1caaa156db2b16e817e0a3884394e7b30fb642f
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/04/2018
---
# <a name="mdschemainputdatasources-rowset"></a>Conjunto de filas MDSCHEMA_INPUT_DATASOURCES
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]
  Describe los orígenes de datos definidos dentro de la base de datos.  
  
## <a name="rowset-columns"></a>Columnas del conjunto de filas  
 El conjunto de filas **MDSCHEMA_INPUT_DATASOURCES** contiene las siguientes columnas.  
  
|Nombre de columna|Indicador de tipo|Longitud|Description|  
|-----------------|--------------------|------------|-----------------|  
|**CATALOG_NAME**|**DBTYPE_WSTR**||El nombre del catálogo al que pertenece este origen de datos.|  
|**SCHEMA_NAME**|**DBTYPE_WSTR**||No compatible.|  
|**DATASOURCE_NAME**|**DBTYPE_WSTR**||El nombre del objeto de origen de datos.|  
|**DATASOURCE_TYPE**|**DBTYPE_WSTR**||Tipo del origen de datos. Los valores válidos incluyen:<br /><br /> **Relacional**<br /><br /> **OLAP**|  
|**CREATED_ON**|**DBTYPE_DBTIMESTAMP**||Fecha de creación del origen de datos.|  
|**LAST_SCHEMA_UPDATE**|**DBTYPE_DBTIMESTAMP**||Fecha y hora de la última modificación del origen de datos.|  
|**DESCRIPTION**|**DBTYPE_WSTR**||Descripción fácil de comprender de la acción.|  
|**TIEMPO DE ESPERA**|**DBTYPE_UI4**||Tiempo de espera del origen de datos.|  
  
 Este conjunto de filas de esquema no está ordenado.  
  
## <a name="restriction-columns"></a>Columnas de restricción  
 El conjunto de filas **MDSCHEMA_INPUT_DATASOURCES** puede tener restricciones en las columnas que se muestran en la tabla siguiente.  
  
|Nombre de columna|Indicador de tipo|Estado de restricción|  
|-----------------|--------------------|-----------------------|  
|**CATALOG_NAME**|**DBTYPE_WSTR**|Opcional.|  
|**SCHEMA_NAME**|**DBTYPE_WSTR**|Opcional.|  
|**DATASOURCE_NAME**|**DBTYPE_WSTR**|Opcional.|  
|**DATASOURCE_TYPE**|**DBTYPE_WSTR**|Opcional.|  
  
## <a name="see-also"></a>Vea también  
 [OLE DB para OLAP Schema Rowsets](../../../analysis-services/schema-rowsets/ole-db-olap/ole-db-for-olap-schema-rowsets.md)  
  
  
