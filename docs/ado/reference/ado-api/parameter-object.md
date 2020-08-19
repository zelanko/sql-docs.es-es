---
description: Objeto Parameter
title: Objeto de parámetro | Microsoft Docs
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
author: rothja
ms.author: jroth
ms.openlocfilehash: ac768cf83d370a1fc60508b5d6a476f0e586d4f6
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/17/2020
ms.locfileid: "88442817"
---
# <a name="parameter-object"></a>Objeto Parameter
Representa un parámetro o un argumento asociado a un objeto de [comando](../../../ado/reference/ado-api/command-object-ado.md) basado en una consulta con parámetros o un procedimiento almacenado.  
  
## <a name="remarks"></a>Observaciones  
 Muchos proveedores admiten comandos con parámetros. Se trata de comandos en los que se define la acción deseada una vez, pero se usan variables (o parámetros) para modificar algunos detalles del comando. Por ejemplo, una instrucción SELECT de SQL podría usar un parámetro para definir los criterios de coincidencia de una cláusula WHERE y otro para definir el nombre de columna para una cláusula SORT BY.  
  
 Los objetos de **parámetro** representan los parámetros asociados a las consultas con parámetros o los argumentos in/out y los valores devueltos de los procedimientos almacenados. Dependiendo de la funcionalidad del proveedor, es posible que algunas colecciones, métodos o propiedades de un objeto de **parámetro** no estén disponibles.  
  
 Con las colecciones, los métodos y las propiedades de un objeto de **parámetro** , puede hacer lo siguiente:  
  
-   Establece o devuelve el nombre de un parámetro con la propiedad [Name](../../../ado/reference/ado-api/name-property-ado.md) .  
  
-   Establece o devuelve el valor de un parámetro con la propiedad [Value](../../../ado/reference/ado-api/value-property-ado.md) . **Value** es la propiedad predeterminada del objeto **Parameter** .  
  
-   Establezca o devuelva características de parámetro con las propiedades [attributes](../../../ado/reference/ado-api/attributes-property-ado.md), [Direction](../../../ado/reference/ado-api/direction-property.md), [Precision](../../../ado/reference/ado-api/precision-property-ado.md), [NumericScale](../../../ado/reference/ado-api/numericscale-property-ado.md), [size](../../../ado/reference/ado-api/size-property-ado-parameter.md)y [Type](../../../ado/reference/ado-api/type-property-ado.md) .  
  
-   Pase datos binarios o de caracteres largos a un parámetro con el método [AppendChunk](../../../ado/reference/ado-api/appendchunk-method-ado.md) .  
  
-   Obtener acceso a los atributos específicos del proveedor mediante la colección [Properties](../../../ado/reference/ado-api/properties-collection-ado.md) .  
  
 Si conoce los nombres y las propiedades de los parámetros asociados al procedimiento almacenado o a la consulta parametrizada a la que desea llamar, puede usar el método [CreateParameter](../../../ado/reference/ado-api/createparameter-method-ado.md) para crear objetos de **parámetro** con la configuración de propiedades adecuada y usar el método [Append](../../../ado/reference/ado-api/append-method-ado.md) para agregarlos a la colección de [parámetros](../../../ado/reference/ado-api/parameters-collection-ado.md) . Esto le permite establecer y devolver valores de parámetro sin tener que llamar al método [Refresh](../../../ado/reference/ado-api/refresh-method-ado.md) en la colección **Parameters** para recuperar la información de parámetros del proveedor, una operación que consume muchos recursos.  
  
 El objeto de **parámetro** no es seguro para el scripting.  
  
 Esta sección contiene el siguiente tema.  
  
-   [Propiedades, métodos y eventos del objeto Parameter](../../../ado/reference/ado-api/parameter-object-properties-methods-and-events.md)  
  
## <a name="see-also"></a>Consulte también  
 [Command (objeto) (ADO)](../../../ado/reference/ado-api/command-object-ado.md)   
 [CreateParameter (método) (ADO)](../../../ado/reference/ado-api/createparameter-method-ado.md)   
 [Parameters (colección) (ADO)](../../../ado/reference/ado-api/parameters-collection-ado.md)   
 [Colección de propiedades (ADO)](../../../ado/reference/ado-api/properties-collection-ado.md)
