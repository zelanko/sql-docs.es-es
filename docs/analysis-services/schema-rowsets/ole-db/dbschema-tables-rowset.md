---
title: Conjunto de filas DBSCHEMA_TABLES | Documentos de Microsoft
ms.date: 05/03/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: schema-rowsets
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 06fc718e4d4bde23bfee4240e89d77bcde3bbf50
ms.sourcegitcommit: c12a7416d1996a3bcce3ebf4a3c9abe61b02fb9e
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/10/2018
ms.locfileid: "34032066"
---
# <a name="dbschematables-rowset"></a>Conjunto de filas DBSCHEMA_TABLES
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]
  Identifica los grupos de medida y dimensiones expuestos como tablas dentro de [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)].  
  
## <a name="rowset-columns"></a>Columnas del conjunto de filas  
 El **DBSCHEMA_TABLES** filas contiene las columnas siguientes.  
  
|Nombre de columna|Indicador de tipo|Longitud|Description|  
|-----------------|--------------------|------------|-----------------|  
|**TABLE_CATALOG**|**DBTYPE_WSTR**|255|El nombre del catálogo al que pertenece este objeto.|  
|**TABLE_SCHEMA**|**DBTYPE_WSTR**|255|Nombre del cubo al que pertenece este objeto.|  
|**TABLE_NAME**|**DBTYPE_WSTR**|255|El nombre del objeto, si **TABLE_TYPE** es **tabla**.|  
|**TABLE_TYPE**|**DBTYPE_WSTR**||El tipo de la tabla.<br /><br /> **TABLA** indica el objeto es un grupo de medida.<br /><br /> **TABLA del sistema** indica que el objeto es una dimensión.|  
|**TABLE_GUID**|**DBTYPE_GUID**||No compatible.|  
|**DESCRIPTION**|**DBTYPE_WSTR**||Descripción legible del objeto.|  
|**TABLE_PROPID**|**DBTYPE_UI4**||No compatible.|  
|**DATE_CREATED**|**DBTYPE_DBTIMESTAMP**||No compatible.|  
|**DATE_MODIFIED**|**DBTYPE_DBTIMESTAMP**||Fecha de la última modificación del objeto.|  
|**TABLE_OLAP_TYPE**|**DBTYPE_WSTR**||Tipo OLAP del objeto.<br /><br /> **MEASURE_GROUP** indica que el objeto es un grupo de medida.<br /><br /> **CUBE_DIMENSION** indica que el objeto es una dimensión.|  
  
 El conjunto de filas está ordenado en **TABLE_TYPE**, **TABLE_CATALOG**, **TABLE_SCHEMA**, y **TABLE_NAME**.  
  
## <a name="restriction-columns"></a>Columnas de restricción  
 El **DBSCHEMA_TABLES** se puede restringir el conjunto de filas en las columnas enumeradas en la tabla siguiente.  
  
|Nombre de columna|Indicador de tipo|Estado de restricción|  
|-----------------|--------------------|-----------------------|  
|**TABLE_CATALOG**|**DBTYPE_WSTR**|Opcional|  
|**TABLE_SCHEMA**|**DBTYPE_WSTR**|Opcional|  
|**TABLE_NAME**|**DBTYPE_WSTR**|Opcional|  
|**TABLE_TYPE**|**DBTYPE_WSTR**|Opcional|  
|**TABLE_OLAP_TYPE**|**DBTYPE_WSTR**|Opcional|  
  
## <a name="see-also"></a>Vea también  
 [Conjuntos de filas de esquema OLE DB](../../../analysis-services/schema-rowsets/ole-db/ole-db-schema-rowsets.md)  
  
  
