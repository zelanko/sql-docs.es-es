---
title: Evento FetchProgress (ADO) | Documentos de Microsoft
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: reference
ms.technology: drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: sql
ms.tgt_pltfrm: 
ms.topic: article
apitype: COM
f1_keywords:
- FetchProgress
- Recordset::FetchProgress
helpviewer_keywords: FetchProgress event [ADO]
ms.assetid: 301716fd-81fc-40eb-8a04-221ef7ab410e
caps.latest.revision: "11"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 990e5bbe3a203cd48c34c6153a9ee0ca8e678758
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/17/2017
---
# <a name="fetchprogress-event-ado"></a>Evento FetchProgress (ADO)
El **FetchProgress**eventos se llama periódicamente durante una operación asincrónica prolongada para informar de cuántas filas se han recuperado actualmente en el [conjunto de registros](../../../ado/reference/ado-api/recordset-object-ado.md).  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
FetchProgress Progress, MaxProgress, adStatus, pRecordset  
```  
  
#### <a name="parameters"></a>Parámetros  
 *Progreso*  
 A **largo** valor que indica el número de registros que han sido recuperados actualmente por la operación de captura.  
  
 *MaxProgress*  
 A **largo** valor que indica el número máximo de registros que se espera recuperar.  
  
 *adStatus*  
 Un [EventStatusEnum](../../../ado/reference/ado-api/eventstatusenum.md) valor de estado.  
  
 *Connection*  
 A **Recordset** objeto que es el objeto para el que se recuperan los registros.  
  
## <a name="remarks"></a>Comentarios  
 Cuando se usa **FetchProgress** con un elemento secundario **Recordset**, tenga en cuenta que la *progreso* y *MaxProgress* se derivan los valores de parámetro desde subyacente [servicio Cursor](../../../ado/guide/appendixes/microsoft-cursor-service-for-ole-db-ado-service-component.md) conjunto de filas. Los valores devueltos representan el número total de registros en el conjunto de filas subyacente, no solo el número de registros en el capítulo actual.  
  
> [!NOTE]
>  Usar **FetchProgress** con Microsoft Visual Basic, Visual Basic 6.0 o posterior es necesario.  
  
## <a name="see-also"></a>Vea también  
 [Ejemplo de modelo de eventos de ADO (VC ++)](../../../ado/reference/ado-api/ado-events-model-example-vc.md)   
 [Conexión ADO y los eventos de conjunto de registros](../../../ado/guide/data/ado-event-handler-summary.md)
