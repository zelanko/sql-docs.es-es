---
title: Conjunto de filas DMSCHEMA_MINING_COLUMNS | Documentos de Microsoft
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
- DMSCHEMA_MINING_COLUMNS
topic_type:
- apiref
helpviewer_keywords:
- DMSCHEMA_MINING_COLUMNS rowset
ms.assetid: ae35ccde-4438-46f4-8611-40b2b1a42fce
caps.latest.revision: 35
author: Minewiskan
ms.author: owend
manager: mblythe
ms.openlocfilehash: d53285b088b471ad7a5fca87536cc897db8126d9
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/19/2018
ms.locfileid: "36198301"
---
# <a name="dmschemaminingcolumns-rowset"></a>Conjunto de filas DMSCHEMA_MINING_COLUMNS
  Describe las columnas individuales de todos los modelos de minería de datos en [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]. Este conjunto de filas está restringido al catálogo actual.  
  
## <a name="rowset-columns"></a>Columnas del conjunto de filas  
 El `DMSCHEMA_MINING_COLUMNS` filas contiene las columnas siguientes.  
  
|Nombre de columna|Indicador de tipo|Longitud|Descripción|  
|-----------------|--------------------|------------|-----------------|  
|`MODEL_CATALOG`|`DBTYPE_WSTR`||Nombre del catálogo. Se rellena con el nombre de la base de datos de la que es miembro el modelo.|  
|`MODEL_SCHEMA`|`DBTYPE_WSTR`||Nombre del esquema sin certificar. Esta columna no es compatible con [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]; siempre contiene `NULL`.|  
|`MODEL_NAME`|`DBTYPE_WSTR`||El nombre del modelo de minería de datos. Esta columna contiene el nombre del modelo de minería al que una columna está asociada y nunca está vacío.|  
|`COLUMN_NAME`|`DBTYPE_WSTR`||Nombre de la columna.|  
|`COLUMN_GUID`|`DBTYPE_GUID`||GUID de la columna. [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] no admite esta columna; siempre contiene `NULL`.|  
|`COLUMN_PROPID`|`DBTYPE_UI4`||Identificador de propiedad de la columna. [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] no admite esta columna; siempre contiene `NULL`.|  
|`ORDINAL_POSITION`|`DBTYPE_UI4`||La posición ordinal de la columna. Las columnas se numeran a partir de 1. Esta columna contiene `NULL` si no hay ningún valor de ordinal estable para la columna.|  
|`COLUMN_HAS_DEFAULT`|`DBTYPE_BOOL`||Valor booleano que indica si la columna tiene un valor predeterminado.<br /><br /> `TRUE` si la columna tiene un valor predeterminado, de lo contrario es `FALSE`.|  
|`COLUMN_DEFAULT`|`DBTYPE_WSTR`||El valor predeterminado de la columna.<br /><br /> Si el valor predeterminado es `NULL`, `COLUMN_HASDEFAULT` contiene el valor `TRUE` y esta columna contiene `NULL`.|  
|`COLUMN_FLAGS`|`DBTYPE_UI4`||Máscara de bits que describe las características de la columna. El tipo enumerado `DBCOLUMNFLAGS` especifica los bits de la máscara de bits. Esta columna nunca está vacía.|  
|`IS_NULLABLE`|`DBTYPE_BOOL`||Valor booleano que indica si la columna admite valores NULL.<br /><br /> `FALSE` si la columna no puede admitir valores NULL; de lo contrario, es `TRUE`.|  
|`DATA_TYPE`|`DBTYPE_UI2`||Indicador del tipo de datos de la columna. La lista siguiente muestra ejemplos de los tipos de indicadores devueltos:<br /><br /> "`TABLE`" devolvería `DBTYPE_HCHAPTER`.<br /><br /> "`TEXT`" devolvería `DBTYPE_WCHAR`.<br /><br /> "`LONG`" devolvería `DBTYPE_I8`.<br /><br /> "`DOUBLE`" devolvería `DBTYPE_R8`.<br /><br /> "`DATE`" devolvería `DBTYPE_DATE`.|  
|`TYPE_GUID`|`DBTYPE_GUID`||GUID del tipo de datos de la columna. [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] no admite esta columna; siempre contiene `VT_NULL`.|  
|`CHARACTER_MAXIMUM_LENGTH`|`DBTYPE_UI4`||Longitud máxima permitida para un valor de la columna. Para las columnas de caracteres, binarias o de tipo bit, es uno de los valores siguientes:<br /><br /> -La longitud máxima de la columna en caracteres, bytes o bits, respectivas al tipo de columna, si se define una longitud. Por ejemplo, una columna `CHAR(5)` de una tabla SQL tiene una longitud máxima de 5.<br />-La longitud máxima del tipo de datos de caracteres, bytes o bits, respectivas al tipo de columna, si la columna no tiene una longitud definida.<br />-Cero (0) si la columna ni el tipo de datos tiene una longitud máxima definida.<br />-   `NULL` para los demás tipos de columnas|  
|`CHARACTER_OCTET_LENGTH`|`DBTYPE_UI4`||Longitud máxima de la columna en octetos (bytes), si la columna es de caracteres o binaria. Un valor cero (0) significa que la columna no tiene una longitud máxima. Esta columna contiene `NULL` para los demás tipos de columnas.|  
|`NUMERIC_PRECISION`|`DBTYPE_UI2`||Precisión máxima de la columna si el tipo de datos de la misma es de un tipo de datos numérico distinto de `VARNUMERIC`.<br /><br /> `NULL` si el tipo de datos de la columna no es numérico o es `VARNUMERIC`.<br /><br /> La precisión de las columnas con un tipo de datos `DBTYPE_DECIMAL` o `DBTYPE_NUMERIC`depende de la definición de la columna.|  
|`NUMERIC_SCALE`|`DBTYPE_I2`||Número de dígitos que se encuentran a la derecha del separador decimal si el indicador de tipo de la columna es `DBTYPE_DECIMAL`, `DBTYPE_NUMERIC` o `DBTYPE_VARNUMERIC`. De lo contrario, esta columna contiene `VT_NULL`.|  
|`DATETIME_PRECISION`|`DBTYPE_UI4`||Precisión de fecha y hora (el número de dígitos en la parte de las fracciones de segundo) de la columna si el tipo de datos de columna es un tipo de intervalo o DateTime; de lo contrario, `NULL`.|  
|`CHARACTER_SET_CATALOG`|`DBTYPE_WSTR`||Nombre del catálogo en el que está definido el juego de caracteres. [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] no admite esta columna; siempre contiene `NULL`.|  
|`CHARACTER_SET_SCHEMA`|`DBTYPE_WSTR`||Nombre del esquema sin certificar en el que se define el juego de caracteres. [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] no admite esta columna; siempre contiene `NULL`.|  
|`CHARACTER_SET_NAME`|`DBTYPE_WSTR`||El juego de caracteres nombre. [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] no admite esta columna; siempre contiene `NULL`.|  
|`COLLATION_CATALOG`|`DBTYPE_WSTR`||Nombre del catálogo en el que está definida la intercalación. [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] no admite esta columna; siempre contiene `NULL`.|  
|`COLLATION_SCHEMA`|`DBTYPE_WSTR`||Nombre del esquema sin certificar en el que se define la intercalación. [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] no admite esta columna; siempre contiene `NULL`.|  
|`COLLATION_NAME`|`DBTYPE_WSTR`||Nombre de intercalación. [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] no admite esta columna; siempre contiene `NULL`.|  
|`DOMAIN_CATALOG`|`DBTYPE_WSTR`||Nombre del catálogo en el que está definido el dominio. [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] no admite esta columna; siempre contiene `NULL`.|  
|`DOMAIN_SCHEMA`|`DBTYPE_WSTR`||Nombre del esquema sin certificar en el que está definido el dominio. [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] no admite esta columna; siempre contiene `NULL`.|  
|`DOMAIN_NAME`|`DBTYPE_WSTR`||Nombre del dominio. [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] no admite esta columna; siempre contiene `NULL`.|  
|`DESCRIPTION`|`DBTYPE_WSTR`||Descripción sencilla de la columna. [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] no admite esta columna; siempre contiene `NULL`.|  
|`DISTRIBUTION_FLAG`|`DBTYPE_WSTR`||Descripción de la distribución estadística de la columna. Esta columna contiene uno de los siguientes datos:<br /><br /> -   "`NORMAL`"<br />-   "`LOG_NORMAL`"<br />-   "`UNIFORM`"|  
|`CONTENT_TYPE`|`DBTYPE_WSTR`||Descripción del contenido de la columna. Esta columna contiene uno de los siguientes datos:<br /><br /> -   "`KEY`"<br />-   "`DISCRETE`"<br />-   "`CONTINUOUS`"<br />-"`DISCRETIZED(`[argumentos]`)`"<br />-   "`ORDERED`"<br />-   "`KEY TIME`"<br />-   "`CYCLICAL`"<br />-   "`PROBABILITY`"<br />-   "`VARIANCE`"<br />-   "`STDEV`"<br />-   "`SUPPORT`"<br />-   "`PROBABILITY_VARIANCE`"<br />-   "`PROBABILITY_STDEV`"<br />-   `"KEY SEQUENCE`"|  
|`MODELING_FLAG`|`DBTYPE_WSTR`||Lista de marcas delimitada por comas. Las marcas definidas son:<br /><br /> -   "`MODEL_EXISTENCE_ONLY`"<br />-   "`REGRESSOR`"<br /><br /> Las marcas de modelado específicas del algoritmo también pueden estar contenidas en esta columna.|  
|`IS_RELATED_TO_KEY`|`DBTYPE_BOOL`||Un valor booleano que indica si la columna está relacionada con la clave.<br /><br /> `TRUE` si esta columna está relacionada con la clave. Si la clave es una columna única, el campo `RELATED_ATTRIBUTE` puede contener su nombre de columna si se desea.|  
|`RELATED_ATTRIBUTE`|`DBTYPE_WSTR`||El nombre de la columna de destino a la que la columna actual se relaciona o es una propiedad especial.|  
|`IS_INPUT`|`DBTYPE_BOOL`||Valor booleano que indica si la columna es de entrada.<br /><br /> `VARIANT_TRUE` si se trata de una columna de entrada.|  
|`IS_PREDICTABLE`|`DBTYPE_BOOL`||Valor booleano que indica si la columna admite es de predicción.<br /><br /> `TRUE` si la columna es de predicción.|  
|`CONTAINING_COLUMN`|`DBTYPE_WSTR`||Nombre de la columna `TABLE` que contiene esta columna. Esta columna contiene `NULL` si no está contenida en otra.|  
|`PREDICTION_SCALAR_FUNCTIONS`|`DBTYPE_WSTR`||Lista delimitada por comas de las funciones escalares que se pueden realizar en la columna.|  
|`PREDICTION_TABLE_FUNCTIONS`|`DBTYPE_WSTR`||Lista delimitada por comas de las funciones que se pueden aplicar a la columna. Las funciones deberían devolver una tabla. El lista tiene el formato siguiente:<br /><br /> `<function name>(<column1> [, <column2>], ...)`<br /><br /> El formato permite a la aplicación cliente determinar la firma (lista de parámetros) de la función respectiva.|  
|`IS_POPULATED`|`DBTYPE_BOOL`||Valor booleano que indica si la columna se ha entrenado con un conjunto de valores posibles.<br /><br /> `TRUE` si la columna se ha entrenado con un conjunto de valores posibles.<br /><br /> Contiene `FALSE` si la columna no se rellena.|  
|`PREDICTION_SCORE`|`DBTYPE_R8`||La puntuación del modelo al predecir la columna. La puntuación se utiliza para medir la exactitud de un modelo.|  
|`SOURCE_COLUMN`|`DBTYPE_WSTR`||Nombre de la columna de estructura de minería de datos de origen para la columna de minería actual.|  
  
## <a name="restriction-columns"></a>Columnas de restricción  
 El `DMSCHEMA_MINING_COLUMNS` se puede restringir el conjunto de filas en las columnas enumeradas en la tabla siguiente.  
  
|Nombre de columna|Indicador de tipo|Estado de restricción|  
|-----------------|--------------------|-----------------------|  
|`MODEL_CATALOG`|`DBTYPE_WSTR`|Opcional.|  
|`MODEL_SCHEMA`|`DBTYPE_WSTR`|Opcional.|  
|`MODEL_NAME`|`DBTYPE_WSTR`|Opcional.|  
|`COLUMN_NAME`|`DBTYPE_WSTR`|Opcional.|  
  
## <a name="see-also"></a>Vea también  
 [Conjuntos de filas de esquema de minería de datos](../../schema-rowsets/data-mining/data-mining-schema-rowsets.md) 
  
  