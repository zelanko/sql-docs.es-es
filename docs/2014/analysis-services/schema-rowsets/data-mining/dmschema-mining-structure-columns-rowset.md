---
title: Conjunto de filas DMSCHEMA_MINING_STRUCTURE_COLUMNS | Documentos de Microsoft
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
api_name:
- DMSCHEMA_MINING_STRUCTURE_COLUMNS
topic_type:
- apiref
helpviewer_keywords:
- DMSCHEMA_MINING_STRUCTURE_COLUMNS rowset
ms.assetid: 81f25502-ac90-42f1-8ddf-7b0f9752ebfd
caps.latest.revision: 34
author: Minewiskan
ms.author: owend
manager: mblythe
ms.openlocfilehash: 98c8ec286e12cfe6198c36900067a26eefd5e1ad
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/19/2018
ms.locfileid: "36107509"
---
# <a name="dmschemaminingstructurecolumns-rowset"></a>Conjunto de filas DMSCHEMA_MINING_STRUCTURE_COLUMNS
  Describe las columnas individuales de todas las estructuras de minería de datos implementadas en un servidor que ejecuta [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)].  
  
## <a name="rowset-columns"></a>Columnas del conjunto de filas  
 El `DMSCHEMA_MINING_STRUCTURE_COLUMNS` filas contiene las columnas siguientes.  
  
