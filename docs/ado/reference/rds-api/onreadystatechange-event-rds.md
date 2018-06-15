---
title: onReadyStateChange eventos (RDS) | Documentos de Microsoft
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.suite: sql
ms.tgt_pltfrm: ''
ms.topic: conceptual
apitype: COM
helpviewer_keywords:
- onReadyStateChange event [ADO]
ms.assetid: bf2ae3ac-bfe4-4709-b50a-ea7c282c3164
caps.latest.revision: 16
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 66de98fbc8c78b194ce41f0f26bb5f1ed6c351c2
ms.sourcegitcommit: 62826c291db93c9017ae219f75c3cfeb8140bf06
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/11/2018
ms.locfileid: "35288129"
---
# <a name="onreadystatechange-event-rds"></a>onReadyStateChange (evento, RDS)
El **onReadyStateChange** eventos se llama cada vez que el valor de la [ReadyState](../../../ado/reference/rds-api/readystate-property-rds.md) cambios de propiedad.  
  
> [!IMPORTANT]
>  A partir de Windows 8 y Windows Server 2012, componentes de servidor RDS ya no están incluidos en el sistema operativo Windows (consulte Windows 8 y [Windows Server 2012 Compatibility Cookbook](https://www.microsoft.com/en-us/download/details.aspx?id=27416) para obtener más detalles). Componentes de cliente RDS se quitará en una versión futura de Windows. Evite utilizar esta característica en nuevos trabajos de desarrollo y tenga previsto modificar las aplicaciones que actualmente la utilizan. Las aplicaciones que utilizan RDS deben migrar a [servicio de datos de WCF](http://go.microsoft.com/fwlink/?LinkId=199565).  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
onReadyStateChange  
```  
  
#### <a name="parameters"></a>Parámetros  
 Ninguno.  
  
## <a name="remarks"></a>Notas  
 El **ReadyState** propiedad refleja el progreso de un [RDS. DataControl](../../../ado/reference/rds-api/datacontrol-object-rds.md) objeto tal y como recupera de forma asincrónica datos en su [Recordset](../../../ado/reference/ado-api/recordset-object-ado.md) objeto. Use la **onReadyStateChange** eventos para supervisar los cambios en el **ReadyState** propiedad cada vez que se producen. Esto es más eficiente que comprobar periódicamente el valor de propiedad.  
  
## <a name="applies-to"></a>Se aplica a  
 [Objeto DataControl (RDS)](../../../ado/reference/rds-api/datacontrol-object-rds.md)  
  
## <a name="see-also"></a>Vea también  
 [Ejemplo de modelo de eventos de ADO (VC ++)](../../../ado/reference/ado-api/ado-events-model-example-vc.md)   
 [Conexión ADO y los eventos de conjunto de registros](../../../ado/guide/data/ado-event-handler-summary.md)


