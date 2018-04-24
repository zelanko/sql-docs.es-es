---
title: Estado de la propiedad (ADO) | Documentos de Microsoft
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: ado
ms.technology:
- drivers
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.suite: sql
ms.tgt_pltfrm: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Command25::State
helpviewer_keywords:
- State property [ADO]
ms.assetid: 0b993bac-2653-40b1-bcbb-5b57b6aae2bf
caps.latest.revision: 8
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: c3f45b4aeb9cd16a2aa166008ac46bf01f5ba9df
ms.sourcegitcommit: bb044a48a6af9b9d8edb178dc8c8bd5658b9ff68
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/18/2018
---
# <a name="state-property-ado"></a>Propiedad State (ADO)
Todos los objetos aplicables indica si el estado del objeto está abierta o cerrada. Si el objeto ejecuta un método asincrónico, indica si el estado actual del objeto es conectando, ejecutando o recuperar.  
  
## <a name="return-value"></a>Valor devuelto  
 Devuelve un **largo** valor que puede ser un [ObjectStateEnum](../../../ado/reference/ado-api/objectstateenum.md) valor. El valor predeterminado es **adStateClosed**.  
  
## <a name="remarks"></a>Comentarios  
 Puede usar el **estado** propiedad para determinar el estado actual de un objeto determinado en cualquier momento.  
  
 El objeto **estado** propiedad puede tener una combinación de valores. Por ejemplo, si se ejecuta una instrucción, esta propiedad tendrá un valor combinado de **adStateOpen** y **adStateExecuting**.  
  
 El **estado** propiedad es de solo lectura.  
  
## <a name="applies-to"></a>Se aplica a  
  
||||  
|-|-|-|  
|[Objeto Command (ADO)](../../../ado/reference/ado-api/command-object-ado.md)|[Objeto de conexión (ADO)](../../../ado/reference/ado-api/connection-object-ado.md)|[Objeto Record (ADO)](../../../ado/reference/ado-api/record-object-ado.md)|  
|[Objeto de conjunto de registros (ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)|[Objeto de secuencia (ADO)](../../../ado/reference/ado-api/stream-object-ado.md)||  
  
## <a name="see-also"></a>Vea también  
 [ConnectionString, ConnectionTimeout y ejemplo de las propiedades de estado (VB)](../../../ado/reference/ado-api/connectionstring-connectiontimeout-and-state-properties-example-vb.md)   
 [ConnectionString, ConnectionTimeout y ejemplo de las propiedades de estado (VC ++)](../../../ado/reference/ado-api/connectionstring-connectiontimeout-and-state-properties-example-vc.md)   
