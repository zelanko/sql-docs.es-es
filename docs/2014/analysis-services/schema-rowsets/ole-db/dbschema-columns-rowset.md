---
title: Conjunto de filas DBSCHEMA_COLUMNS | Documentos de Microsoft
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: ''
ms.topic: reference
api_name:
- DBSCHEMA_COLUMNS
topic_type:
- apiref
helpviewer_keywords:
- DBSCHEMA_COLUMNS rowset
ms.assetid: 653bdd07-a533-4a99-8b6a-6e5c7322e1f3
caps.latest.revision: 40
author: Minewiskan
ms.author: owend
manager: mblythe
ms.openlocfilehash: 413e86e156db59e7621c94bdc1c99cd0087a987f
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/19/2018
ms.locfileid: "36196322"
---
# <a name="dbschemacolumns-rowset"></a>Conjunto de filas DBSCHEMA_COLUMNS
  Proporciona información de columna de todas las columnas que cumplen los criterios de restricción proporcionados.  
  
## <a name="rowset-columns"></a>Columnas del conjunto de filas  
 El `DBSCHEMA_COLUMNS` filas contiene las columnas siguientes.  
  
|Nombre de columna|Indicador de tipo|Longitud|Descripción|  
|-----------------|--------------------|------------|-----------------|  
|`TABLE_CATALOG`|`DBTYPE_WSTR`||Nombre de la base de datos.|  
|`TABLE_SCHEMA`|`DBTYPE_WSTR`||No compatible.|  
|`TABLE_NAME`|`DBTYPE_WSTR`||Nombre del cubo.|  
|`COLUMN_NAME`|`DBTYPE_WSTR`||Nombre de la medida o jerarquía de atributo.|  
|`COLUMN_GUID`|`DBTYPE_GUID`||No compatible.|  
|`COLUMN_PROPID`|`DBTYPE_UI4`||No compatible.|  
|`ORDINAL_POSITION`|`DBTYPE_UI4`||Posición de la columna, comenzando por 1.|  
|`COLUMN_HAS_DEFAULT`|`DBTYPE_BOOL`||No compatible.|  
|`COLUMN_DEFAULT`|`DBTYPE_WSTR`||No compatible.|  
|`COLUMN_FLAGS`|`DBTYPE_UI4`||Máscara de bits `DBCOLUMNFLAGS` que indica las propiedades de columna. Vea "Tipo enumerado DBCOLUMNFLAGS" en [IColumnsInfo:: GetColumnInfo](http://msdn2.microsoft.com/library/ms722704.aspx)|  
|`IS_NULLABLE`|`DBTYPE_BOOL`||Siempre devuelve `false`.|  
|`DATA_TYPE`|`DBTYPE_WSTR`<br /><br /> `DBTYPE_VARIANT`||Tipo de datos de la columna. Devuelve una cadena para las columnas de dimensión y una variante para las medidas.|  
|`TYPE_GUID`|`DBTYPE_GUID`||No compatible.|  
|`CHARACTER_MAXIMUM_LENGTH`|`DBTYPE_UI4`||Longitud máxima permitida para un valor incluido en la columna.<br /><br /> Este valor se recupera desde la propiedad `DataSize` en `DataItem`.|  
|`CHARACTER_OCTET_LENGTH`|`DBTYPE_UI4`||Longitud máxima permitida, en bytes, para un valor incluido en la columna; se aplica a columnas binarias o de caracteres.<br /><br /> Un valor de cero (0) indica que la columna no tiene una longitud máxima.<br /><br /> Se devolverá `NULL` para las columnas que no devuelven tipos de datos binarios o de caracteres.|  
|`NUMERIC_PRECISION`|`DBTYPE_UI2`||Precisión máxima de la columna para tipos de datos numéricos distintos de `DBTYPE_VARNUMERIC`.|  
|`NUMERIC_SCALE`|`DBTYPE_I2`||Número de dígitos que se encuentran a la derecha del separador decimal para `DBTYPE_DECIMAL`, `DBTYPE_NUMERIC`, `DBTYPE_VARNUMERIC`. De lo contrario, su valor es `NULL`.|  
|`DATETIME_PRECISION`|`DBTYPE_UI4`||No compatible.|  
|`CHARACTER_SET_CATALOG`|`DBTYPE_WSTR`||No compatible.|  
|`CHARACTER_SET_SCHEMA`|`DBTYPE_WSTR`||No compatible.|  
|`CHARACTER_SET_NAME`|`DBTYPE_WSTR`||No compatible.|  
|`COLLATION_CATALOG`|`DBTYPE_WSTR`||No compatible.|  
|`COLLATION_SCHEMA`|`DBTYPE_WSTR`||No compatible.|  
|`COLLATION_NAME`|`DBTYPE_WSTR`||No compatible.|  
|`DOMAIN_CATALOG`|`DBTYPE_WSTR`||No compatible.|  
|`DOMAIN_SCHEMA`|`DBTYPE_WSTR`||No compatible.|  
|`DOMAIN_NAME`|`DBTYPE_WSTR`||No compatible.|  
|`DESCRIPTION`|`DBTYPE_WSTR`||No compatible.|  
|`COLUMN_OLAP_TYPE`|`DBTYPE_WSTR`||Tipo OLAP del objeto.<br /><br /> `MEASURE` indica que el objeto es una medida.<br /><br /> `ATTRIBUTE` indica que el objeto es un atributo de dimensión.<br /><br /> `SCHEMA` indica que el objeto es una columna de un esquema.|  
  
 El conjunto de filas se ordena en `TABLE_CATALOG`, `TABLE_SCHEMA`, `TABLE_NAME`.  
  
## <a name="restriction-columns"></a>Columnas de restricción  
 El `DBSCHEMA_COLUMNS` se puede restringir el conjunto de filas en las columnas enumeradas en la tabla siguiente.  
  
|Nombre de columna|Indicador de tipo|Estado de restricción|  
|-----------------|--------------------|-----------------------|  
|`TABLE_CATALOG`|`DBTYPE_WSTR`|Opcional|  
|`TABLE_SCHEMA`|`DBTYPE_WSTR`|Opcional|  
|`TABLE_NAME`|`DBTYPE_WSTR`|Opcional|  
|`COLUMN_NAME`|`DBTYPE_WSTR`|Opcional|  
|`COLUMN_OLAP_TYPE`|`DBTYPE_WSTR`|Opcional|  
  
## <a name="see-also"></a>Vea también  
 [Conjuntos de filas de esquema OLE DB](ole-db-schema-rowsets.md)  
  
  