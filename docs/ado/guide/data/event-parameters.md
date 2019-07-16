---
title: Parámetros de evento | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- Error parameter [ADO]
- Object parameter [ADO]
- Status parameter [ADO]
- events [ADO], parameters
- Reason parameter [ADO]
- event parameters [ADO]
ms.assetid: bd5c5afa-d301-4899-acda-40f98a6afa4d
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 26caf2b54b4f0affbbe7cdc58fa2bf742f0d4101
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/15/2019
ms.locfileid: "67925366"
---
# <a name="event-parameters"></a>Parámetros de eventos
Cada controlador de eventos tiene un parámetro de estado que controla el controlador de eventos. Para los eventos de finalización, este parámetro también se utiliza para indicar el éxito o fracaso de la operación que generó el evento. Eventos más completos también tienen un parámetro de error para proporcionar información sobre los errores que pudieran haberse producido y uno o más parámetros de objeto que hacen referencia a los objetos ADO que se usa para realizar la operación. Por ejemplo, el [ExecuteComplete](../../../ado/reference/ado-api/executecomplete-event-ado.md) evento incluye parámetros de objeto para el **comando**, **Recordset**, y **conexión** objetos asociado al evento. En el siguiente ejemplo de Microsoft® Visual Basic®, puede ver los objetos pCommand, Connection y pConnection los objetos que representan el **comando**, **Recordset**, y **conexión** objetos utilizados por el **Execute** método.  
  
```  
Private Sub connEvent_ExecuteComplete(ByVal RecordsAffected As Long, _  
     ByVal pError As ADODB.Error, _  
     adStatus As ADODB.EventStatusEnum, _  
     ByVal pCommand As ADODB.Command, _  
     ByVal pRecordset As ADODB.Recordset, _  
     ByVal pConnection As ADODB.Connection)  
```  
  
 Excepto para el **Error** objeto, los mismos parámetros se pasan a los eventos Will. Esto le permite examinar cada uno de los objetos que se usará en la operación pendiente y determinan si se debe permitir la operación finalice.  
  
 Algunos controladores de eventos tienen un *motivo* parámetro, que proporciona información adicional acerca de por qué se produjo el evento. Por ejemplo, el **WillMove** y **MoveComplete** los eventos pueden producirse debido a uno de los métodos de navegación (**MoveNext**, **MovePrevious**, y así sucesivamente) llamado o como el resultado de una nueva consulta.  
  
## <a name="status-parameter"></a>Parámetro de estado  
 Cuando se llama a la rutina de controlador de eventos, el *estado* parámetro se establece en uno de los siguientes valores.  
  
|Valor|Descripción|  
|-----------|-----------------|  
|**adStatusOK**|Pasa a la usará y eventos de finalización. Este valor significa que la operación que provocó el evento que se completó correctamente.|  
|**adStatusErrorsOccurred**|Se pasa a solo eventos de finalización. Este valor significa que la operación que provocó el evento se realizó correctamente, o un evento Will canceló la operación. Compruebe el *Error* parámetro para obtener más detalles.|  
|**adStatusCantDeny**|Pasan solo a voluntad. Este valor significa que la operación no se puede cancelar el evento de voluntad. Deben realizarse.|  
  
 Si se determina en el evento Will que la operación debe continuar, deje el *estado* parámetro sin modificar. Siempre y cuando no se estableció el parámetro de estado entrante **adStatusCantDeny**, sin embargo, puede cancelar la operación pendiente cambiando *estado* a **adStatusCancel**. Al hacerlo, el evento Complete asociado a la operación tiene su *estado* parámetro establecido en **adStatusErrorsOccurred**. El **Error** objeto pasado al evento Complete contendrá el valor **adErrOperationCancelled**.  
  
 Si ya no desea procesar un evento, puede establecer *estado* a **adStatusUnwantedEvent** y la aplicación ya no recibirá notificación de ese evento. Sin embargo, recuerde que algunos eventos se pueden generar más de uno de los motivos. En ese caso, debe especificar **adStatusUnwantedEvent** para todas las razones posibles. Por ejemplo, para dejar de recibir notificación pendiente **RecordChange** eventos, debe establecer el *estado* parámetro **adStatusUnwantedEvent** para  **adRsnAddNew**, **adRsnDelete**, **adRsnUpdate**, **adRsnUndoUpdate**, **adRsnUndoAddNew**, **adRsnUndoDelete**, y **adRsnFirstChange** cuando se producen.  
  
