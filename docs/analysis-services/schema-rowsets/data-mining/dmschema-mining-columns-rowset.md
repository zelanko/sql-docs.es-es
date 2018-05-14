---
title: Conjunto de filas DMSCHEMA_MINING_COLUMNS | Documentos de Microsoft
ms.date: 05/03/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: schema-rowsets
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 1f5d5dcc4385634b24cadf9e08c2298cc7bacc26
ms.sourcegitcommit: c12a7416d1996a3bcce3ebf4a3c9abe61b02fb9e
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/10/2018
---
# <a name="dmschemaminingcolumns-rowset"></a>Conjunto de filas DMSCHEMA_MINING_COLUMNS
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]
  Describe las columnas individuales de todos los modelos de minería de datos en [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]. Este conjunto de filas está restringido al catálogo actual.  
  
## <a name="rowset-columns"></a>Columnas del conjunto de filas  
 El **DMSCHEMA_MINING_COLUMNS** filas contiene las columnas siguientes.  
  
|Nombre de columna|Indicador de tipo|Description|  
|-----------------|--------------------|-----------------|  
|**MODEL_CATALOG**|**DBTYPE_WSTR**|Nombre del catálogo. Se rellena con el nombre de la base de datos de la que es miembro el modelo.|  
|**MODEL_SCHEMA**|**DBTYPE_WSTR**|Nombre del esquema sin certificar. Esta columna no es compatible con [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]; siempre contiene **NULL**.|  
|**MODEL_NAME**|**DBTYPE_WSTR**|El nombre del modelo de minería de datos. Esta columna contiene el nombre del modelo de minería al que una columna está asociada y nunca está vacío.|  
|**COLUMN_NAME**|**DBTYPE_WSTR**|Nombre de la columna.|  
|**COLUMN_GUID**|**DBTYPE_GUID**|GUID de la columna. Esta columna no es compatible con [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]; siempre contiene **NULL**.|  
|**COLUMN_PROPID**|**DBTYPE_UI4**|Identificador de propiedad de la columna. Esta columna no es compatible con [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]; siempre contiene **NULL**.|  
|**ORDINAL_POSITION**|**DBTYPE_UI4**|La posición ordinal de la columna. Las columnas se numeran a partir de 1. Esta columna contiene **NULL** si no hay ningún valor ordinal estable para la columna.|  
|**COLUMN_HAS_DEFAULT**|**DBTYPE_BOOL**|Valor booleano que indica si la columna tiene un valor predeterminado.<br /><br /> **TRUE** si la columna tiene un valor predeterminado, en caso contrario, **FALSE**.|  
|**COLUMN_DEFAULT**|**DBTYPE_WSTR**|El valor predeterminado de la columna.<br /><br /> Si el valor predeterminado es el **NULL** valor, **COLUMN_HASDEFAULT** contiene **TRUE**, y esta columna contiene **NULL**.|  
|**COLUMN_FLAGS**|**DBTYPE_UI4**|Máscara de bits que describe las características de la columna. El **DBCOLUMNFLAGS** tipo enumerado especifica los bits de la máscara de bits. Esta columna nunca está vacía.|  
|**IS_NULLABLE**|**DBTYPE_BOOL**|Valor booleano que indica si la columna admite valores NULL.<br /><br /> **FALSE** si la columna se sabe que no acepta valores NULL; en caso contrario, **TRUE**.|  
|**DATA_TYPE**|**DBTYPE_UI2**|Indicador del tipo de datos de la columna. La lista siguiente muestra ejemplos de los tipos de indicadores devueltos:<br /><br /> "**Tabla**" devolvería **DBTYPE_HCHAPTER**.<br /><br /> "**Texto**" devolvería **DBTYPE_WCHAR**.<br /><br /> "**Largo**" devolvería **DBTYPE_I8**.<br /><br /> "**Doble**" devolvería **DBTYPE_R8**.<br /><br /> "**Fecha**" devolvería **DBTYPE_DATE**.|  
|**TYPE_GUID**|**DBTYPE_GUID**|GUID del tipo de datos de la columna. Esta columna no es compatible con [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]; siempre contiene **VT_NULL**.|  
|**CAMPO CHARACTER_MAXIMUM_LENGTH**|**DBTYPE_UI4**|Longitud máxima permitida para un valor de la columna. Para las columnas de caracteres, binarias o de tipo bit, es uno de los valores siguientes:<br /><br /> Longitud máxima de la columna en caracteres, bytes o bits, respecto al tipo de columna, si se define una longitud. Por ejemplo, un **char (5)** columna en una tabla de SQL tiene una longitud máxima de 5.<br /><br /> Longitud máxima del tipo de datos en caracteres, bytes o bits, respecto al tipo de columna, si la columna no tiene una longitud definida.<br /><br /> Cero (0) si la columna y el tipo de datos no tienen una longitud máxima definida.<br /><br /> **NULL** para todos los demás tipos de columnas|  
|**CHARACTER_OCTET_LENGTH**|**DBTYPE_UI4**|Longitud máxima de la columna en octetos (bytes), si la columna es de caracteres o binaria. Un valor cero (0) significa que la columna no tiene una longitud máxima. Esta columna contiene **NULL** para todos los demás tipos de columnas.|  
|**CAMPO NUMERIC_PRECISION**|**DBTYPE_UI2**|La precisión máxima de la columna si el tipo de datos de la columna es un tipo de datos numérico distinto de **VARNUMERIC**.<br /><br /> **NULL** si el tipo de datos de la columna no es numérico o es **VARNUMERIC**.<br /><br /> La precisión de las columnas con un tipo de datos de **DBTYPE_DECIMAL** o **DBTYPE_NUMERIC** depende de la definición de columna.|  
|**NUMERIC_SCALE**|**DBTYPE_I2**|El número de dígitos a la derecha del separador decimal si el indicador de tipo de la columna es **DBTYPE_DECIMAL**, **DBTYPE_NUMERIC**, o **DBTYPE_VARNUMERIC**. En caso contrario, esta columna contiene **VT_NULL**.|  
|**DATETIME_PRECISION**|**DBTYPE_UI4**|La precisión de fecha y hora (número de dígitos en la parte de las fracciones de segundo) de la columna si el tipo de datos de columna es un tipo de intervalo o DateTime; en caso contrario, **NULL**.|  
|**CHARACTER_SET_CATALOG**|**DBTYPE_WSTR**|Nombre del catálogo en el que está definido el juego de caracteres. Esta columna no es compatible con [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]; siempre contiene **NULL**.|  
|**CHARACTER_SET_SCHEMA**|**DBTYPE_WSTR**|Nombre del esquema sin certificar en el que se define el juego de caracteres. Esta columna no es compatible con [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]; siempre contiene **NULL**.|  
|**CHARACTER_SET_NAME**|**DBTYPE_WSTR**|El juego de caracteres nombre. Esta columna no es compatible con [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]; siempre contiene **NULL**.|  
|**COLLATION_CATALOG**|**DBTYPE_WSTR**|Nombre del catálogo en el que está definida la intercalación. Esta columna no es compatible con [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]; siempre contiene **NULL**.|  
|**COLLATION_SCHEMA**|**DBTYPE_WSTR**|Nombre del esquema sin certificar en el que se define la intercalación. Esta columna no es compatible con [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]; siempre contiene **NULL**.|  
|**COLLATION_NAME**|**DBTYPE_WSTR**|Nombre de intercalación. Esta columna no es compatible con [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]; siempre contiene **NULL**.|  
|**DOMAIN_CATALOG**|**DBTYPE_WSTR**|Nombre del catálogo en el que está definido el dominio. Esta columna no es compatible con [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]; siempre contiene **NULL**.|  
|**DOMAIN_SCHEMA**|**DBTYPE_WSTR**|Nombre del esquema sin certificar en el que está definido el dominio. Esta columna no es compatible con [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]; siempre contiene **NULL**.|  
|**NOMBRE_DOMINIO**|**DBTYPE_WSTR**|Nombre del dominio. Esta columna no es compatible con [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]; siempre contiene **NULL**.|  
|**DESCRIPTION**|**DBTYPE_WSTR**|Una descripción fácil de usar de la columna de esta columna no es compatible con [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]; siempre contiene **NULL**.|  
|**DISTRIBUTION_FLAG ES**|**DBTYPE_WSTR**|Descripción de la distribución estadística de la columna. Esta columna contiene uno de los siguientes datos:<br /><br /> "**NORMAL**"<br /><br /> "**LOG_NORMAL**"<br /><br /> "**UNIFORME**"|  
|**CONTENT_TYPE**|**DBTYPE_WSTR**|Descripción del contenido de la columna. Esta columna contiene uno de los siguientes datos:<br /><br /> "**CLAVE**"<br /><br /> "**DISCRETAS**"<br /><br /> "**CONTINUOUS**"<br /><br /> "**DISCRETIZED (**[argumentos]**)**"<br /><br /> "**ORDENADOS**"<br /><br /> "**CLAVE TEMPORAL**"<br /><br /> "**CÍCLICOS**"<br /><br /> "**PROBABILIDAD**"<br /><br /> "**VARIANZA**"<br /><br /> "**STDEV**"<br /><br /> "**COMPATIBILIDAD**"<br /><br /> "**PROBABILITY_VARIANCE**"<br /><br /> "**PROBABILITY_STDEV**"<br /><br /> **"SECUENCIA DE TECLAS**"|  
|**MODELING_FLAG**|**DBTYPE_WSTR**|Lista de marcas delimitada por comas. Las marcas definidas son:<br /><br /> "**MODEL_EXISTENCE_ONLY**"<br /><br /> "**REGRESOR**"<br /><br /> Las marcas de modelado específicas del algoritmo también pueden estar contenidas en esta columna.|  
|**IS_RELATED_TO_KEY**|**DBTYPE_BOOL**|Un valor booleano que indica si la columna está relacionada con la clave.<br /><br /> **TRUE** si esta columna está relacionada con la clave. Si la clave es una sola columna, el **RELATED_ATTRIBUTE** campo, opcionalmente, puede contener su nombre de columna.|  
|**RELATED_ATTRIBUTE**|**DBTYPE_WSTR**|El nombre de la columna de destino a la que la columna actual se relaciona o es una propiedad especial.|  
|**IS_INPUT**|**DBTYPE_BOOL**|Valor booleano que indica si la columna es de entrada.<br /><br /> **VARIANT_TRUE** si se trata de una columna de entrada.|  
|**IS_PREDICTABLE**|**DBTYPE_BOOL**|Valor booleano que indica si la columna admite es de predicción.<br /><br /> **TRUE** si la columna es de predicción.|  
|**CONTAINING_COLUMN**|**DBTYPE_WSTR**|El nombre de la **tabla** columna que contiene esta columna. Esta columna contiene **NULL** si la columna no se encuentra en otra columna.|  
|**PREDICTION_SCALAR_FUNCTIONS**|**DBTYPE_WSTR**|Lista delimitada por comas de las funciones escalares que se pueden realizar en la columna.|  
|**PREDICTION_TABLE_FUNCTIONS**|**DBTYPE_WSTR**|Lista delimitada por comas de las funciones que se pueden aplicar a la columna. Las funciones deberían devolver una tabla. El lista tiene el formato siguiente:<br /><br /> `<function name>(<column1> [, <column2>], ...)`<br /><br /> El formato permite a la aplicación cliente determinar la firma (lista de parámetros) de la función respectiva.|  
|**IS_POPULATED**|**DBTYPE_BOOL**|Valor booleano que indica si la columna se ha entrenado con un conjunto de valores posibles.<br /><br /> **TRUE** si la columna se ha entrenado con un conjunto de valores posibles.<br /><br /> Contiene **FALSE** si no se rellena la columna.|  
|**PREDICTION_SCORE**|**DBTYPE_R8**|La puntuación del modelo al predecir la columna. La puntuación se utiliza para medir la exactitud de un modelo.|  
|**SOURCE_COLUMN**|**DBTYPE_WSTR**|Nombre de la columna de estructura de minería de datos de origen para la columna de minería actual.|  
  
## <a name="restriction-columns"></a>Columnas de restricción  
 El **DMSCHEMA_MINING_COLUMNS** se puede restringir el conjunto de filas en las columnas enumeradas en la tabla siguiente.  
  
|Nombre de columna|Indicador de tipo|Estado de restricción|  
|-----------------|--------------------|-----------------------|  
|**MODEL_CATALOG**|**DBTYPE_WSTR**|Opcional.|  
|**MODEL_SCHEMA**|**DBTYPE_WSTR**|Opcional.|  
|**MODEL_NAME**|**DBTYPE_WSTR**|Opcional.|  
|**COLUMN_NAME**|**DBTYPE_WSTR**|Opcional.|  
  
## <a name="see-also"></a>Vea también  
 [Conjuntos de filas de esquema de minería de datos](../../../analysis-services/schema-rowsets/data-mining/data-mining-schema-rowsets.md)  
  
  
