---
title: Evento WillExecute (ADO) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- WillExecute
- Connection::WillExecute
helpviewer_keywords:
- WillExecute event [ADO]
ms.assetid: dd755e46-f589-48a3-93a9-51ff998d44b5
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: 571c63e0b8e06c08fb066c3bb6b2d42a019895e5
ms.sourcegitcommit: 074d44994b6e84fe4552ad4843d2ce0882b92871
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/05/2019
ms.locfileid: "66710035"
---
# <a name="willexecute-event-ado"></a>Evento WillExecute (ADO)
El **WillExecute** eventos se llama justo antes de que se ejecuta un comando pendiente en una conexión.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
WillExecute Source, CursorType, LockType, Options, adStatus, pCommand, pRecordset, pConnection  
```  
  
#### <a name="parameters"></a>Parámetros  
 *Source*  
 Un **cadena** que contiene un comando SQL o un nombre de procedimiento almacenado.  
  
 *CursorType*  
 Un [CursorTypeEnum](../../../ado/reference/ado-api/cursortypeenum.md) que contiene el tipo de cursor para el **Recordset** que se va a abrir. Con este parámetro, puede cambiar el cursor a cualquier tipo durante un **Recordset**[método Open (ADO Recordset)](../../../ado/reference/ado-api/open-method-ado-recordset.md) operación. *CursorType* se omitirá para cualquier otra operación.  
  
 *LockType*  
 Un [LockTypeEnum](../../../ado/reference/ado-api/locktypeenum.md) que contiene el tipo de bloqueo para el **Recordset** que se va a abrir. Con este parámetro, puede cambiar el bloqueo a cualquier tipo durante un **RecordsetOpen** operación. *LockType* se omitirá para cualquier otra operación.  
  
 *Opciones*  
 Un **largo** valor que indica las opciones que pueden usarse para ejecutar el comando o abrir el **Recordset**.  
  
 *adStatus*  
 Un [EventStatusEnum](../../../ado/reference/ado-api/eventstatusenum.md) valor de estado que puede ser **adStatusCantDeny** o **adStatusOK** cuando se llama a este evento. Si es **adStatusCantDeny**, este evento no puede solicitar la cancelación de la operación pendiente.  
  
 *pCommand*  
 El [comando ADO (objetos)](../../../ado/reference/ado-api/command-object-ado.md) el objeto para el que se aplica esta notificación de eventos.  
  
 *pRecordset*  
 El [conjunto de registros ADO (objetos)](../../../ado/reference/ado-api/recordset-object-ado.md) el objeto para el que se aplica esta notificación de eventos.  
  
 *pConnection*  
 El [conexión ADO (objetos)](../../../ado/reference/ado-api/connection-object-ado.md) el objeto para el que se aplica esta notificación de eventos.  
  
## <a name="remarks"></a>Comentarios  
 Un **WillExecute** evento puede producirse debido a una conexión.  [Ejecutar el método (conexión de ADO)](../../../ado/reference/ado-api/execute-method-ado-connection.md), [método Execute (Command ADO)](../../../ado/reference/ado-api/execute-method-ado-command.md), o [método Open (ADO Recordset)](../../../ado/reference/ado-api/open-method-ado-recordset.md) método la *pConnection* parámetro debería siempre contienen una referencia válida a un **conexión** objeto. Si el evento es debido a **Connection.Execute**, *Connection* y *pCommand* parámetros están establecidos en **nada**. Si el evento es debido a **Recordset.Open**, el *Connection* parámetro hará referencia el **Recordset** objeto y el *pCommand* parámetro se establece en **nada**. Si el evento es debido a **Command.Execute**, el *pCommand* parámetro hará referencia el **comando** objeto y el *Connection* parámetro se establece en **nada**.  
  
 **WillExecute** le permite examinar y modificar los parámetros de ejecución pendiente. Este evento puede devolver una solicitud de cancelación del comando pendiente.  
  
> [!NOTE]
>  Si la versión original de origen para un **comando** es una secuencia especificada por el [propiedad CommandStream (ADO)](../../../ado/reference/ado-api/commandstream-property-ado.md) propiedad, asignando una cadena nueva a la **WillExecute** _Origen_ parámetro cambia el origen de la **comando**. El **CommandStream** propiedad se borrará y [propiedad CommandText (ADO)](../../../ado/reference/ado-api/commandtext-property-ado.md) propiedad se actualizará con el nuevo origen. La secuencia original especificada por **CommandStream** se publicará y no es accesible.  
  
 Si el dialecto de la nueva cadena de origen difiere de la configuración original de la [propiedad Dialect](../../../ado/reference/ado-api/dialect-property.md) propiedad (que correspondía a la **CommandStream**), se debe especificar el dialecto correcto estableciendo el **dialecto** propiedad del objeto de comando al que hace referencia *pCommand*.  
  
## <a name="see-also"></a>Vea también  
 [Ejemplo de modelo de eventos de ADO (VC ++)](../../../ado/reference/ado-api/ado-events-model-example-vc.md)   
 [Resumen del controlador de eventos de ADO](../../../ado/guide/data/ado-event-handler-summary.md)   
 [Objeto de conexión (ADO)](../../../ado/reference/ado-api/connection-object-ado.md)
