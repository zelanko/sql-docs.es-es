---
title: Índice de elemento (DTA) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: conceptual
dev_langs:
- XML
helpviewer_keywords:
- Index element (DTA)
ms.assetid: 447d3964-b387-40f6-9189-71386774c29e
caps.latest.revision: 18
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: a9f2efa4761248c94a6db7a2747184808ffce3d3
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/02/2018
ms.locfileid: "37299365"
---
# <a name="index-element-dta"></a>Index, elemento (DTA)
  Contiene información acerca de un índice de una configuración especificada por el usuario que se desea crear o quitar.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
<Recommendation>  
  <Create>  
    <Index [Clustered | Unique | Online | IndexSizeInMB | NumberOfRows             | QUOTED_IDENTIFIER | ARITHABORT | CONCAT_NULL_YIELDS_NULL             | ANSI_NULLS | ANSI_PADDING | ANSI_WARNINGS  
            | NUMERIC_ROUNDABORT]  
     ...code removed here...  
    </Index>  
```  
  
## <a name="element-attributes"></a>Atributos del elemento  
  
|Atributo Index|Tipo de datos|Descripción|  
|---------------------|---------------|-----------------|  
|`Clustered`|`boolean`|Opcional. Especifica un índice clúster. Se establece en "true" o "false", por ejemplo:<br /><br /> `<Index Clustered="true">`<br /><br /> De forma predeterminada, este atributo está establecido en "false".|  
|`Unique`|`boolean`|Opcional. Especifica un índice único. Se establece en "true" o "false", por ejemplo:<br /><br /> `<Index Unique="true">`<br /><br /> De forma predeterminada, este atributo está establecido en "false".|  
|`Online`|`boolean`|Opcional. Especifica un índice que puede realizar operaciones mientras el servidor está en línea, lo que exige espacio temporal en disco. Se establece en "true" o "false", por ejemplo:<br /><br /> `<Index Online="true">`<br /><br /> De forma predeterminada, este atributo está establecido en "false".<br /><br /> Para más información, consulte [Perform Index Operations Online](../../relational-databases/indexes/perform-index-operations-online.md).|  
|`IndexSizeInMB`|`double`|Opcional. Especifica el tamaño máximo del índice en megabytes, por ejemplo:<br /><br /> `<Index IndexSizeInMB="873.75">`<br /><br /> Sin valor predeterminado.|  
|`NumberOfRows`|`integer`|Opcional. Simula diferentes tamaños de índice, lo que simula de forma eficaz diferentes tamaños de tabla, por ejemplo:<br /><br /> `<Index NumberOfRows="3000">`<br /><br /> Sin valor predeterminado.|  
|`QUOTED_IDENTIFIER`|`boolean`|Opcional. Hace que [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] siga las reglas de ISO en cuanto a las comillas delimitadoras de identificadores y cadenas literales. Si el índice se encuentra en una columna o una vista calculada, este atributo debe estar activado. Por ejemplo, la sintaxis siguiente activa este atributo:<br /><br /> `<Index QUOTED_IDENTIFIER [...]>`<br /><br /> De forma predeterminada, este atributo está desactivado.<br /><br /> Para obtener más información, vea [SET QUOTED_IDENTIFIER &#40;Transact-SQL&#41;](/sql/t-sql/statements/set-quoted-identifier-transact-sql).|  
|`ARITHABORT`|`boolean`|Opcional. Cancela una consulta cuando se produce un error de desbordamiento o división por cero durante su ejecución. Si el índice se encuentra en una columna o una vista calculada, este atributo debe estar activado. Por ejemplo, la sintaxis siguiente activa este atributo:<br /><br /> `<Index ARITHABORT [...]>`<br /><br /> De forma predeterminada, este atributo está desactivado.<br /><br /> Para obtener más información, vea [SET ARITHABORT &#40;Transact-SQL&#41;](/sql/t-sql/statements/set-arithabort-transact-sql).|  
|`CONCAT_NULL_YIELDS_`<br /><br /> `NULL`|`boolean`|Opcional. Determina si los resultados de la concatenación se tratan como valor NULL o como cadena vacía. Si el índice se encuentra en una columna o una vista calculada, este atributo debe estar activado. Por ejemplo, la sintaxis siguiente activa este atributo:<br /><br /> `<Index CONCAT_NULL_YIELDS_NULL [...]>`<br /><br /> De forma predeterminada, este atributo está desactivado.<br /><br /> Para obtener más información, vea [SET CONCAT_NULL_YIELDS_NULL &#40;Transact-SQL&#41;](/sql/t-sql/statements/set-concat-null-yields-null-transact-sql).|  
|`ANSI_NULLS`|`boolean`|Opcional. Especifica el comportamiento conforme a ISO de los operadores de comparación Es igual a (=) y No es igual a (<>) cuando se utilizan con valores NULL. Si el índice se encuentra en una columna o una vista calculada, este atributo debe estar activado. Por ejemplo, la sintaxis siguiente activa este atributo:<br /><br /> `<Index ANSI_NULLS [...]>`<br /><br /> De forma predeterminada, este atributo está desactivado.<br /><br /> Para obtener más información, vea [SET ANSI_NULLS &#40;Transact-SQL&#41;](/sql/t-sql/statements/set-ansi-nulls-transact-sql).|  
|`ANSI_PADDING`|`boolean`|Opcional. Controla el modo en que una columna almacena valores inferiores a su tamaño definido. Si el índice se encuentra en una columna o una vista calculada, este atributo debe estar activado. Por ejemplo, la sintaxis siguiente activa este atributo:<br /><br /> `<Index ANSI_PADDING [...]>`<br /><br /> De forma predeterminada, este atributo está desactivado.<br /><br /> Para obtener más información, vea [SET ANSI_PADDING &#40;Transact-SQL&#41;](/sql/t-sql/statements/set-ansi-padding-transact-sql).|  
|`ANSI_WARNINGS`|`boolean`|Opcional. Especifica el comportamiento estándar de ISO para diversas condiciones de error. Si el índice se encuentra en una columna o una vista calculada, este atributo debe estar activado. Por ejemplo, la sintaxis siguiente activa este atributo:<br /><br /> `<Index ANSI_WARNING [...]>`<br /><br /> De forma predeterminada, este atributo está desactivado.<br /><br /> Para obtener más información, vea [SET ANSI_WARNINGS &#40;Transact-SQL&#41;](/sql/t-sql/statements/set-ansi-warnings-transact-sql).|  
|`NUMERIC_ROUNDABORT`|`boolean`|Opcional. Especifica el nivel de informes de error generados cuando el redondeo en una expresión produce pérdida de precisión. Si el índice se encuentra en una columna o una vista calculada, este atributo debe estar desactivado.<br /><br /> La sintaxis siguiente activa este atributo:<br /><br /> `<Index ANSI_WARNING [...]>`<br /><br /> De forma predeterminada, este atributo está desactivado.<br /><br /> Para obtener más información, vea [SET NUMERIC_ROUNDABORT &#40;Transact-SQL&#41;](/sql/t-sql/statements/set-numeric-roundabort-transact-sql).|  
  
## <a name="element-characteristics"></a>Características del elemento  
  
|Característica|Descripción|  
|--------------------|-----------------|  
|**Tipo y longitud de los datos**|Ninguno.|  
|**Valor predeterminado**|Ninguno.|  
|**Repetición**|Una obligatoria por cada elemento `Create` o `Drop` si no se especifica otra estructura de diseño físico con el elemento `Statistics` o `Heap`.|  
  
## <a name="element-relationships"></a>Relaciones del elemento  
  
|Relación|Elementos|  
|------------------|--------------|  
|**Elemento primario**|[Crear elemento &#40;DTA&#41;](create-element-dta.md)<br /><br /> `Drop` Elemento. Para obtener más información, vea el esquema XML del Asistente para la optimización de motor de base de datos.|  
|**Elementos secundarios**|[Nombre de elemento para el índice &#40;DTA&#41;](name-element-for-index-dta.md)<br /><br /> [Elemento de la columna de índice &#40;DTA&#41;](column-element-for-index-dta.md)<br /><br /> `PartitionScheme` Elemento. Para obtener más información, vea el esquema XML del Asistente para la optimización de motor de base de datos.<br /><br /> `PartitionColumn` Elemento. Para obtener más información, vea el esquema XML del Asistente para la optimización de motor de base de datos.<br /><br /> [Grupo de archivos de elemento de Index &#40;DTA&#41;](filegroup-element-for-index-dta.md)<br /><br /> `NumberOfReferences` Elemento. Para obtener más información, vea el esquema XML del Asistente para la optimización de motor de base de datos.<br /><br /> `PercentUsage` Elemento. Para obtener más información, vea el esquema XML del Asistente para la optimización de motor de base de datos.|  
  
## <a name="example"></a>Ejemplo  
 Para obtener un ejemplo de uso de este elemento, vea [Ejemplo de archivo de entrada XML con configuración especificada por el usuario &#40;DTA&#41;](xml-input-file-sample-with-user-specified-configuration-dta.md).  
  
## <a name="see-also"></a>Vea también  
 [Referencia del archivo de entrada XML &#40;Asistente para la optimización de motor de base de datos&#41;](../../relational-databases/performance/database-engine-tuning-advisor.md)  
  
  
