---
title: Evento WillExecute (ADO) | Documentos de Microsoft
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
- WillExecute
- Connection::WillExecute
helpviewer_keywords:
- WillExecute event [ADO]
ms.assetid: dd755e46-f589-48a3-93a9-51ff998d44b5
caps.latest.revision: 11
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 28d9fee251d53f5966f83fb1a49d3ecd75fe0813
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/03/2018
---
# <a name="willexecute-event-ado"></a>Evento WillExecute (ADO)
El **WillExecute** eventos se llama justo antes de que se ejecuta un comando pendiente en una conexión.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
WillExecute Source, CursorType, LockType, Options, adStatus, pCommand, pRecordset, pConnection  
```  
  
#### <a name="parameters"></a>Parámetros  
 *Source*  
 A **cadena** que contiene un comando SQL o un nombre de procedimiento almacenado.  
  
 *CursorType*  
 A [CursorTypeEnum](../../../ado/reference/ado-api/cursortypeenum.md) que contiene el tipo de cursor para la **Recordset** que se abrirá. Con este parámetro, puede cambiar el cursor a cualquier tipo durante una **Recordset**[Open (método) (conjunto de registros ADO)](../../../ado/reference/ado-api/open-method-ado-recordset.md) operación. *CursorType* se omitirá para cualquier otra operación.  
  
 *LockType*  
 A [LockTypeEnum](../../../ado/reference/ado-api/locktypeenum.md) que contiene el tipo de bloqueo para el **Recordset** que se abrirá. Con este parámetro, puede cambiar el bloqueo a cualquier tipo durante una **RecordsetOpen** operación. *LockType* se omitirá para cualquier otra operación.  
  
 *Opciones*  
 A **largo** valor que indica las opciones que pueden usarse para ejecutar el comando o abrir el **conjunto de registros**.  
  
 *adStatus*  
 Un [EventStatusEnum](../../../ado/reference/ado-api/eventstatusenum.md) valor de estado que puede ser **adStatusCantDeny** o **adStatusOK** cuando se llama a este evento. Si es **adStatusCantDeny**, este evento no puede solicitar la cancelación de la operación pendiente.  
  
 *pCommand*  
 El [comando ADO (objetos)](../../../ado/reference/ado-api/command-object-ado.md) el objeto para el que se aplica esta notificación de eventos.  
  
 *pRecordset*  
 El [conjunto de registros ADO (objetos)](../../../ado/reference/ado-api/recordset-object-ado.md) el objeto para el que se aplica esta notificación de eventos.  
  
 *pConnection*  
 El [conexión ADO (objetos)](../../../ado/reference/ado-api/connection-object-ado.md) el objeto para el que se aplica esta notificación de eventos.  
  
## <a name="remarks"></a>Comentarios  
 A **WillExecute** evento puede producirse debido a una conexión.  [Execute (método) (conexión de ADO)](../../../ado/reference/ado-api/execute-method-ado-connection.md), [método Execute (comando ADO)](../../../ado/reference/ado-api/execute-method-ado-command.md), o [Open (método) (conjunto de registros ADO)](../../../ado/reference/ado-api/open-method-ado-recordset.md) método la *pConnection* parámetro debe siempre contienen una referencia válida a un **conexión** objeto. Si el evento es debido a **Connection.Execute**, *Connection* y *pCommand* parámetros están establecidos en **nada**. Si el evento es debido a **Recordset.Open**, *Connection* parámetro hará referencia el **Recordset** objeto y el *pCommand* parámetro se establece en **nada**. Si el evento es debido a **Command.Execute**, *pCommand* parámetro hará referencia el **comando** objeto y el *Connection* parámetro se establece en **nada**.  
  
 **WillExecute** le permite examinar y modificar los parámetros de ejecución pendiente. Este evento puede devolver una solicitud de cancelación del comando pendiente.  
  
> [!NOTE]
>  Si la versión original de origen para un **comando** es una secuencia especificada por el [propiedad CommandStream (ADO)](../../../ado/reference/ado-api/commandstream-property-ado.md) propiedad, asignando una cadena nueva a la **WillExecute *** origen* parámetro cambia el origen de la **comando**. El **CommandStream** propiedad se borrará y [propiedad CommandText (ADO)](../../../ado/reference/ado-api/commandtext-property-ado.md) propiedad se actualizará con el nuevo origen. La secuencia original especificada por **CommandStream** se publican y no son accesibles.  
  
 Si el dialecto de la nueva cadena de origen difiere de la configuración original de la [propiedad Dialect](../../../ado/reference/ado-api/dialect-property.md) propiedad (que correspondía a la **CommandStream**), debe especificar el dialecto correcto estableciendo el **dialecto** propiedad del objeto de comando al que hace referencia *pCommand*.  
  
## <a name="see-also"></a>Vea también  
 [Ejemplo de modelo de eventos de ADO (VC ++)](../../../ado/reference/ado-api/ado-events-model-example-vc.md)   
 [Resumen del controlador de eventos de ADO](../../../ado/guide/data/ado-event-handler-summary.md)   
 [Objeto de conexión (ADO)](../../../ado/reference/ado-api/connection-object-ado.md)