|Valor|Descripción|  
|-----------|-----------------|  
|**adStatusUnwantedEvent**|La solicitud que este controlador de eventos deje de recibir notificaciones.|  
|**adStatusCancel**|Solicitar la cancelación de la operación que está a punto de producirse.|  
  
## <a name="error-parameter"></a>Parámetro de error  
 El *Error* parámetro es una referencia a ADO [Error](../../../ado/reference/ado-api/error-object.md) objeto. Cuando el *estado* parámetro está establecido en **adStatusErrorsOccurred**, **Error** objeto contiene detalles sobre el motivo del error de la operación. Si el evento Will asociado a un evento Complete ha cancelado la operación estableciendo el *estado* parámetro **adStatusCancel**, el objeto de error siempre se establece en  **adErrOperationCancelled**.  
  
## <a name="object-parameter"></a>Parámetro de objeto  
 Cada evento recibe uno o más objetos que representan los objetos que están implicados en la operación. Por ejemplo, el **ExecuteComplete** evento recibe un **comando** objeto, un **Recordset** objeto y un **conexión** objeto.  
  
## <a name="reason-parameter"></a>Parámetro Reason  
 El *motivo* parámetro, *adReason*, proporciona información adicional sobre por qué se produjo el evento. Los eventos con un *adReason* parámetro puede llamarse varias veces, incluso para la misma operación por un motivo distinto cada vez. Por ejemplo, el **WillChangeRecord** se llama al controlador de eventos para las operaciones que se van a realizar o deshacer la inserción, eliminación o modificación de un registro. Si desea que procese un evento solo cuando se produce por una razón determinada, puede usar el *adReason* parámetro para filtrar las repeticiones que no le interesa. Por ejemplo, si desea procesar los eventos de cambio de registro solo cuando se producen porque se ha agregado un registro, puede usar algo similar al siguiente.  
  
```  
' BeginEventExampleVB01  
Private Sub rsTest_WillChangeRecord(ByVal adReason As ADODB.EventReasonEnum, ByVal cRecords As Long, adStatus As ADODB.EventStatusEnum, ByVal pRecordset As ADODB.Recordset)  
   If adReason = adRsnAddNew Then  
       ' Process event  
       '...  
   Else  
       ' Cancel event notification for all  
       ' other possible adReason values.  
       adStatus = adStatusUnwantedEvent  
   End If  
End Sub  
' EndEventExampleVB01  
```  
  
 En este caso, la notificación potencialmente puede producirse para cada uno de los otros motivos. Sin embargo, se producirá una sola vez por cada razón. Después de la notificación se ha producido una vez por cada razón, recibirá notificación solo para la adición de un nuevo registro.  
  
 En cambio, deberá establecer *adStatus* a **adStatusUnwantedEvent** solo una vez para solicitar que un controlador de eventos sin una **adReason** receptora evento de detención de parámetro notificaciones.  
  
## <a name="see-also"></a>Vea también  
 [Resumen del controlador de eventos de ADO](../../../ado/guide/data/ado-event-handler-summary.md)   
 [Creación de instancias de eventos de ADO por idioma](../../../ado/guide/data/ado-event-instantiation-by-language.md)   
 [Cómo funcionan conjuntamente los controladores de eventos](../../../ado/guide/data/how-event-handlers-work-together.md)   
 [Tipos de eventos](../../../ado/guide/data/types-of-events.md)
