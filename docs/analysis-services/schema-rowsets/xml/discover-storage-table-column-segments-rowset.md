---
title: Conjunto de filas DISCOVER_STORAGE_TABLE_COLUMN_SEGMENTS | Documentos de Microsoft
ms.custom: 
ms.date: 03/04/2017
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: 
ms.component: 
ms.reviewer: 
ms.suite: pro-bi
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: reference
applies_to: SQL Server 2016 Preview
ms.assetid: 3e514715-9fe6-4e6a-accb-4149ffd7e0bf
caps.latest.revision: "15"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: 878568721816c90e202727dc3e516370f9c3ee56
ms.sourcegitcommit: f486d12078a45c87b0fcf52270b904ca7b0c7fc8
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 01/08/2018
---
# <a name="discoverstoragetablecolumnsegments-rowset"></a>DISCOVER_STORAGE_TABLE_COLUMN_SEGMENTS, conjunto de filas
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]Proporciona información en el nivel de columna y segmento acerca de las tablas de almacenamiento utilizado por una base de datos de Analysis Services que se ejecutan en tabular o [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] modo. Este conjunto de filas se utiliza principalmente para solucionar problemas y realizar análisis.  
  
 **Se aplica a:** modelos tabulares  
  
## <a name="rowset-columns"></a>Columnas del conjunto de filas  
 El conjunto de filas **DISCOVER_STORAGE_TABLE_COLUMN_SEGMENTS** contiene las siguientes columnas.  
  
|**Nombre de columna**|**Indicador de tipo**|**Restricción**|**Descripción**|  
|---------------------|------------------------|---------------------|---------------------|  
|**DATABASE_NAME**|**DBTYPE_WSTR**|Sí|Especifica la base de datos tabular.<br /><br /> El conjunto de filas **DISCOVER_STORAGE_TABLE_COLUMN_SEGMENTS** puede restringirse mediante esta columna. Si se omite, se utiliza la base de datos actual.|  
|**RESTRICCIONES OBLIGATORIAS CUBE_NAME**|**DBTYPE_WSTR**|Sí|Nombre del modelo.<br /><br /> El conjunto de filas **DISCOVER_STORAGE_TABLES** puede restringirse mediante esta columna.|  
|**MEASURE_GROUP_NAME**|**DBTYPE_WSTR**|Sí|Nombre del grupo de medida.|  
|**PARTICIÓN**|**DBTYPE_WSTR**|Sí|Nombre de la partición.|  
|**DIMENSION_NAME**|**DBTYPE_WSTR**||Nombre de la dimensión.|  
|**TABLE_ID**|**DBTYPE_WSTR**||Identificador interno del segmento de la tabla.|  
|**COLUMN_ID**|**DBTYPE_WSTR**||Identificador interno de la columna.|  
|**_NÚMERO DE SEGMENTO**|**DBTYPE_I8**||Número ordinal del segmento de la tabla.|  
|**TABLE_PARTTION_NUMBER**|**DBTYPE_I8**||Número ordinal de la partición.|  
|**RECORDS_COUNT**|**DBTYPE_I8**||Número de registros de la partición.|  
|**ALLOCATED_SIZE**|**DBTYPE_UI8**||Tamaño en bytes asignado al segmento de la columna.|  
|**USED_SIZE**|**DBTYPE_UI8**||Tamaño en bytes utilizados por el segmento de la columna.|  
|**COMPRESSION_TYPE**|**DBTYPE_WSTR**||Tipo de compresión aplicado al segmento de la columna. Este valor está pensado para uso interno y del servicio de soporte técnico solamente. Microsoft no publica valores válidos o descripciones para esta columna.|  
|**BITS_COUNT**|**DBTYPE_I8**||Recuento de bits.|  
|**BOOKMARK_BITS_COUNT**|**DBTYPE_I8**||Recuento de bits de marcador.|  
|**VERTIPAQ_STATE**|**DBTYPE_WSTR**||El estado de la compresión VertiPaq para este sector de la columna. El valor puede ser:<br /><br /> SKIPPED: se omitió la compresión VertiPaq.<br /><br /> COMPLETED: la compresión VertiPaq se completó correctamente.<br /><br /> TIMEBOXED: la compresión VertiPaq se ha delimitado a un periodo de tiempo.|  
  
## <a name="using-adomdnet-to-return-the-rowset"></a>Usar ADOMD.NET para devolver el conjunto de filas  
 Cuando se utilizan ADOMD.NET y el conjunto de filas de esquema para recuperar metadatos, puede utilizar el GUID o una cadena para hacer referencia a un objeto de conjunto de filas de esquema del método GetSchemaDataSet. Para obtener más información, vea [Working with Schema Rowsets in ADOMD.NET](../../../analysis-services/multidimensional-models-adomd-net-client/retrieving-metadata-working-with-schema-rowsets.md).  
  
 La tabla siguiente proporciona el GUID y los valores de cadena que identifican este conjunto de filas.  
  
|Argumento|Valor|  
|--------------|-----------|  
|GUID|a07ccd45-8148-11d0-87bb-00c04fc33942|  
|ADOMDNAME|StorageSegments|  
  
## <a name="example"></a>Ejemplo  
 La consulta siguiente devuelve los segmentos de la tabla de almacenamiento asociados con el atributo de modelo LastName de la base de datos actual.  
  
```  
SELECT DISTINCT TABLE_ID, COLUMN_ID   
FROM $system.DISCOVER_STORAGE_TABLE_COLUMN_SEGMENTS  
WHERE COLUMN_ID = 'LastName'  
ORDER BY TABLE_ID  
  
```  
  
## <a name="see-also"></a>Vea también  
 [Conjuntos de filas de esquema de Analysis Services](../../../analysis-services/schema-rowsets/analysis-services-schema-rowsets.md)  
  
  
