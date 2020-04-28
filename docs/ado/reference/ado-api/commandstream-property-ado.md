---
title: CommandStream (propiedad, ADO) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- _Command::CommandStream
helpviewer_keywords:
- CommandStream property [ADO]
ms.assetid: f78f61b6-87e0-48dc-961e-83d0e20da58e
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 23ec65380bfea16d38f02cab0a070ab69f85d525
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/27/2020
ms.locfileid: "67919745"
---
# <a name="commandstream-property-ado"></a>Propiedad CommandStream (ADO)
Indica la secuencia que se usa como entrada para un objeto de [comando](../../../ado/reference/ado-api/command-object-ado.md) .  
  
## <a name="settings-and-return-values"></a>Configuración y valores devueltos  
 Establece o devuelve la secuencia que se usa como entrada para un objeto de **comando** . El formato de esta secuencia es específico del proveedor; Consulte la documentación del proveedor para obtener más información. Esta propiedad es similar a la propiedad [CommandText](../../../ado/reference/ado-api/commandtext-property-ado.md) , que se usa para especificar una cadena para la entrada de un **comando**.  
  
## <a name="remarks"></a>Observaciones  
 **CommandStream** y **CommandText** son mutuamente excluyentes. Cuando el usuario establece la propiedad **CommandStream** , la propiedad **CommandText** se establecerá en la cadena vacía (""). Si el usuario establece la propiedad **CommandText** , la propiedad **CommandStream** se establecerá en **Nothing**.  
  
 El proveedor define los comportamientos de los métodos **Command. Parameters. Refresh** y **Command. Prepare** . No se pueden actualizar los valores de los parámetros de una secuencia.  
  
 El flujo de entrada no está disponible para otros objetos ADO que devuelven el origen de un **comando**. Por ejemplo, si el [origen](../../../ado/reference/ado-api/source-property-ado-recordset.md) de un [conjunto de registros](../../../ado/reference/ado-api/recordset-object-ado.md) se establece en un objeto de **comando** que tiene una secuencia como su entrada, **Recordset. Source** continúa devolviendo la propiedad **CommandText** , que contiene una cadena vacía (""), en lugar del contenido de la secuencia de la propiedad **CommandStream** .  
  
 Cuando se usa una secuencia de comandos (tal y como se especifica en **CommandStream**), los únicos valores de [CommandTypeEnum](../../../ado/reference/ado-api/commandtypeenum.md) válidos para la propiedad [CommandType](../../../ado/reference/ado-api/commandtype-property-ado.md) son **adCmdText** y **adCmdUnknown**. Cualquier otro valor generará un error.  
  
## <a name="applies-to"></a>Se aplica a  
 [Objeto Command (ADO)](../../../ado/reference/ado-api/command-object-ado.md)  
  
## <a name="see-also"></a>Consulte también  
 [CommandText (propiedad, ADO)](../../../ado/reference/ado-api/commandtext-property-ado.md)   
 [Propiedad Dialect](../../../ado/reference/ado-api/dialect-property.md)   
 [CommandTypeEnum](../../../ado/reference/ado-api/commandtypeenum.md)
