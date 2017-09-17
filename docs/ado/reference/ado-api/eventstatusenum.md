---
title: EventStatusEnum | Documentos de Microsoft
ms.prod: sql-non-specified
ms.technology:
- drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: 
ms.tgt_pltfrm: 
ms.topic: article
apitype: COM
f1_keywords:
- EventStatusEnum
helpviewer_keywords:
- EventStatusEnum enumeration [ADO]
ms.assetid: ebfd4cda-4017-4873-9d28-38b1c7db12a8
caps.latest.revision: 11
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 2e0b963373521b7d981e192dbbfc94d5fe008bf6
ms.contentlocale: es-es
ms.lasthandoff: 09/09/2017

---
# <a name="eventstatusenum"></a>EventStatusEnum
Especifica el estado actual de la ejecución de un evento.  
  
|Constante|Valor|Description|  
|--------------|-----------|-----------------|  
|**adStatusCancel**|4|Solicita la cancelación de la operación que provocó que se produzca el evento.|  
|**adStatusCantDeny**|3|Indica que la operación no puede solicitar la cancelación de la operación pendiente.|  
|**adStatusErrorsOccurred**|2|Indica que la operación que provocó el evento ha fallado debido a un error o errores.|  
|**adStatusOK**|1|Indica que la operación que provocó el evento se realizó correctamente.|  
|**adStatusUnwantedEvent**|5|Impide posibles notificaciones posteriores antes de que el método de evento ha terminado de ejecutarse.|  
  
## <a name="adowfc-equivalent"></a>Equivalente ADO/WFC  
 Paquete: **com.ms.wfc.data**  
  
|Constante|  
|--------------|  
|AdoEnums.EventStatus.CANCEL|  
|AdoEnums.EventStatus.CANTDENY|  
|AdoEnums.EventStatus.ERRORSOCCURRED|  
|AdoEnums.EventStatus.OK|  
|AdoEnums.EventStatus.UNWANTEDEVENT|  
  
## <a name="applies-to"></a>Se aplica a  
  
||||  
|-|-|-|  
|[Eventos BeginTransComplete, CommitTransComplete y RollbackTransComplete eventos (ADO)](../../../ado/reference/ado-api/begintranscomplete-committranscomplete-and-rollbacktranscomplete-events-ado.md)|[ConnectComplete y eventos (ADO) de desconexión](../../../ado/reference/ado-api/connectcomplete-and-disconnect-events-ado.md)|[Evento EndOfRecordset (ADO)](../../../ado/reference/ado-api/endofrecordset-event-ado.md)|  
|[Evento ExecuteComplete (ADO)](../../../ado/reference/ado-api/executecomplete-event-ado.md)|[Evento FetchComplete (ADO)](../../../ado/reference/ado-api/fetchcomplete-event-ado.md)|[Evento InfoMessage (ADO)](../../../ado/reference/ado-api/infomessage-event-ado.md)|  
|[Eventos WillChangeField y FieldChangeComplete (ADO)](../../../ado/reference/ado-api/willchangefield-and-fieldchangecomplete-events-ado.md)|[Eventos WillChangeRecord y RecordChangeComplete (ADO)](../../../ado/reference/ado-api/willchangerecord-and-recordchangecomplete-events-ado.md)|[Eventos WillChangeRecordset y RecordsetChangeComplete (ADO)](../../../ado/reference/ado-api/willchangerecordset-and-recordsetchangecomplete-events-ado.md)|  
|[Evento WillConnect (ADO)](../../../ado/reference/ado-api/willconnect-event-ado.md)|[Evento WillExecute (ADO)](../../../ado/reference/ado-api/willexecute-event-ado.md)|[Eventos WillMove y MoveComplete (ADO)](../../../ado/reference/ado-api/willmove-and-movecomplete-events-ado.md)|
