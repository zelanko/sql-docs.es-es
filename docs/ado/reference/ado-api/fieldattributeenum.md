---
title: FieldAttributeEnum | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- FieldAttributeEnum
helpviewer_keywords:
- FieldAttributeEnum enumeration [ADO]
ms.assetid: 6e34d886-005a-40dc-bd5c-6adcbf81e5cd
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: e0f6984c464c08518c7b3143986a041b195cce69
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/15/2019
ms.locfileid: "66695065"
---
# <a name="fieldattributeenum"></a>FieldAttributeEnum
Especifica uno o varios atributos de un [campo](../../../ado/reference/ado-api/field-object.md) objeto.  
  
|Constante|Valor|Descripción|  
|--------------|-----------|-----------------|  
|**adFldCacheDeferred**|0x1000|Indica que el proveedor almacena en caché los valores de campo y que se realizan las lecturas subsiguientes de la memoria caché.|  
|**adFldFixed**|0x10|Indica que el campo contiene datos de longitud fija.|  
|**adFldIsChapter**|0x2000|Indica que el campo contiene un valor de capítulo, que especifica un conjunto de registros secundarios específicos relacionados con este campo primario. Normalmente se usan los campos de capítulo con forma de datos o filtros.|  
|**adFldIsCollection**|0x40000|Indica que el campo especifica que el recurso representado por el registro es una colección de otros recursos, como una carpeta, en lugar de un recurso simple, como un archivo de texto.|  
|**adFldKeyColumn**|0x8000|Indica que el campo especifica todo o parte de clave principal la columna.|  
|**adFldIsDefaultStream**|0x20000|Indica que el campo contiene la secuencia predeterminada para el recurso representado por el registro. Por ejemplo, la secuencia predeterminada puede ser el contenido HTML de una carpeta raíz en un sitio Web, que se sirven automáticamente cuando se especifica la dirección URL raíz.|  
|**adFldIsNullable**|0x20|Indica que el campo acepta valores null.|  
|**adFldIsRowURL**|0x10000|Indica que el campo contiene la dirección URL que los nombres de los recursos del almacén de datos representado por el registro.|  
|**adFldLong**|0x80|Indica que el campo es un campo binario largo. También indica que se puede utilizar el [AppendChunk](../../../ado/reference/ado-api/appendchunk-method-ado.md) y [GetChunk](../../../ado/reference/ado-api/getchunk-method-ado.md) métodos.|  
|**adFldMayBeNull**|0x40|Indica que puede leer valores nulos del campo.|  
|**adFldMayDefer**|0x2|Indica que el campo es que aplaza es, no se recuperan los valores de campo del origen de datos con el registro completo, pero solo cuando se realiza un acceso explícito a ellos.|  
|**adFldNegativeScale**|0x4000|Indica que el campo representa un valor numérico de una columna que admite valores de escala negativos. La escala es especificada por el [NumericScale](../../../ado/reference/ado-api/numericscale-property-ado.md) propiedad.|  
|**adFldRowID**|0x100|Indica que el campo contiene un identificador de fila persistente que no se puede escribir y no tiene ningún valor significativo salvo para identificar la fila (por ejemplo, un número de registro, identificador único y así sucesivamente).|  
|**adFldRowVersion**|0x200|Indica que el campo contiene algún tipo de marca de hora o fecha usada para realizar el seguimiento de las actualizaciones.|  
|**adFldUnknownUpdatable**|0x8|Indica que el proveedor no puede determinar si puede escribir en el campo.|  
|**adFldUnspecified**|-0xFFFFFFFF 1|Indica que el proveedor no especifica los atributos del campo.|  
|**adFldUpdatable**|0x4|Indica que puede escribir en el campo.|  
  
## <a name="adowfc-equivalent"></a>Equivalente de ADO y WFC  
 Package: **com.ms.wfc.data**  
  
|Constante|  
|--------------|  
|AdoEnums.FieldAttribute.CACHEDEFERRED|  
|AdoEnums.FieldAttribute.FIXED|  
|AdoEnums.FieldAttribute.ISNULLABLE|  
|AdoEnums.FieldAttribute.LONG|  
|AdoEnums.FieldAttribute.MAYBENULL|  
|AdoEnums.FieldAttribute.MAYDEFER|  
|AdoEnums.FieldAttribute.NEGATIVESCALE|  
|AdoEnums.FieldAttribute.ROWID|  
|AdoEnums.FieldAttribute.ROWVERSION|  
|AdoEnums.FieldAttribute.UNKNOWNUPDATABLE|  
|AdoEnums.FieldAttribute.UNSPECIFIED|  
|AdoEnums.FieldAttribute.UPDATABLE|  
  
## <a name="applies-to"></a>Se aplica a  
  
|||  
|-|-|  
|[Append (método) (ADO)](../../../ado/reference/ado-api/append-method-ado.md)|[Propiedad Attributes (ADO)](../../../ado/reference/ado-api/attributes-property-ado.md)|
