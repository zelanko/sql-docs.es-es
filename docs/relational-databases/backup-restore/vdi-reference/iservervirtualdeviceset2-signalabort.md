---
title: IServerVirtualDeviceSet2::SignalAbort
titlesuffix: SQL Server VDI reference
description: En este artículo se proporciona una referencia para el comando IServerVirtualDeviceSet2::SignalAbort.
ms.date: 08/30/2019
ms.prod: sql
ms.prod_service: backup-restore
ms.technology: backup-restore
ms.topic: reference
author: mashamsft
ms.author: mathoma
ms.openlocfilehash: b61a972d7b379ff40440124c875d8d49a7af1835
ms.sourcegitcommit: b2e81cb349eecacee91cd3766410ffb3677ad7e2
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 02/01/2020
ms.locfileid: "70847176"
---
# <a name="iservervirtualdeviceset2signalabort-vdi"></a>IServerVirtualDeviceSet2::SignalAbort (VDI)

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

La función **SignalAbort** indica que se debe producir una finalización anómala.

## <a name="syntax"></a>Sintaxis

```c
HRESULT IServerVirtualDeviceSet2::SignalAbort ();
```

## <a name="return-value"></a>Valor devuelto

Devuelve *HRESULT* que indica si la llamada al método se realizó correctamente o no. Un valor de NOERROR indica que la llamada al método se ha realizado correctamente. Un valor distinto de cero indica que se ha producido un error.

## <a name="remarks"></a>Observaciones

En cualquier momento, el servidor puede optar por anular la operación BACKUP o RESTORE.

Esta rutina indica que todas las operaciones deben cesar. La interfaz general entra en un estado de anulación. No se aceptan más comandos en ningún dispositivo. El agente de finalización devuelve ERROR_OPERATION_ABORTED para cada solicitud pendiente y vuelve al autor de la llamada. Se omiten todas las finalizaciones registradas en el cliente.

El servidor se asegura de que no haya ningún uso más necesario de los búferes o dispositivos devueltos por la interfaz del dispositivo virtual. Después, el servidor realiza una limpieza de finalización anómala, que debe incluir la llamada a la función IServerVirtualDeviceSet2::Close.

## <a name="next-steps"></a>Pasos siguientes

Para más información, vea la [información general de la referencia de interfaces de dispositivo virtual de SQL Server](reference-virtual-device-interface.md).