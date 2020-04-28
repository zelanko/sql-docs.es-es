---
title: Evento FetchProgress (ADO) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- FetchProgress
- Recordset::FetchProgress
helpviewer_keywords:
- FetchProgress event [ADO]
ms.assetid: 301716fd-81fc-40eb-8a04-221ef7ab410e
author: MightyPen
ms.author: genemi
ms.openlocfilehash: ab93d8117a5fb3d2bbc95ea33bbacdc7fba3f151
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/27/2020
ms.locfileid: "67932827"
---
# <a name="fetchprogress-event-ado"></a>Evento FetchProgress (ADO)
Se llama al evento **FetchProgress**periódicamente durante una operación asincrónica larga para informar del número de filas que se han recuperado actualmente en el [conjunto de registros](../../../ado/reference/ado-api/recordset-object-ado.md).  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
FetchProgress Progress, MaxProgress, adStatus, pRecordset  
```  
  
#### <a name="parameters"></a>Parámetros  
 *Progress*  
 Un valor **largo** que indica el número de registros que ha recuperado actualmente la operación de captura.  
  
 *MaxProgress*  
 Un valor **largo** que indica el número máximo de registros que se espera que se recuperen.  
  
 *adStatus*  
 Valor de estado de [EventStatusEnum](../../../ado/reference/ado-api/eventstatusenum.md) .  
  
 *pRecordset*  
 Objeto de **conjunto de registros** que es el objeto para el que se recuperan los registros.  
  
## <a name="remarks"></a>Observaciones  
 Al usar **FetchProgress** con un **conjunto de registros**secundario, tenga en cuenta que los valores de los parámetros *Progress* y *MaxProgress* se derivan del conjunto de filas del [servicio de cursor](../../../ado/guide/appendixes/microsoft-cursor-service-for-ole-db-ado-service-component.md) subyacente. Los valores devueltos representan el número total de registros del conjunto de filas subyacente, no solo el número de registros del capítulo actual.  
  
> [!NOTE]
>  Para usar **FetchProgress** con Microsoft Visual Basic, se requiere Visual Basic 6,0 o posterior.  
  
## <a name="see-also"></a>Consulte también  
 [Ejemplo de modelo de eventos de ADO (VC + +)](../../../ado/reference/ado-api/ado-events-model-example-vc.md)   
 [Conexión ADO y los eventos de conjunto de registros](../../../ado/guide/data/ado-event-handler-summary.md)
