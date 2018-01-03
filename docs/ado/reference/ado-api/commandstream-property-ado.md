---
title: La propiedad CommandStream (ADO) | Documentos de Microsoft
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: ado
ms.technology: drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: sql
ms.tgt_pltfrm: 
ms.topic: article
apitype: COM
f1_keywords: _Command::CommandStream
helpviewer_keywords: CommandStream property [ADO]
ms.assetid: f78f61b6-87e0-48dc-961e-83d0e20da58e
caps.latest.revision: "13"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 2d1c75a7db62475c8f717e36a93b9bf554c6248d
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 12/21/2017
---
# <a name="commandstream-property-ado"></a>Propiedad CommandStream (ADO)
Indica la secuencia que se usa como entrada para un [comando](../../../ado/reference/ado-api/command-object-ado.md) objeto.  
  
## <a name="settings-and-return-values"></a>Configuración y valores devueltos  
 Establece o devuelve la secuencia que se usa como entrada para un **comando** objeto. El formato de esta secuencia es específica del proveedor; Consulte la documentación del proveedor para obtener más información. Esta propiedad es similar a la [CommandText](../../../ado/reference/ado-api/commandtext-property-ado.md) propiedad, que se utiliza para especificar una cadena para la entrada de un **comando**.  
  
## <a name="remarks"></a>Comentarios  
 **CommandStream** y **CommandText** son mutuamente excluyentes. Cuando el usuario establece el **CommandStream** propiedad, el **CommandText** propiedad se establecerá en la cadena vacía (""). Si el usuario establece el **CommandText** propiedad, el **CommandStream** propiedad se establecerá en **nada**.  
  
 Los comportamientos de la **Command.Parameters.Refresh** y **Command.Prepare** métodos definidos por el proveedor. No se pueden actualizar los valores de parámetros en una secuencia.  
  
 El flujo de entrada no está disponible para otros objetos de ADO que devuelven el origen de un **comando**. Por ejemplo, si la [origen](../../../ado/reference/ado-api/source-property-ado-recordset.md) de un [Recordset](../../../ado/reference/ado-api/recordset-object-ado.md) está establecido en un **comando** objeto que tiene una secuencia como entrada, **Recordset.Source** continúa devolviendo el **CommandText** propiedad, que contiene una cadena vacía (""), en lugar del contenido de la secuencia de la **CommandStream** propiedad.  
  
 Cuando se utiliza una secuencia de comandos (tal y como especifica **CommandStream**), el único valor válido [CommandTypeEnum](../../../ado/reference/ado-api/commandtypeenum.md) los valores para la [CommandType](../../../ado/reference/ado-api/commandtype-property-ado.md) propiedad son  **adCmdText** y **adCmdUnknown**. Cualquier otro valor producirá un error.  
  
## <a name="applies-to"></a>Se aplica a  
 [Objeto Command (ADO)](../../../ado/reference/ado-api/command-object-ado.md)  
  
## <a name="see-also"></a>Vea también  
 [Propiedad CommandText (ADO)](../../../ado/reference/ado-api/commandtext-property-ado.md)   
 [Propiedad Dialect](../../../ado/reference/ado-api/dialect-property.md)   
 [CommandTypeEnum](../../../ado/reference/ado-api/commandtypeenum.md)
