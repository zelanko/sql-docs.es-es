---
title: Conjunto de filas DISCOVER_STORAGE_TABLE_COLUMN_SEGMENTS | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: ''
ms.topic: reference
ms.assetid: 3e514715-9fe6-4e6a-accb-4149ffd7e0bf
caps.latest.revision: 13
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: ae9955e9f052e4be2317206d5618ccf9294232cb
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/02/2018
ms.locfileid: "37325025"
---
# <a name="discoverstoragetablecolumnsegments-rowset"></a>DISCOVER_STORAGE_TABLE_COLUMN_SEGMENTS, conjunto de filas
  Proporciona información en el nivel de columna y segmento acerca de las tablas de almacenamiento que usa una base de datos de Analysis Services que se ejecuta en modo tabular o de PowerPivot. Este conjunto de filas se utiliza principalmente para solucionar problemas y realizar análisis.  
  
 **Se aplica a:** modelos tabulares  
  
## <a name="rowset-columns"></a>Columnas del conjunto de filas  
 El `DISCOVER_STORAGE_TABLE_COLUMN_SEGMENTS` conjunto de filas contiene las siguientes columnas.  
  
|**Nombre de columna**|**Indicador de tipo**|**Restricción**|**Descripción**|  
|---------------------|------------------------|---------------------|---------------------|  
|`DATABASE_NAME`|`DBTYPE_WSTR`|Sí|Especifica la base de datos tabular.<br /><br /> El `DISCOVER_STORAGE_TABLE_COLUMN_SEGMENTS` conjunto de filas puede restringirse mediante esta columna. Si se omite, se utiliza la base de datos actual.|  
|`CUBE_NAME`|`DBTYPE_WSTR`|Sí|Nombre del modelo.<br /><br /> El `DISCOVER_STORAGE_TABLES` conjunto de filas puede restringirse mediante esta columna.|  
|`MEASURE_GROUP_NAME`|`DBTYPE_WSTR`|Sí|Nombre del grupo de medida.|  
|`PARTITION_NAME`|`DBTYPE_WSTR`|Sí|Nombre de la partición.|  
|`DIMENSION_NAME`|`DBTYPE_WSTR`||Nombre de la dimensión.|  
|`TABLE_ID`|`DBTYPE_WSTR`||Identificador interno del segmento de la tabla.|  
|`COLUMN_ID`|`DBTYPE_WSTR`||Identificador interno de la columna.|  
|`SEGMENT _NUMBER`|`DBTYPE_I8`||Número ordinal del segmento de la tabla.|  
|`TABLE_PARTTION_NUMBER`|`DBTYPE_I8`||Número ordinal de la partición.|  
|`RECORDS_COUNT`|`DBTYPE_I8`||Número de registros de la partición.|  
|`ALLOCATED_SIZE`|`DBTYPE_UI8`||Tamaño en bytes asignado al segmento de la columna.|  
|`USED_SIZE`|`DBTYPE_UI8`||Tamaño en bytes utilizados por el segmento de la columna.|  
|`COMPRESSION_TYPE`|`DBTYPE_WSTR`||Tipo de compresión aplicado al segmento de la columna. Este valor está pensado para uso interno y del servicio de soporte técnico solamente. Microsoft no publica valores válidos o descripciones para esta columna.|  
|`BITS_COUNT`|`DBTYPE_I8`||Recuento de bits.|  
|`BOOKMARK_BITS_COUNT`|`DBTYPE_I8`||Recuento de bits de marcador.|  
|`VERTIPAQ_STATE`|`DBTYPE_WSTR`||El estado de la compresión VertiPaq para este sector de la columna. El valor puede ser:<br /><br /> -SKIPPED: se omitió la compresión de VertiPaq.<br />-COMPLETAR: la compresión de VertiPaq se completó correctamente.<br />Compresión - TIMEBOXED: la VertiPaq era timeboxed.|  
  
## <a name="using-adomdnet-to-return-the-rowset"></a>Usar ADOMD.NET para devolver el conjunto de filas  
 Cuando se utilizan ADOMD.NET y el conjunto de filas de esquema para recuperar metadatos, puede utilizar el GUID o una cadena para hacer referencia a un objeto de conjunto de filas de esquema del método GetSchemaDataSet. Para obtener más información, vea [Working with Schema Rowsets in ADOMD.NET](../../../relational-databases/native-client-ole-db-rowsets/rowsets.md).  
  
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
 [Conjuntos de filas de esquema de Analysis Services](../analysis-services-schema-rowsets.md)  
  
  
