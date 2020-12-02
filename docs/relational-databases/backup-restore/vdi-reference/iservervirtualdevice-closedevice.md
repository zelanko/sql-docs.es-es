---
title: IServerVirtualDevice::CloseDevice
titlesuffix: SQL Server VDI reference
description: En este artículo se proporciona una referencia para el comando IServerVirtualDevice::CloseDevice.
ms.date: 08/30/2019
ms.prod: sql
ms.prod_service: backup-restore
ms.technology: backup-restore
ms.topic: reference
author: cawrites
ms.author: chadam
ms.openlocfilehash: 61d877fddb32f6455303a006e8955b1042ce7aa6
ms.sourcegitcommit: 5a1ed81749800c33059dac91b0e18bd8bb3081b1
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 11/23/2020
ms.locfileid: "96128906"
---
# <a name="iservervirtualdeviceclosedevice-vdi"></a>IServerVirtualDevice::CloseDevice (VDI)

[!INCLUDE [SQL Server](../../../includes/applies-to-version/sqlserver.md)]

La función **CloseDevice** cierra un dispositivo virtual que se ha abierto con IServerVirtualDeviceSet2::OpenDevice

## <a name="syntax"></a>Sintaxis

```c
HRESULT IServerVirtualDevice::CloseDevice ();
```

## <a name="return-value"></a>Valor devuelto

|Valor devuelto | Explicación |
|---|---|
| VD_E_CLOSE | El dispositivo ya está cerrado. |
| VD_E_ABORT | La interfaz está en el estado Anular. |

## <a name="remarks"></a>Observaciones

CloseDevice no es necesario después de usar SignalAbort para forzar una terminación anómala. Si se invoca CloseDevice después de usar SignalAbort, no se realiza ninguna acción.

## <a name="next-steps"></a>Pasos siguientes

Para más información, vea la [información general de la referencia de interfaces de dispositivo virtual de SQL Server](reference-virtual-device-interface.md).