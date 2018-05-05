---
title: Cancel (método) (ADO) | Documentos de Microsoft
ms.prod: sql
ms.prod_service: connectivity
ms.component: ado
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.suite: sql
ms.tgt_pltfrm: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Recordset20::Cancel
- _Record::Cancel
- _Connection::Cancel
- Command25::Cancel
- _Stream::Cancel
helpviewer_keywords:
- Cancel method [ADO]
ms.assetid: e0db4e15-6787-41e2-8f13-9e9b524d620a
caps.latest.revision: 13
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: a9538bfe7e0c98cf89c052ba3244482def661ef3
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/03/2018
---
# <a name="cancel-method-ado"></a>Cancel (método) (ADO)
Cancela la ejecución de una llamada de método asincrónico pendiente.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
object.Cancel  
```  
  
## <a name="remarks"></a>Comentarios  
 Use la **cancelar** método para finalizar la ejecución de una llamada de método asincrónico: es decir, se invoca un método con el **adAsyncConnect**, **adAsyncExecute**, o **adAsyncFetch** opción.  
  
 En la tabla siguiente se muestra qué tarea finaliza cuando se usa el **cancelar** método en un determinado tipo de objeto.  
  
|Si *objeto* es un|Finaliza la última llamada asincrónica a este método|  
|----------------------|-------------------------------------------------------------|  
|[Command](../../../ado/reference/ado-api/command-object-ado.md)|[Execute](../../../ado/reference/ado-api/execute-method-ado-command.md)|  
|[Conexión](../../../ado/reference/ado-api/connection-object-ado.md)|[Ejecutar](../../../ado/reference/ado-api/execute-method-ado-connection.md) o [abierto](../../../ado/reference/ado-api/open-method-ado-connection.md)|  
|[Registro](../../../ado/reference/ado-api/record-object-ado.md)|[CopyRecord](../../../ado/reference/ado-api/copyrecord-method-ado.md), [DeleteRecord](../../../ado/reference/ado-api/deleterecord-method-ado.md), [MoveRecord](../../../ado/reference/ado-api/moverecord-method-ado.md), o [abierto](../../../ado/reference/ado-api/open-method-ado-record.md)|  
|[Conjunto de registros](../../../ado/reference/ado-api/recordset-object-ado.md)|[Abrir](../../../ado/reference/ado-api/open-method-ado-recordset.md)|  
|[Secuencia](../../../ado/reference/ado-api/stream-object-ado.md)|[Abrir](../../../ado/reference/ado-api/open-method-ado-stream.md)|  
  
## <a name="applies-to"></a>Se aplica a  
  
||||  
|-|-|-|  
|[Objeto Command (ADO)](../../../ado/reference/ado-api/command-object-ado.md)|[Objeto de conexión (ADO)](../../../ado/reference/ado-api/connection-object-ado.md)|[Objeto Record (ADO)](../../../ado/reference/ado-api/record-object-ado.md)|  
|[Objeto de conjunto de registros (ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)|[Objeto de secuencia (ADO)](../../../ado/reference/ado-api/stream-object-ado.md)||  
  
## <a name="see-also"></a>Vea también  
 [Ejemplo del método Cancel (VB)](../../../ado/reference/ado-api/cancel-method-example-vb.md)   
 [Ejemplo del método Cancel (VBScript)](../../../ado/reference/rds-api/cancel-method-example-vbscript.md)   
 [Ejemplo del método Cancel (VC ++)](../../../ado/reference/ado-api/cancel-method-example-vc.md)   
 [Cancel (método) (RDS)](../../../ado/reference/rds-api/cancel-method-rds.md)   
 [Método CancelBatch (ADO)](../../../ado/reference/ado-api/cancelbatch-method-ado.md)   
 [Método CancelUpdate (ADO)](../../../ado/reference/ado-api/cancelupdate-method-ado.md)   
 [Método CancelUpdate (RDS)](../../../ado/reference/rds-api/cancelupdate-method-rds.md)   
 [Método Execute (Command ADO)](../../../ado/reference/ado-api/execute-method-ado-command.md)   
 [Execute (método) (conexión de ADO)](../../../ado/reference/ado-api/execute-method-ado-connection.md)   
 [Open (método) (conexión de ADO)](../../../ado/reference/ado-api/open-method-ado-connection.md)   
 [Open (método) (conjunto de registros ADO)](../../../ado/reference/ado-api/open-method-ado-recordset.md)
