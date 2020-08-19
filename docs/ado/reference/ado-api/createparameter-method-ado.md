---
description: Método CreateParameter (ADO)
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
author: rothja
ms.author: jroth
ms.openlocfilehash: 6bf45e2d458784972d7057e95878c9db3526ffac
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/17/2020
ms.locfileid: "88444327"
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
  
 *Dirección*  
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
