---
title: IClientVirtualDeviceSet2::SignalAbort
titlesuffix: SQL Server VDI reference
description: En este artículo se proporciona una referencia para el comando IClientVirtualDeviceSet2::SignalAbort.
ms.date: 08/30/2019
ms.prod: sql
ms.prod_service: backup-restore
ms.technology: backup-restore
ms.topic: reference
author: mashamsft
ms.author: mathoma
ms.openlocfilehash: ec46b61b89f19c568dc924f5651e9bb544a63ca9
ms.sourcegitcommit: f7ac1976d4bfa224332edd9ef2f4377a4d55a2c9
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 07/02/2020
ms.locfileid: "85896840"
---
# <a name="iclientvirtualdeviceset2signalabort-vdi"></a>IClientVirtualDeviceSet2::SignalAbort (VDI)

[!INCLUDE [SQL Server](../../../includes/applies-to-version/sqlserver.md)]

La función **SignalAbort** se usa para indicar que se debe producir una finalización anómala.

## <a name="syntax"></a>Sintaxis

```c
HRESULT IClientVirtualDeviceSet2::SignalAbort ();
```

## <a name="return-value"></a>Valor devuelto

Devuelve *HRESULT* que indica si la llamada al método se realizó correctamente o no. Un valor de NOERROR indica que la llamada al método se ha realizado correctamente. Un valor distinto de cero indica que se ha producido un error.

## <a name="remarks"></a>Observaciones

En cualquier momento, el cliente puede optar por anular la operación BACKUP o RESTORE. Esta rutina indica que todas las operaciones deben cesar. El estado del conjunto de dispositivos virtuales completo entra en el estado Anular. No se devuelven más comandos en ningún dispositivo. Todos los comandos incompletos se completan automáticamente y devuelven ERROR_OPERATION_ABORTED como código de finalización. El cliente debe llamar a IClientVirtualDeviceSet2::Close una vez que haya finalizado de forma segura cualquier uso pendiente de los búferes proporcionados al cliente. Para más información, vea Terminación anómala.

## <a name="next-steps"></a>Pasos siguientes

Para más información, vea la [información general de la referencia de interfaces de dispositivo virtual de SQL Server](reference-virtual-device-interface.md).