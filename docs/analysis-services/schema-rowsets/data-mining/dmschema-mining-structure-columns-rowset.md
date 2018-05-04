---
title: Conjunto de filas DMSCHEMA_MINING_STRUCTURE_COLUMNS | Documentos de Microsoft
ms.custom: ''
ms.date: 03/14/2017
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: ''
ms.component: data-mining
ms.reviewer: ''
ms.suite: pro-bi
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: reference
apiname:
- DMSCHEMA_MINING_STRUCTURE_COLUMNS
apitype: NA
applies_to:
- SQL Server 2016 Preview
helpviewer_keywords:
- DMSCHEMA_MINING_STRUCTURE_COLUMNS rowset
ms.assetid: 81f25502-ac90-42f1-8ddf-7b0f9752ebfd
caps.latest.revision: 35
author: Minewiskan
ms.author: owend
manager: kfile
ms.openlocfilehash: bbfd30d94a7f6ad129eee3ee82e9bb7fb951c19f
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 05/03/2018
---
# <a name="dmschemaminingstructurecolumns-rowset"></a>Conjunto de filas DMSCHEMA_MINING_STRUCTURE_COLUMNS
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]
  Describe las columnas individuales de todas las estructuras de minería de datos implementadas en un servidor que ejecuta [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)].  
  
## <a name="rowset-columns"></a>Columnas del conjunto de filas  
 El **DMSCHEMA_MINING_STRUCTURE_COLUMNS** filas contiene las columnas siguientes.  
  
