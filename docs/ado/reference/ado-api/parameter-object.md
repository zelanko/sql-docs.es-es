---
title: Objeto Parameter | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Parameter
helpviewer_keywords:
- Parameter object [ADO]
ms.assetid: e010e794-7f0f-4026-8b5b-37328e437d63
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: 152186c0bb1c2fb75197a920e06e0b6bb96dadd0
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/15/2019
ms.locfileid: "66703314"
---
# <a name="parameter-object"></a>Objeto Parameter
Representa un parámetro o un argumento asociado a un [comando](../../../ado/reference/ado-api/command-object-ado.md) objeto basado en un procedimiento almacenado o una consulta parametrizada.  
  
## <a name="remarks"></a>Comentarios  
 Muchos proveedores admiten comandos parametrizados. Estos son los comandos en el que la acción deseada se define una vez, pero se utilizan variables (o parámetros) para modificar algunos detalles del comando. Por ejemplo, una instrucción SELECT de SQL podría usar un parámetro para definir los criterios de coincidencia de una cláusula WHERE y otro para definir el nombre de una cláusula de ordenación por columna.  
  
 **Parámetro** objetos representan parámetros asociados a las consultas con parámetros o los argumentos de entrada/salida y los valores devueltos de procedimientos almacenan. Dependiendo de la funcionalidad del proveedor, algunas colecciones, métodos o propiedades de un **parámetro** objeto no esté disponible.  
  
 Con las colecciones, métodos y propiedades de un **parámetro** objeto, puede hacer lo siguiente:  
  
-   Establecer o devolver el nombre de un parámetro con el [nombre](../../../ado/reference/ado-api/name-property-ado.md) propiedad.  
  
-   Establecer o devolver el valor de un parámetro con el [valor](../../../ado/reference/ado-api/value-property-ado.md) propiedad. **Valor** es la propiedad predeterminada de la **parámetro** objeto.  
  
-   Establecer o devolver las características de parámetro con el [atributos](../../../ado/reference/ado-api/attributes-property-ado.md), [dirección](../../../ado/reference/ado-api/direction-property.md), [precisión](../../../ado/reference/ado-api/precision-property-ado.md), [NumericScale](../../../ado/reference/ado-api/numericscale-property-ado.md), [ Tamaño](../../../ado/reference/ado-api/size-property-ado-parameter.md), y [tipo](../../../ado/reference/ado-api/type-property-ado.md) propiedades.  
  
-   Pasar datos de caracteres o binarios largos a un parámetro con el [AppendChunk](../../../ado/reference/ado-api/appendchunk-method-ado.md) método.  
  
-   Obtener acceso a atributos específicos del proveedor mediante el [propiedades](../../../ado/reference/ado-api/properties-collection-ado.md) colección.  
  
 Si conoce los nombres y propiedades de los parámetros asocian con el procedimiento almacenado o una consulta con parámetros que desea llamar, puede usar el [CreateParameter](../../../ado/reference/ado-api/createparameter-method-ado.md) método para crear **parámetro** objetos con la configuración de la propiedad adecuada y el uso del [Append](../../../ado/reference/ado-api/append-method-ado.md) método para agregarlos a la [parámetros](../../../ado/reference/ado-api/parameters-collection-ado.md) colección. Esto le permite establecer y devolver valores de parámetro sin tener que llamar el [actualizar](../../../ado/reference/ado-api/refresh-method-ado.md) método en el **parámetros** colección para recuperar la información de parámetros del proveedor, un potencialmente operación que consume muchos recursos.  
  
 El **parámetro** objeto no es seguro para scripting.  
  
 Esta sección contiene el siguiente tema.  
  
-   [Los eventos, métodos y propiedades del objeto parameter](../../../ado/reference/ado-api/parameter-object-properties-methods-and-events.md)  
  
## <a name="see-also"></a>Vea también  
 [Objeto Command (ADO)](../../../ado/reference/ado-api/command-object-ado.md)   
 [Método CreateParameter (ADO)](../../../ado/reference/ado-api/createparameter-method-ado.md)   
 [Colección de parámetros (ADO)](../../../ado/reference/ado-api/parameters-collection-ado.md)   
 [Colección de propiedades (ADO)](../../../ado/reference/ado-api/properties-collection-ado.md)
