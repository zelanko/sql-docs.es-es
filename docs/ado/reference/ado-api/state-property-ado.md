---
title: Estado (propiedad, ADO) | Microsoft Docs
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
manager: craigg
ms.openlocfilehash: 98d3e61b37eb22ebaf793252f49b2b11621abd80
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/01/2018
ms.locfileid: "47659363"
---
# <a name="state-property-ado"></a>Propiedad State (ADO)
Todos los objetos aplicables indica si el estado del objeto está abierto o cerrado. Si el objeto está ejecutando un método asincrónico, indica si el estado actual del objeto se conecta, ejecutar o recuperar.  
  
## <a name="return-value"></a>Valor devuelto  
 Devuelve un **largo** valor que puede ser un [ObjectStateEnum](../../../ado/reference/ado-api/objectstateenum.md) valor. El valor predeterminado es **adStateClosed**.  
  
## <a name="remarks"></a>Comentarios  
 Puede usar el **estado** propiedad para determinar el estado actual de un objeto determinado en cualquier momento.  
  
 El objeto **estado** propiedad puede tener una combinación de valores. Por ejemplo, si está ejecutando una instrucción, esta propiedad tendrá un valor combinado de **adStateOpen** y **adStateExecuting**.  
  
 El **estado** propiedad es de solo lectura.  
  
## <a name="applies-to"></a>Se aplica a  
  
||||  
|-|-|-|  
|[Objeto Command (ADO)](../../../ado/reference/ado-api/command-object-ado.md)|[Objeto de conexión (ADO)](../../../ado/reference/ado-api/connection-object-ado.md)|[Objeto Record (ADO)](../../../ado/reference/ado-api/record-object-ado.md)|  
|[Objeto de conjunto de registros (ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)|[Objeto de secuencia (ADO)](../../../ado/reference/ado-api/stream-object-ado.md)||  
  
## <a name="see-also"></a>Vea también  
 [ConnectionString, ConnectionTimeout y ejemplo de las propiedades de estado (VB)](../../../ado/reference/ado-api/connectionstring-connectiontimeout-and-state-properties-example-vb.md)   
 [ConnectionString, ConnectionTimeout y ejemplo de las propiedades de estado (VC ++)](../../../ado/reference/ado-api/connectionstring-connectiontimeout-and-state-properties-example-vc.md)   