|Nombre de columna|Indicador de tipo|Longitud|Description|  
|-----------------|--------------------|------------|-----------------|  
|**STRUCTURE_CATALOG**|**DBTYPE_WSTR**||Nombre del catálogo.|  
|**STRUCTURE_SCHEMA**|**DBTYPE_WSTR**||Nombre del esquema sin certificar. [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] no admite los esquemas, por lo que esta columna es siempre **NULL**.|  
|**NOMBRE_ESTRUCTURA**|**DBTYPE_WSTR**||Nombre de la estructura. Esta columna no puede contener una **NULL**.|  
|**COLUMN_NAME**|**DBTYPE_WSTR**||Nombre de la columna. La unicidad solamente se garantiza entre las columnas que comparten el mismo patrón. Por ejemplo, dos columnas anidadas pueden tener el mismo nombre si pertenecen a dos tablas anidadas distintas dentro de la misma estructura.|  
|**COLUMN_GUID**|**DBTYPE_GUID**||GUID de la columna. Los proveedores que no utilizan GUID para identificar las columnas deben devolver **NULL** en esta columna.|  
|**COLUMN_PROPID**|**DBTYPE_UI4**||Identificador de propiedad de la columna. Los proveedores que no asocian identificadores de propiedad a las columnas deben devolver **NULL** en esta columna. [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] Devuelve **NULL** para esta columna.|  
|**ORDINAL_POSITION**|**DBTYPE_UI4**||El ordinal de la columna. Las columnas se numeran a partir de 1. **NULL** si no hay ningún valor ordinal estable para la columna.|  
|**COLUMN_HASDEFAULT**|**DBTYPE_BOOL**||Valor booleano que indica si esta columna tiene un valor predeterminado.<br /><br /> **TRUE** si la columna tiene un valor predeterminado.<br /><br /> **FALSE** si la columna no tiene un valor predeterminado o si no se sabe si la columna tiene un valor predeterminado.|  
|**COLUMN_DEFAULT**|**DBTYPE_WSTR**||El valor predeterminado de la columna. Un proveedor puede exponer **DBCOLUMN_DEFAULTVALUE** pero no **DBCOLUMN_HASDEFAULT** (para tablas ISO) en el conjunto de filas devuelto por **IColumnsRowset:: GetColumnsRowset**.<br /><br /> Si el valor predeterminado es **NULL**, **COLUMN_HASDEFAULT** es **TRUE** y **COLUMN_DEFAULT** columna es un **NULL** valor.|  
|**COLUMN_FLAGS**|**DBTYPE_UI4**||Máscara de bits que describe características de columna. El **DBCOLUMNFLAGS** tipo enumerado especifica los bits de la máscara de bits. Esta columna no puede contener una **NULL** valor. Los valores válidos incluyen:<br /><br /> **DBCOLUMNFLAGS_ISNULLABLE** (**0 x 20**)<br /><br /> **DBCOLUMNFLAGS_MAYBENULL** (**0 x 40**)<br /><br /> **DBCOLUMNFLAGS_ISLONG** (**0 x 80**)|  
|**IS_NULLABLE**|**DBTYPE_BOOL**||Valor booleano que indica si esta columna tiene un valor predeterminado.<br /><br /> **TRUE** si la columna puede contener **NULL**; **FALSE**, en caso contrario.|  
|**DATA_TYPE**|**DBTYPE_UI2**||Indicador del tipo de datos de la columna. Por ejemplo:<br /><br /> "**TABLA**" = **DBTYPE_HCHAPTER**<br /><br /> "**TEXTO**" = **DBTYPE_WCHAR**<br /><br /> "**LARGO**" = **DBTYPE_I8**<br /><br /> "**DOBLE**" = **DBTYPE_R8**<br /><br /> "**FECHA**" = **DBTYPE_DATE**|  
|**TYPE_GUID**|**DBTYPE_GUID**||GUID del tipo de datos de la columna. Los proveedores que no utilizan GUID para identificar los tipos de datos deben devolver **NULL** en esta columna.|  
|**CAMPO CHARACTER_MAXIMUM_LENGTH**|**DBTYPE_UI4**||Longitud máxima permitida para un valor de la columna. Para las columnas de caracteres, binarias o de tipo bit, es uno de los valores siguientes:<br /><br /> La longitud máxima de la columna en caracteres, bytes o bits, respectivamente, si se define la longitud. Por ejemplo, una columna `CHAR(5)` de una tabla SQL tiene una longitud máxima de 5.<br /><br /> La longitud máxima del tipo de datos en caracteres, bytes o bits, respectivamente, si la columna no tiene una longitud definida.<br /><br /> Cero (0) si la columna y el tipo de datos no tienen una longitud máxima definida.<br /><br /> **NULL** para todos los demás tipos de columnas.|  
|**CHARACTER_OCTET_LENGTH**|**DBTYPE_UI4**||Longitud máxima de la columna en octetos (bytes), si la columna es de caracteres o binaria. Un valor cero (0) significa que la columna no tiene una longitud máxima. **NULL** para todos los demás tipos de columnas.|  
|**CAMPO NUMERIC_PRECISION**|**DBTYPE_UI2**||La precisión máxima de la columna si el tipo de datos de la columna es un tipo de datos numérico distinto de **VARNUMERIC**; **NULL** si el tipo de datos de la columna no es numérico o es **VARNUMERIC**.<br /><br /> La precisión de las columnas con un tipo de datos de **DBTYPE_DECIMAL** o **DBTYPE_NUM**ERIC depende de la definición de la columna.|  
|**NUMERIC_SCALE**|**DBTYPE_I2**||El número de dígitos a la derecha del separador decimal si el indicador de tipo de la columna es **DBTYPE_DECIMAL**, **DBTYPE_NUMERIC**, o **DBTYPE_VARNUMERIC**. De lo contrario, es **NULL**.|  
|**DATETIME_PRECISION**|**DBTYPE_UI4**||Precisión DateTime (número de dígitos en la parte que indica las fracciones de segundo) de la columna si ésta es de tipo de fecha y hora o de intervalo. Si el tipo de datos de la columna no es datetime, se trata de **NULL**.|  
|**CHARACTER_SET_CATALOG**|**DBTYPE_WSTR**||Nombre del catálogo en el que está definido el juego de caracteres. **NULL** si el proveedor no admite catálogos o distintos juegos de caracteres.|  
|**CHARACTER_SET_SCHEMA**|**DBTYPE_WSTR**||Nombre del esquema no calificado en el que se define el juego de caracteres. **NULL** si el proveedor no admite esquemas o distintos juegos de caracteres.|  
|**CHARACTER_SET_NAME**|**DBTYPE_WSTR**||El juego de caracteres nombre. **NULL** si el proveedor no admite distintos juegos de caracteres.|  
|**COLLATION_CATALOG**|**DBTYPE_WSTR**||Nombre del catálogo en el que está definida la intercalación. **NULL** si el proveedor no admite catálogos o intercalaciones diferentes.|  
|**COLLATION_SCHEMA**|**DBTYPE_WSTR**||Nombre del esquema no calificado en el que se define la intercalación. **NULL** si el proveedor no admite esquemas o intercalaciones diferentes.|  
|**COLLATION_NAME**|**DBTYPE_WSTR**||Nombre de intercalación. **NULL** si el proveedor no admite intercalaciones diferentes.|  
|**DOMAIN_CATALOG**|**DBTYPE_WSTR**||Nombre del catálogo en el que está definido el dominio. **NULL** si el proveedor no admite catálogos o dominios.|  
|**DOMAIN_SCHEMA**|**DBTYPE_WSTR**||Nombre del esquema sin certificar en el que está definido el dominio. **NULL** si el proveedor no admite esquemas o dominios.|  
|**NOMBRE_DOMINIO**|**DBTYPE_WSTR**||Nombre del dominio. **NULL** si el proveedor no admite dominios.|  
|**DESCRIPTION**|**DBTYPE_WSTR**||Descripción de la columna en lenguaje natural. **NULL** si no hay ninguna descripción asociada a la columna.|  
|**DISTRIBUTION_FLAG ES**|**DBTYPE_WSTR**||Distribución de la columna de estructura de minería de datos:<br /><br /> "**NORMAL**"<br /><br /> "**LOG_NORM**AL"<br /><br /> "**UNIFORME**"|  
|**CONTENT_TYPE**|**DBTYPE_WSTR**||Tipo de contenido de la columna de estructura de minería de datos:<br /><br /> "**CLAVE**"<br /><br /> "**DISCRETAS**"<br /><br /> "**CONTINUOUS**"<br /><br /> "**DISCRETIZED (**[args]**)**"<br /><br /> "**ORDENADOS**"<br /><br /> "**SEQUENCE_TIME**"<br /><br /> "**CÍCLICOS**"<br /><br /> "**PROBABILIDAD**"<br /><br /> "**VARIANZA**"<br /><br /> "**STDEV**"<br /><br /> "**COMPATIBILIDAD**"<br /><br /> "**PROBABILITY_VARIANCE**"<br /><br /> "**PROBABILITY_STDEV**"|  
|**MODELING_FLAG**|**DBTYPE_WSTR**||Lista delimitada por comas de marcas de modelado. La única marca admitida para una columna de estructura es "**NOT NULL**".|  
|**IS_RELATED_TO_KEY**|**DBTYPE_BOOL**||Valor booleano que indica si esta columna está relacionada con la clave.<br /><br /> **VARIANT_TRUE** si esta columna está relacionada con la clave; **VARIANT_FALSE** en caso contrario. Si la clave es una sola columna, el **RELATED_ATTRIBUTE** campo, opcionalmente, puede contener su nombre de columna.|  
|**RELATED_ATTRIBUTE**|**DBTYPE_WSTR**||Nombre de la columna de destino con la que se relaciona la columna actual o de la que es una propiedad especial.|  
|**CONTAINING_COLUMN**|**DBTYPE_WSTR**||El nombre de la **tabla** columna que contiene esta columna. **NULL** si no hay ninguna tabla contiene la columna.|  
|**IS_POPULATED**|**DBTYPE_BOOL**||Valor booleano que indica si esta columna ha obtenido información sobre un conjunto de valores posibles.<br /><br /> **TRUE** si la columna ha obtenido información sobre un conjunto de posibles valores; **FALSE**, en caso contrario.|  
  
## <a name="restriction-columns"></a>Columnas de restricción  
 El **DMSCHEMA_MINING_STRUCTURE_COLUMNS** se puede restringir el conjunto de filas en las columnas de la tabla siguiente.  
  
|Nombre de columna|Indicador de tipo|Estado de restricción|  
|-----------------|--------------------|-----------------------|  
|**STRUCTURE_CATALOG**|**DBTYPE_WSTR**|Opcional.|  
|**STRUCTURE_SCHEMA**|**DBTYPE_WSTR**|Opcional.|  
|**NOMBRE_ESTRUCTURA**|**DBTYPE_WSTR**|Opcional.|  
|**COLUMN_NAME**|**DBTYPE_WSTR**|Opcional.|  
  
## <a name="see-also"></a>Vea también  
 [Conjuntos de filas de esquema de minería de datos](../../../analysis-services/schema-rowsets/data-mining/data-mining-schema-rowsets.md)  
  
  
