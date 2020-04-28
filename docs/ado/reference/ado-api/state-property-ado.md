---
title: Propiedad State (ADO) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Command25::State
helpviewer_keywords:
- State property [ADO]
ms.assetid: 0b993bac-2653-40b1-bcbb-5b57b6aae2bf
author: MightyPen
ms.author: genemi
ms.openlocfilehash: c45b9331ddd538cdf23a57eaf39b6efb71bccc4a
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/27/2020
ms.locfileid: "67930853"
---
# <a name="state-property-ado"></a>Propiedad State (ADO)
Indica para todos los objetos aplicables si el estado del objeto es abierto o cerrado. Si el objeto está ejecutando un método asincrónico, indica si el estado actual del objeto es conexión, ejecución o recuperación.  
  
## <a name="return-value"></a>Valor devuelto  
 Devuelve un valor de **tipo Long** que puede ser un valor de [ObjectStateEnum](../../../ado/reference/ado-api/objectstateenum.md) . El valor predeterminado es **adStateClosed**.  
  
## <a name="remarks"></a>Observaciones  
 Puede utilizar la propiedad **State** para determinar el estado actual de un objeto determinado en cualquier momento.  
  
 La propiedad de **Estado** del objeto puede tener una combinación de valores. Por ejemplo, si se está ejecutando una instrucción, esta propiedad tendrá un valor combinado de **adStateOpen** y **adStateExecuting**.  
  
 La propiedad **State** es de solo lectura.  
  
## <a name="applies-to"></a>Se aplica a  
  
||||  
|-|-|-|  
|[Objeto Command (ADO)](../../../ado/reference/ado-api/command-object-ado.md)|[Objeto de conexión (ADO)](../../../ado/reference/ado-api/connection-object-ado.md)|[Objeto Record (ADO)](../../../ado/reference/ado-api/record-object-ado.md)|  
|[Objeto de conjunto de registros (ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)|[Objeto de secuencia (ADO)](../../../ado/reference/ado-api/stream-object-ado.md)||  
  
## <a name="see-also"></a>Consulte también  
 [Ejemplo de las propiedades ConnectionString, ConnectionTimeout y State (VB)](../../../ado/reference/ado-api/connectionstring-connectiontimeout-and-state-properties-example-vb.md)   
 [Ejemplo de las propiedades ConnectionString, ConnectionTimeout y State (VC + +)](../../../ado/reference/ado-api/connectionstring-connectiontimeout-and-state-properties-example-vc.md)   
