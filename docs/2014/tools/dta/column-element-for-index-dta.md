---
title: Column (DTA, elemento de index) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: tools-other
ms.topic: conceptual
dev_langs:
- XML
helpviewer_keywords:
- Column element
ms.assetid: ba9fac20-26bd-4333-940e-842c15241b46
author: stevestein
ms.author: sstein
ms.openlocfilehash: 23e6a3225dc8ddd3049f59986924c1fbb71c173b
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/18/2020
ms.locfileid: "85007707"
---
# <a name="column-element-for-index-dta"></a>Column (DTA, elemento de Index)
  Establece las columnas de una configuración especificada por el usuario en las que se va a crear el índice.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
<Create>  
  <Index>  
    <Name>...</Name>  
    <Column [Type | SortOrder]>  
     ...code removed here...  
     </Column>  
```  
  
## <a name="element-attributes"></a>Atributos del elemento  
  
|Atributo Column|Descripción|  
|----------------------|-----------------|  
|`Type`|Opcional. Especifica el tipo de columna de índice. Utilice un tipo de datos **string** para especificar este atributo mediante uno de los siguientes valores permitidos:<br /><br /> `KeyColumn`:<br />                  Especifica que una clave de índice hace referencia a la columna. Utilice la siguiente sintaxis para establecer este atributo:<br />`<Column Type="KeyColumn">`<br />Para obtener más información sobre las columnas de claves, vea [Índices agrupados y no agrupados descritos](../../relational-databases/indexes/clustered-and-nonclustered-indexes-described.md).<br /><br /> `IncludedColumn`: Especifica que la columna es una columna incluida (en lugar de una columna de clave). Utilice la siguiente sintaxis para establecer este atributo:<br />`<Column Type="IncludedColumn">`<br />Para obtener más información sobre las columnas incluidas, vea [Crear índices con columnas incluidas](../../relational-databases/indexes/create-indexes-with-included-columns.md).|  
|`SortOrder`|Opcional. Especifica el orden de la columna. Utilice un tipo de datos **string** para especificar un orden **"Ascending"** (ascendente) o **"Descending"** (descendente), como se muestra a continuación:<br /><br /> `<Column SortOrder="Ascending">`|  
  
## <a name="element-characteristics"></a>Características de los elementos  
  
|Característica|Descripción|  
|--------------------|-----------------|  
|**Tipo y longitud de los datos**|Ninguno.|  
|**Valor predeterminado**|Ninguno.|  
|**Repetición**|Puede especificar hasta 1.024 columnas para el elemento `Index`.|  
  
## <a name="element-relationships"></a>Relaciones del elemento  
  
|Relación|Elementos|  
|------------------|--------------|  
|**Elemento primario**|[Index &#40;DTA, elemento&#41;](index-element-dta.md)|  
|**Elementos secundarios**|[Elemento Name de Column &#40;DTA&#41;](name-element-for-column-dta.md)|  
  
## <a name="example"></a>Ejemplo  
 Para obtener un ejemplo de uso de este elemento, vea [Ejemplo de archivo de entrada XML con configuración especificada por el usuario &#40;DTA&#41;](xml-input-file-sample-with-user-specified-configuration-dta.md).  
  
## <a name="see-also"></a>Consulte también  
 [Referencia del archivo de entrada XML &#40;Asistente para la optimización de motor de base de datos&#41;](xml-input-file-reference-database-engine-tuning-advisor.md)  
  
  
