---
description: onReadyStateChange (evento, RDS)
title: onReadyStateChange (evento) (RDS) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
helpviewer_keywords:
- onReadyStateChange event [ADO]
ms.assetid: bf2ae3ac-bfe4-4709-b50a-ea7c282c3164
author: rothja
ms.author: jroth
ms.openlocfilehash: ee9f48a3cba1190cdd9400b5ee5ecb30c35bfaed
ms.sourcegitcommit: c7f40918dc3ecdb0ed2ef5c237a3996cb4cd268d
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/05/2020
ms.locfileid: "91724456"
---
# <a name="onreadystatechange-event-rds"></a>onReadyStateChange (evento, RDS)
Se llama al evento **onreadystatechange** siempre que cambia el valor de la propiedad [ReadyState](./readystate-property-rds.md) .  
  
> [!IMPORTANT]
>  A partir de Windows 8 y Windows Server 2012, los componentes de servidor RDS ya no se incluyen en el sistema operativo Windows (consulte la guía de compatibilidad de Windows 8 y [Windows server 2012](https://www.microsoft.com/download/details.aspx?id=27416) para obtener más detalles). Los componentes de cliente RDS se quitarán en una versión futura de Windows. Evite utilizar esta característica en nuevos trabajos de desarrollo y tenga previsto modificar las aplicaciones que actualmente la utilizan. Las aplicaciones que utilizan RDS deben migrar al [servicio de datos de WCF](/dotnet/framework/wcf/).  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
onReadyStateChange  
```  
  
#### <a name="parameters"></a>Parámetros  
 Ninguno.  
  
## <a name="remarks"></a>Observaciones  
 La propiedad **ReadyState** refleja el progreso de un [objeto RDS. Objeto DataControl](./datacontrol-object-rds.md) , ya que recupera de forma asincrónica los datos en su objeto de [conjunto de registros](../ado-api/recordset-object-ado.md) . Use el evento **onreadystatechange** para supervisar los cambios en la propiedad **ReadyState** siempre que se produzcan. Esto es más eficaz que comprobar periódicamente el valor de la propiedad.  
  
## <a name="applies-to"></a>Se aplica a  
 [Objeto DataControl (RDS)](./datacontrol-object-rds.md)  
  
## <a name="see-also"></a>Consulte también  
 [Ejemplo de modelo de eventos de ADO (VC + +)](../ado-api/ado-events-model-example-vc.md)   
 [Conexión ADO y los eventos de conjunto de registros](../../guide/data/ado-event-handler-summary.md)