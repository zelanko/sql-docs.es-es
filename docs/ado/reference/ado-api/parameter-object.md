---
title: Objeto Parameter | Documentos de Microsoft
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: reference
ms.technology:
- drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: sql
ms.tgt_pltfrm: 
ms.topic: article
apitype: COM
f1_keywords:
- Parameter
helpviewer_keywords:
- Parameter object [ADO]
ms.assetid: e010e794-7f0f-4026-8b5b-37328e437d63
caps.latest.revision: 11
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 8ed793606962eda3b6d7b29fedad3bb0f0dd18b0
ms.contentlocale: es-es
ms.lasthandoff: 09/09/2017

---
# <a name="parameter-object"></a>Objeto Parameter
Representa un parámetro o un argumento asociado con un [comando](../../../ado/reference/ado-api/command-object-ado.md) objeto basado en una consulta con parámetros o un procedimiento almacenado.  
  
## <a name="remarks"></a>Comentarios  
 Muchos proveedores admiten comandos parametrizados. Estos son los comandos en el que la acción deseada se define una vez, pero se utilizan variables (o parámetros) para modificar algunos detalles del comando. Por ejemplo, una instrucción SELECT de SQL podría usar un parámetro para definir los criterios de coincidencia de una cláusula WHERE y otro para definir el nombre de una cláusula Ordenar por columna.  
  
 **Parámetro** objetos representan parámetros asociados a consultas parametrizadas, o los argumentos de entrada/salida y los valores devueltos de los procedimientos almacenan. Dependiendo de la funcionalidad del proveedor, algunas colecciones, métodos o propiedades de un **parámetro** objeto no estén disponible.  
  
 Con las colecciones, métodos y propiedades de un **parámetro** de objeto, puede hacer lo siguiente:  
  
-   Establecer o devolver el nombre de un parámetro con el [nombre](../../../ado/reference/ado-api/name-property-ado.md) propiedad.  
  
-   Establecer o devolver el valor de un parámetro con el [valor](../../../ado/reference/ado-api/value-property-ado.md) propiedad. **Valor** es la propiedad predeterminada de la **parámetro** objeto.  
  
-   Establecer o devolver las características de parámetro con el [atributos](../../../ado/reference/ado-api/attributes-property-ado.md), [dirección](../../../ado/reference/ado-api/direction-property.md), [precisión](../../../ado/reference/ado-api/precision-property-ado.md), [NumericScale](../../../ado/reference/ado-api/numericscale-property-ado.md), [ Tamaño](../../../ado/reference/ado-api/size-property-ado-parameter.md), y [tipo](../../../ado/reference/ado-api/type-property-ado.md) propiedades.  
  
-   Pasar datos de caracteres o binarios largos a un parámetro con el [AppendChunk](../../../ado/reference/ado-api/appendchunk-method-ado.md) método.  
  
-   Obtener acceso a atributos específicos del proveedor mediante el [propiedades](../../../ado/reference/ado-api/properties-collection-ado.md) colección.  
  
 Si se conocen los nombres y propiedades de los parámetros asocian con el procedimiento almacenado o la consulta parametrizada que desea llamar, puede usar el [CreateParameter](../../../ado/reference/ado-api/createparameter-method-ado.md) método para crear **parámetro** objetos con los valores de propiedad adecuados y utilice el [anexado](../../../ado/reference/ado-api/append-method-ado.md) método para agregarlos a la [parámetros](../../../ado/reference/ado-api/parameters-collection-ado.md) colección. Esto le permite establecer y devolver valores de parámetro sin tener que llamar a la [actualizar](../../../ado/reference/ado-api/refresh-method-ado.md) método en el **parámetros** colección para recuperar la información de parámetros del proveedor, un potencialmente operación que consume muchos recursos.  
  
 El **parámetro** objeto no es seguro para scripting.  
  
 Esta sección contiene el siguiente tema.  
  
-   [Eventos, métodos y propiedades del objeto de parámetro](../../../ado/reference/ado-api/parameter-object-properties-methods-and-events.md)  
  
## <a name="see-also"></a>Vea también  
 [Objeto de comando (ADO)](../../../ado/reference/ado-api/command-object-ado.md)   
 [Método CreateParameter (ADO)](../../../ado/reference/ado-api/createparameter-method-ado.md)   
 [Colección de parámetros (ADO)](../../../ado/reference/ado-api/parameters-collection-ado.md)   
 [Colección de propiedades (ADO)](../../../ado/reference/ado-api/properties-collection-ado.md)