|Nombre de columna|Indicador de tipo|Longitud|Descripción|  
|-----------------|--------------------|------------|-----------------|  
|`STRUCTURE_CATALOG`|`DBTYPE_WSTR`||Nombre del catálogo.|  
|`STRUCTURE_SCHEMA`|`DBTYPE_WSTR`||Nombre del esquema sin certificar. [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] no admite los esquemas, por lo que esta columna siempre es `NULL`.|  
|`STRUCTURE_NAME`|`DBTYPE_WSTR`||Nombre de la estructura. Esta columna no puede contener una `NULL`.|  
|`COLUMN_NAME`|`DBTYPE_WSTR`||Nombre de la columna. La unicidad solamente se garantiza entre las columnas que comparten el mismo patrón. Por ejemplo, dos columnas anidadas pueden tener el mismo nombre si pertenecen a dos tablas anidadas distintas dentro de la misma estructura.|  
|`COLUMN_GUID`|`DBTYPE_GUID`||GUID de la columna. Los proveedores que no utilizan identificadores GUID para identificar las columnas, deben devolver `NULL` en esta columna.|  
|`COLUMN_PROPID`|`DBTYPE_UI4`||Identificador de propiedad de la columna. Los proveedores que no asocian identificadores de propiedad a las columnas deben devolver `NULL` en esta columna. [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] Devuelve `NULL` para esta columna.|  
|`ORDINAL_POSITION`|`DBTYPE_UI4`||El ordinal de la columna. Las columnas se numeran a partir de 1. Su valor es `NULL` si no hay un valor ordinal estable para la columna.|  
|`COLUMN_HASDEFAULT`|`DBTYPE_BOOL`||Valor booleano que indica si esta columna tiene un valor predeterminado.<br /><br /> `TRUE` si la columna tiene un valor predeterminado.<br /><br /> `FALSE` si la columna no tiene un valor predeterminado o si no se sabe si lo tiene.|  
|`COLUMN_DEFAULT`|`DBTYPE_WSTR`||El valor predeterminado de la columna. Un proveedor puede exponer `DBCOLUMN_DEFAULTVALUE` pero no `DBCOLUMN_HASDEFAULT` (para tablas ISO) en el conjunto de filas devuelto por `IColumnsRowset::GetColumnsRowset`.<br /><br /> Si el valor predeterminado es `NULL`, `COLUMN_HASDEFAULT` es `TRUE` y la columna `COLUMN_DEFAULT` tiene un valor `NULL`.|  
|`COLUMN_FLAGS`|`DBTYPE_UI4`||-Una máscara de bits que describe las características de la columna. El tipo enumerado `DBCOLUMNFLAGS` especifica los bits de la máscara de bits. Esta columna no puede contener un valor `NULL`. Los valores válidos incluyen:<br />-   **DBCOLUMNFLAGS_ISNULLABLE** (`0x20`)<br />-   **DBCOLUMNFLAGS_MAYBENULL** (`0x40`)<br />-   **DBCOLUMNFLAGS_ISLONG** (`0x80`)|  
|`IS_NULLABLE`|`DBTYPE_BOOL`||Valor booleano que indica si esta columna tiene un valor predeterminado.<br /><br /> `TRUE` si la columna puede contener un valor `NULL`; de lo contrario, `FALSE`.|  
|`DATA_TYPE`|`DBTYPE_UI2`||Indicador del tipo de datos de la columna. Por ejemplo:<br /><br /> -   "`TABLE`" = `DBTYPE_HCHAPTER`<br />-   "`TEXT`" = `DBTYPE_WCHAR`<br />-   "`LONG`" = `DBTYPE_I8`<br />-   "`DOUBLE`" = `DBTYPE_R8`<br />-   "`DATE`" = `DBTYPE_DATE`|  
|`TYPE_GUID`|`DBTYPE_GUID`||GUID del tipo de datos de la columna. Los proveedores que no utilizan identificadores GUID para identificar los tipos de datos deben devolver `NULL` en esta columna.|  
|`CHARACTER_MAXIMUM_LENGTH`|`DBTYPE_UI4`||Longitud máxima permitida para un valor de la columna. Para las columnas de caracteres, binarias o de tipo bit, es uno de los valores siguientes:<br /><br /> -La longitud máxima de la columna en caracteres, bytes o bits, respectivamente, si se define la longitud. Por ejemplo, una columna `CHAR(5)` de una tabla SQL tiene una longitud máxima de 5.<br />-La longitud máxima de los datos de tipo en caracteres, bytes o bits, respectivamente, si la columna no tiene una longitud definida.<br />-Cero (0) si la columna ni el tipo de datos tiene una longitud máxima definida.<br />-   `NULL` para los demás tipos de columnas.|  
|`CHARACTER_OCTET_LENGTH`|`DBTYPE_UI4`||Longitud máxima de la columna en octetos (bytes), si la columna es de caracteres o binaria. Un valor cero (0) significa que la columna no tiene una longitud máxima. `NULL` para los demás tipos de columnas.|  
|`NUMERIC_PRECISION`|`DBTYPE_UI2`||Precisión máxima de la columna si el tipo de datos de la columna es un tipo de datos numérico distinto de `VARNUMERIC`; `NULL` si el tipo de datos de la columna no es numérico o es `VARNUMERIC`.<br /><br /> La precisión de las columnas con un tipo de datos `DBTYPE_DECIMAL` or `DBTYPE_NUM`ERIC depende de la definición de la columna.|  
|`NUMERIC_SCALE`|`DBTYPE_I2`||Número de dígitos que se encuentran a la derecha del separador decimal si el indicador de tipo de la columna es `DBTYPE_DECIMAL`, `DBTYPE_NUMERIC` o `DBTYPE_VARNUMERIC`. De lo contrario, su valor es `NULL`.|  
|`DATETIME_PRECISION`|`DBTYPE_UI4`||Precisión DateTime (número de dígitos en la parte que indica las fracciones de segundo) de la columna si ésta es de tipo de fecha y hora o de intervalo. Si el tipo de datos de la columna no es de fecha y hora, este valor es `NULL`.|  
|`CHARACTER_SET_CATALOG`|`DBTYPE_WSTR`||Nombre del catálogo en el que está definido el juego de caracteres. Si el proveedor no admite catálogos o distintos juegos de caracteres, su valor es `NULL`.|  
|`CHARACTER_SET_SCHEMA`|`DBTYPE_WSTR`||Nombre del esquema no calificado en el que se define el juego de caracteres. Si el proveedor no admite esquemas o distintos juegos de caracteres, su valor es `NULL`.|  
|`CHARACTER_SET_NAME`|`DBTYPE_WSTR`||El juego de caracteres nombre. Si el proveedor no admite distintos juegos de caracteres, su valor es `NULL`.|  
|`COLLATION_CATALOG`|`DBTYPE_WSTR`||Nombre del catálogo en el que está definida la intercalación. Si el proveedor no admite catálogos o intercalaciones diferentes, su valor es `NULL`.|  
|`COLLATION_SCHEMA`|`DBTYPE_WSTR`||Nombre del esquema no calificado en el que se define la intercalación. Si el proveedor no admite esquemas o intercalaciones diferentes, su valor es `NULL`.|  
|`COLLATION_NAME`|`DBTYPE_WSTR`||Nombre de intercalación. Si el proveedor no admite intercalaciones diferentes, su valor es `NULL`.|  
|`DOMAIN_CATALOG`|`DBTYPE_WSTR`||Nombre del catálogo en el que está definido el dominio. Si el proveedor no admite catálogos o dominios, su valor es `NULL`.|  
|`DOMAIN_SCHEMA`|`DBTYPE_WSTR`||Nombre del esquema sin certificar en el que está definido el dominio. Si el proveedor no admite esquemas o dominios, su valor es `NULL`.|  
|`DOMAIN_NAME`|`DBTYPE_WSTR`||Nombre del dominio. Si el proveedor no admite dominios, su valor es `NULL`.|  
|`DESCRIPTION`|`DBTYPE_WSTR`||Descripción de la columna en lenguaje natural. Si no hay ninguna descripción asociada a la columna, su valor es `NULL`.|  
|`DISTRIBUTION_FLAG`|`DBTYPE_WSTR`||Distribución de la columna de estructura de minería de datos:<br /><br /> -   "`NORMAL`"<br />-"`LOG_NORM`AL"<br />-   "`UNIFORM`"|  
|`CONTENT_TYPE`|`DBTYPE_WSTR`||Tipo de contenido de la columna de estructura de minería de datos:<br /><br /> -   "`KEY`"<br />-   "`DISCRETE`"<br />-   "`CONTINUOUS`"<br />-"`DISCRETIZED(`[args]`)`"<br />-   "`ORDERED`"<br />-   "`SEQUENCE_TIME`"<br />-   "`CYCLICAL`"<br />-   "`PROBABILITY`"<br />-   "`VARIANCE`"<br />-   "`STDEV`"<br />-   "`SUPPORT`"<br />-   "`PROBABILITY_VARIANCE`"<br />-   "`PROBABILITY_STDEV`"|  
|`MODELING_FLAG`|`DBTYPE_WSTR`||Lista delimitada por comas de marcas de modelado. La única marca admitida para una columna de estructura es "`NOT NULL`".|  
|`IS_RELATED_TO_KEY`|`DBTYPE_BOOL`||Valor booleano que indica si esta columna está relacionada con la clave.<br /><br /> Su valor es `VARIANT_TRUE` si la columna está relacionada con la clave; de lo contrario, `VARIANT_FALSE`. Si la clave es una columna única, el campo `RELATED_ATTRIBUTE` puede contener su nombre de columna opcionalmente.|  
|`RELATED_ATTRIBUTE`|`DBTYPE_WSTR`||Nombre de la columna de destino con la que se relaciona la columna actual o de la que es una propiedad especial.|  
|`CONTAINING_COLUMN`|`DBTYPE_WSTR`||El nombre de la `TABLE` columna que contiene esta columna. Si ninguna tabla contiene la columna, su valor es `NULL`.|  
|`IS_POPULATED`|`DBTYPE_BOOL`||Valor booleano que indica si esta columna ha obtenido información sobre un conjunto de valores posibles.<br /><br /> Su valor es `TRUE` si la columna ha obtenido información sobre un conjunto de valores posibles; de lo contrario, `FALSE`.|  
  
## <a name="restriction-columns"></a>Columnas de restricción  
 El `DMSCHEMA_MINING_STRUCTURE_COLUMNS` se puede restringir el conjunto de filas en las columnas de la tabla siguiente.  
  
|Nombre de columna|Indicador de tipo|Estado de restricción|  
|-----------------|--------------------|-----------------------|  
|`STRUCTURE_CATALOG`|`DBTYPE_WSTR`|Opcional.|  
|`STRUCTURE_SCHEMA`|`DBTYPE_WSTR`|Opcional.|  
|`STRUCTURE_NAME`|`DBTYPE_WSTR`|Opcional.|  
|`COLUMN_NAME`|`DBTYPE_WSTR`|Opcional.|  
  
## <a name="see-also"></a>Vea también  
 [Conjuntos de filas de esquema de minería de datos](../../schema-rowsets/data-mining/data-mining-schema-rowsets.md) 
  
  