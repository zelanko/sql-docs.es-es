---
title: CreateParameter (método) (ADO) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Command15::raw_CreateParameter
- Command15::CreateParameter
helpviewer_keywords:
- CreateParameter method [RDS]
ms.assetid: 9666fdcc-0544-4ed7-a97b-c415f2a56d7e
author: MightyPen
ms.author: genemi
ms.openlocfilehash: af796c36bd2960730536ec07ac49614876311e84
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/08/2020
ms.locfileid: "67933298"
---
# <a name="createparameter-method-ado"></a>Método CreateParameter (ADO)
Crea un nuevo objeto de [parámetro](../../../ado/reference/ado-api/parameter-object.md) con las propiedades especificadas.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
Set parameter = command.CreateParameter (Name, Type, Direction, Size, Value)  
```  
  
## <a name="return-value"></a>Valor devuelto  
 Devuelve un objeto de **parámetro** .  
  
#### <a name="parameters"></a>Parámetros  
 *Nombre*  
 Opcional. Valor de **cadena** que contiene el nombre del objeto de **parámetro** .  
  
 *Tipo*  
 Opcional. Valor de [DataTypeEnum](../../../ado/reference/ado-api/datatypeenum.md) que especifica el tipo de datos del objeto de **parámetro** .  
  
 *Direcciona*  
 Opcional. Valor [ParameterDirectionEnum](../../../ado/reference/ado-api/parameterdirectionenum.md) que especifica el tipo de objeto de **parámetro** .  
  
 *Tamaño*  
 Opcional. Valor de **tipo Long** que especifica la longitud máxima del valor del parámetro en caracteres o bytes.  
  
 *Valor*  
 Opcional. **Variante** que especifica el valor del objeto de **parámetro** .  
  
## <a name="remarks"></a>Observaciones  
 Use el método **CreateParameter** para crear un nuevo objeto de **parámetro** con el nombre, el tipo, la dirección, el tamaño y el valor especificados. Los valores que se pasan en los argumentos se escriben en las propiedades de **parámetro** correspondientes.  
  
 Este método no anexa automáticamente el objeto de **parámetro** a la colección **Parameters** de un objeto [Command](../../../ado/reference/ado-api/command-object-ado.md) . Esto le permite establecer propiedades adicionales cuyos valores se validarán ADO al anexar el objeto de **parámetro** a la colección.  
  
 Si especifica un tipo de datos de longitud variable en el argumento de *tipo* , debe pasar un argumento de *tamaño* o establecer la propiedad [size](../../../ado/reference/ado-api/size-property-ado-parameter.md) del objeto de **parámetro** antes de anexarlo a la colección **Parameters** ; de lo contrario, se produce un error.  
  
 Si especifica un tipo de datos numérico (**adNumeric** o **adDecimal**) en el argumento de *tipo* , también debe establecer las propiedades [NumericScale](../../../ado/reference/ado-api/numericscale-property-ado.md) y [Precision](../../../ado/reference/ado-api/precision-property-ado.md) .  
  
## <a name="applies-to"></a>Se aplica a  
 [Objeto Command (ADO)](../../../ado/reference/ado-api/command-object-ado.md)  
  
## <a name="see-also"></a>Consulte también  
 [Ejemplo de los métodos Append y CreateParameter (VB)](../../../ado/reference/ado-api/append-and-createparameter-methods-example-vb.md)   
 [Ejemplo de los métodos Append y CreateParameter (VC + +)](../../../ado/reference/ado-api/append-and-createparameter-methods-example-vc.md)   
 [Append (método) (ADO)](../../../ado/reference/ado-api/append-method-ado.md)   
 [Parameter (objeto)](../../../ado/reference/ado-api/parameter-object.md)   
 [Colección de parámetros (ADO)](../../../ado/reference/ado-api/parameters-collection-ado.md)
