---
title: Conjunto de filas DISCOVER_STORAGE_TABLES | Documentos de Microsoft
ms.date: 05/03/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: schema-rowsets
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: b87759d736044febc89099d493fb357d7e5153b9
ms.sourcegitcommit: c12a7416d1996a3bcce3ebf4a3c9abe61b02fb9e
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/10/2018
---
# <a name="discoverstoragetables-rowset"></a>DISCOVER_STORAGE_TABLES, conjunto de filas
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]
  Permite al cliente determinar las tablas incluidas en una base de datos de Analysis Services que se ejecuta en modo Tabular o SharePoint.  
  
## <a name="rowset-columns"></a>Columnas del conjunto de filas  
 El conjunto de filas **DISCOVER_STORAGE_TABLES** contiene las siguientes columnas.  
  
|**Nombre de columna**|**Indicador de tipo**|**Longitud**|**Description**|  
|---------------------|------------------------|----------------|---------------------|  
|**DATABASE_NAME**|**DBTYPE_WSTR**||Especifica el nombre de la base de datos que contiene las tablas.<br /><br /> El conjunto de filas **DISCOVER_STORAGE_TABLES** puede restringirse mediante esta columna. Si esta columna no se utiliza para restringir el conjunto de filas, se utiliza la base de datos actual.|  
|**RESTRICCIONES OBLIGATORIAS CUBE_NAME**|**DBTYPE_WSTR**||Especifica el cubo o el modelo que contiene las tablas.<br /><br /> El conjunto de filas **DISCOVER_STORAGE_TABLES** puede restringirse mediante esta columna.|  
|**MEASURE_GROUP_NAME**|**DBTYPE_WSTR**||Nombre del grupo de medida.|  
|**PARTICIÓN**|**DBTYPE_WSTR**||Nombre de la partición.|  
|**DIMENSION_NAME**|**DBTYPE_WSTR**||Nombre de la dimensión.|  
|**TABLE_ID**|**DBTYPE_WSTR**||Identificador de la tabla que se utiliza para almacenar la tabla de atributos.|  
|**TABLE_PARTITIONS_COUNT**|**DBTYPE_ WSTR**||Recuento de particiones de la tabla.|  
|**HINT_TABLE_TYPE**|**DBTYPE_ WSTR**||Sugerencia del tipo de tabla.|  
|**ROWS_COUNT**|**DBTYPE_UI4**||Número de filas de la partición.|  
|**RIVIOLATION_COUNT**|**DBTYPE_UI4**||Número de filas con infracciones de integridad referencial.|  
  
## <a name="restriction-columns"></a>Columnas de restricción  
 El conjunto de filas **DISCOVER_STORAGE_TABLES** puede tener restricciones en las columnas que se muestran en la tabla siguiente.  
  
|**Nombre de columna**|**Indicador de tipo**|**Estado de restricción**|  
|---------------------|------------------------|---------------------------|  
|**DATABASE_NAME**|**DBTYPE_WSTR**|Opcional.|  
|**RESTRICCIONES OBLIGATORIAS CUBE_NAME**|**DBTYPE_WSTR**|Opcional.|  
|**MEASURE_GROUP_NAME**|**DBTYPE_WSTR**|Opcional|  
|**PARTICIÓN**|**DBTYPE_WSTR**|Opcional|  
  
## <a name="example"></a>Ejemplo  
 El ejemplo de código siguiente devuelve una lista de las tablas de almacenamiento y el número de filas de cada una, de la base de datos predeterminada en la conexión actual.  
  
```  
SELECT TABLE_ID, ROWS_COUNT  
FROM $system.DISCOVER_STORAGE_TABLES  
ORDER BY TABLE_ID DESC  
  
```  
  
## <a name="see-also"></a>Vea también  
 [Conjuntos de filas de esquema de Analysis Services](../../../analysis-services/schema-rowsets/analysis-services-schema-rowsets.md)  
  
  
