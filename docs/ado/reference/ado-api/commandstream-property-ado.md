---
title: Propiedad CommandStream (ADO) | Microsoft Docs
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
manager: craigg
ms.openlocfilehash: b1048e8d243bd19d86d60c3c4f92e4e4b9d137a9
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/23/2019
ms.locfileid: "63267277"
---
# <a name="commandstream-property-ado"></a>Propiedad CommandStream (ADO)
Indica la secuencia que se utiliza como entrada para un [comando](../../../ado/reference/ado-api/command-object-ado.md) objeto.  
  
## <a name="settings-and-return-values"></a>Configuración y valores devueltos  
 Establece o devuelve la secuencia que se utiliza como entrada para un **comando** objeto. El formato de esta secuencia es específica del proveedor; Consulte la documentación del proveedor para obtener más información. Esta propiedad es similar a la [CommandText](../../../ado/reference/ado-api/commandtext-property-ado.md) propiedad, que se utiliza para especificar una cadena para la entrada de un **comando**.  
  
## <a name="remarks"></a>Comentarios  
 **CommandStream** y **CommandText** son mutuamente excluyentes. Cuando el usuario establece el **CommandStream** propiedad, el **CommandText** propiedad se establecerá en la cadena vacía (""). Si el usuario establece el **CommandText** propiedad, el **CommandStream** propiedad se establecerá en **nada**.  
  
 Los comportamientos de la **Command.Parameters.Refresh** y **Command.Prepare** métodos definidos por el proveedor. No se pueden actualizar los valores de parámetros en una secuencia.  
  
 El flujo de entrada no está disponible para otros objetos de ADO que devuelven el origen de un **comando**. Por ejemplo, si la [origen](../../../ado/reference/ado-api/source-property-ado-recordset.md) de un [Recordset](../../../ado/reference/ado-api/recordset-object-ado.md) está establecido en un **comando** objeto que tiene un flujo como entrada, **Recordset.Source** continúa devolviendo el **CommandText** propiedad, que contiene una cadena vacía (""), en lugar del contenido de la secuencia de la **CommandStream** propiedad.  
  
 Cuando se usa una secuencia de comandos (tal y como especifica **CommandStream**), el único valor válido [CommandTypeEnum](../../../ado/reference/ado-api/commandtypeenum.md) valores para el [CommandType](../../../ado/reference/ado-api/commandtype-property-ado.md) son propiedad  **adCmdText** y **adCmdUnknown**. Cualquier otro valor generará un error.  
  
## <a name="applies-to"></a>Se aplica a  
 [Objeto Command (ADO)](../../../ado/reference/ado-api/command-object-ado.md)  
  
## <a name="see-also"></a>Vea también  
 [Propiedad CommandText (ADO)](../../../ado/reference/ado-api/commandtext-property-ado.md)   
 [Propiedad Dialect](../../../ado/reference/ado-api/dialect-property.md)   
 [CommandTypeEnum](../../../ado/reference/ado-api/commandtypeenum.md)
