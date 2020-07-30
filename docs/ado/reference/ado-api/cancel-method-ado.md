---
title: CANCEL (método) (ADO) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
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
author: rothja
ms.author: jroth
ms.openlocfilehash: 25b6de609d286847fe7458353203dd7f4b9c7b4b
ms.sourcegitcommit: 216f377451e53874718ae1645a2611cdb198808a
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/28/2020
ms.locfileid: "87242431"
---
# <a name="cancel-method-ado"></a>Cancel (método) (ADO)
Cancela la ejecución de una llamada de método asincrónica pendiente.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
object.Cancel  
```  
  
## <a name="remarks"></a>Observaciones  
 Use el método **Cancel** para finalizar la ejecución de una llamada de método asincrónico: es decir, un método invocado con la opción **adAsyncConnect**, **adAsyncExecute**o **adAsyncFetch** .  
  
 En la tabla siguiente se muestra qué tarea se termina cuando se usa el método **Cancel** en un tipo de objeto determinado.  
  
|Si el *objeto* es un|Finalizó la última llamada asincrónica a este método|  
|----------------------|-------------------------------------------------------------|  
|[Comando](../../../ado/reference/ado-api/command-object-ado.md)|[Ejecut](../../../ado/reference/ado-api/execute-method-ado-command.md)|  
|[Connection](../../../ado/reference/ado-api/connection-object-ado.md)|[Ejecutar](../../../ado/reference/ado-api/execute-method-ado-connection.md) o [abrir](../../../ado/reference/ado-api/open-method-ado-connection.md)|  
|[Registro](../../../ado/reference/ado-api/record-object-ado.md)|[CopyRecord](../../../ado/reference/ado-api/copyrecord-method-ado.md), [DeleteRecord](../../../ado/reference/ado-api/deleterecord-method-ado.md), [MoveRecord](../../../ado/reference/ado-api/moverecord-method-ado.md)o [Open](../../../ado/reference/ado-api/open-method-ado-record.md)|  
|[DataRecordsets](../../../ado/reference/ado-api/recordset-object-ado.md)|[Abrir](../../../ado/reference/ado-api/open-method-ado-recordset.md)|  
|[Stream](../../../ado/reference/ado-api/stream-object-ado.md)|[Abrir](../../../ado/reference/ado-api/open-method-ado-stream.md)|  
  
## <a name="applies-to"></a>Se aplica a  

:::row:::
    :::column:::
        [Objeto Command (ADO)](../../../ado/reference/ado-api/command-object-ado.md)  
        [Objeto de conexión (ADO)](../../../ado/reference/ado-api/connection-object-ado.md)  
    :::column-end:::
    :::column:::
        [Objeto Record (ADO)](../../../ado/reference/ado-api/record-object-ado.md)  
        [Objeto de conjunto de registros (ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)  
    :::column-end:::
    :::column:::
        [Objeto de secuencia (ADO)](../../../ado/reference/ado-api/stream-object-ado.md)  
    :::column-end:::
:::row-end:::

## <a name="see-also"></a>Consulte también  
 [Ejemplo del método CANCEL (VB)](../../../ado/reference/ado-api/cancel-method-example-vb.md)   
 [Ejemplo del método CANCEL (VBScript)](../../../ado/reference/rds-api/cancel-method-example-vbscript.md)   
 [Ejemplo del método CANCEL (VC + +)](../../../ado/reference/ado-api/cancel-method-example-vc.md)   
 [Método CANCEL (RDS)](../../../ado/reference/rds-api/cancel-method-rds.md)   
 [CancelBatch (método) (ADO)](../../../ado/reference/ado-api/cancelbatch-method-ado.md)   
 [CancelUpdate (método) (ADO)](../../../ado/reference/ado-api/cancelupdate-method-ado.md)   
 [Método CancelUpdate (RDS)](../../../ado/reference/rds-api/cancelupdate-method-rds.md)   
 [Método execute (comando de ADO)](../../../ado/reference/ado-api/execute-method-ado-command.md)   
 [Método execute (conexión ADO)](../../../ado/reference/ado-api/execute-method-ado-connection.md)   
 [Open (método) (conexión de ADO)](../../../ado/reference/ado-api/open-method-ado-connection.md)   
 [Open (método) (conjunto de registros ADO)](../../../ado/reference/ado-api/open-method-ado-recordset.md)
