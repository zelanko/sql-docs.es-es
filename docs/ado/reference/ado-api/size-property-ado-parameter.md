---
title: Cambiar el tamaño de propiedad (parámetro de ADO) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- _Parameter::Size
helpviewer_keywords:
- Size property [ADO Parameter]
ms.assetid: e6bad449-ebdb-4dd3-886a-9e6f1e7ee5d2
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 682a7aa30596af8a3727eec0daaba4e9fd412ac4
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/23/2019
ms.locfileid: "63192839"
---
# <a name="size-property-ado-parameter"></a>Propiedad Size (parámetro de ADO)
Indica el tamaño máximo, en bytes o caracteres, de un [parámetro](../../../ado/reference/ado-api/parameter-object.md) objeto.  
  
## <a name="settings-and-return-values"></a>Configuración y valores devueltos  
 Establece o devuelve un **largo** valor que indica el tamaño máximo en bytes o caracteres de un valor en un **parámetro** objeto.  
  
## <a name="remarks"></a>Comentarios  
 Use la **tamaño** propiedad para determinar el tamaño máximo de valores escritos en o leer desde el [valor](../../../ado/reference/ado-api/value-property-ado.md) propiedad de un **parámetro** objeto.  
  
 Si se especifica un tipo de datos de longitud variable para un **parámetro** objeto (por ejemplo, cualquier **cadena** escriba, por ejemplo, **parámetros**), debe establecer el objeto  **Tamaño** propiedad antes de agregarlo a la [parámetros](../../../ado/reference/ado-api/parameters-collection-ado.md) colección; en caso contrario, se produce un error.  
  
 Si ya se ha anexado el **parámetro** de objeto para el **parámetros** colección de un [comando](../../../ado/reference/ado-api/command-object-ado.md) objeto y cambia su tipo a un tipo de datos de longitud variable, debe establecer el **parámetro** del objeto **tamaño** propiedad antes de ejecutar el **comando** objeto; en caso contrario, se produce un error.  
  
 Si usas el [actualizar](../../../ado/reference/ado-api/refresh-method-ado.md) método para obtener información de parámetros desde el proveedor y devuelve uno o varios tipos de datos de longitud variable **parámetro** objetos, ADO puede asignar memoria para los parámetros de acuerdo en su tamaño potencial máximo, que podría producirse un error durante la ejecución. Para evitar un error, debe establecer explícitamente el **tamaño** propiedad de estos parámetros antes de ejecutar el comando.  
  
 El **tamaño** propiedad es de lectura/escritura.  
  
## <a name="applies-to"></a>Se aplica a  
 [Objeto Parameter](../../../ado/reference/ado-api/parameter-object.md)  
  
## <a name="see-also"></a>Vea también  
 [ActiveConnection, CommandText, CommandTimeout, CommandType, tamaño y ejemplo de propiedades de dirección (VB)](../../../ado/reference/ado-api/activeconnection-commandtext-commandtimeout-commandtype-size-example-vb.md)   
 [ActiveConnection, CommandText, CommandTimeout, CommandType, tamaño y ejemplo de propiedades de dirección (VC ++)](../../../ado/reference/ado-api/activeconnection-commandtext-commandtimeout-commandtype-size-example-vc.md)   
 [ActiveConnection, CommandText, CommandTimeout, CommandType, tamaño y ejemplo de propiedades de dirección (JScript)](../../../ado/reference/ado-api/activeconnection-commandtext-timeout-type-size-example-jscript.md)   
 [Propiedad Size (Stream de ADO)](../../../ado/reference/ado-api/size-property-ado-stream.md)
