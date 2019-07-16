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
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/15/2019
ms.locfileid: "67932827"
---
# <a name="fetchprogress-event-ado"></a>Evento FetchProgress (ADO)
El **FetchProgress**se llama al evento periódicamente durante una operación asincrónica prolongada para informar de cuántas filas se han recuperado actualmente en el [Recordset](../../../ado/reference/ado-api/recordset-object-ado.md).  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
FetchProgress Progress, MaxProgress, adStatus, pRecordset  
```  
  
#### <a name="parameters"></a>Parámetros  
 *Progreso*  
 Un **largo** valor que indica el número de registros que actualmente se han recuperado por la operación de búsqueda.  
  
 *MaxProgress*  
 Un **largo** valor que indica el número máximo de registros que se espera recuperar.  
  
 *adStatus*  
 Un [EventStatusEnum](../../../ado/reference/ado-api/eventstatusenum.md) valor de estado.  
  
 *pRecordset*  
 Un **Recordset** objeto que es el objeto para el que se están recuperando los registros.  
  
## <a name="remarks"></a>Comentarios  
 Cuando se usa **FetchProgress** con un elemento secundario **Recordset**, tenga en cuenta que el *progreso* y *MaxProgress* derivan los valores de parámetro subyacente [Cursor servicio](../../../ado/guide/appendixes/microsoft-cursor-service-for-ole-db-ado-service-component.md) conjunto de filas. Los valores devueltos representan el número total de registros en el conjunto de filas subyacente, no solo el número de registros en el capítulo actual.  
  
> [!NOTE]
>  Para usar **FetchProgress** con Microsoft Visual Basic, Visual Basic 6.0 o posterior es necesario.  
  
## <a name="see-also"></a>Vea también  
 [Ejemplo de modelo de eventos de ADO (VC ++)](../../../ado/reference/ado-api/ado-events-model-example-vc.md)   
 [Conexión ADO y los eventos de conjunto de registros](../../../ado/guide/data/ado-event-handler-summary.md)
