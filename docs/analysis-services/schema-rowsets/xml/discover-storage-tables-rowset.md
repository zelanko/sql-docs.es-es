---
title: Conjunto de filas DISCOVER_STORAGE_TABLES | Documentos de Microsoft
ms.custom: ''
ms.date: 03/06/2017
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: ''
ms.component: ''
ms.reviewer: ''
ms.suite: pro-bi
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: reference
applies_to:
- SQL Server 2016 Preview
ms.assetid: 13df6f10-8efe-4fe9-83a6-96d108809ed1
caps.latest.revision: 13
author: Minewiskan
ms.author: owend
manager: kfile
ms.openlocfilehash: 2bfa54e95a97aeb8bd79b9551da461473c4be980
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 05/03/2018
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
  
  
