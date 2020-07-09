---
title: IServerVirtualDeviceSet2::OpenDevice
titlesuffix: SQL Server VDI reference
description: En este artículo se proporciona una referencia para el comando IServerVirtualDeviceSet2::OpenDevice.
ms.date: 08/30/2019
ms.prod: sql
ms.prod_service: backup-restore
ms.technology: backup-restore
ms.topic: reference
author: mashamsft
ms.author: mathoma
ms.openlocfilehash: b43f2adedde0c317f24ee811c4ac1b2a69057de2
ms.sourcegitcommit: f7ac1976d4bfa224332edd9ef2f4377a4d55a2c9
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 07/02/2020
ms.locfileid: "85898926"
---
# <a name="iservervirtualdeviceset2opendevice-vdi"></a>IServerVirtualDeviceSet2::OpenDevice (VDI)

[!INCLUDE [SQL Server](../../../includes/applies-to-version/sqlserver.md)]

La función **OpenDevice** obtiene las interfaces de dispositivo virtual del conjunto de dispositivos virtuales.

## <a name="syntax"></a>Sintaxis

```c
HRESULT IServerVirtualDeviceSet2::OpenDevice (
   LPCWSTR                     lpName,
   IServerVirtualDevice**      ppVirtualDevice
);
```

## <a name="parameters"></a>Parámetros

*lpName* Se proporciona desde la primera cláusula VIRTUAL_DEVICE = del comando BACKUP o RESTORE. Este nombre se usa como la clave para obtener acceso al conjunto de dispositivos virtuales creado por el cliente.

*ppVirtualDevice* Se usa para devolver una interfaz de dispositivo virtual.

## <a name="return-value"></a>Valor devuelto

|Valor devuelto | Explicación |
|---|---|
| NOERROR | La función se ha realizado correctamente. |
| VD_E_OPEN |Se han abierto todos los dispositivos. |

## <a name="remarks"></a>Observaciones

Cada llamada devuelve el siguiente dispositivo sin abrir. Solo se puede llamar a la función un número de veces igual al número de dispositivos especificado en la configuración del conjunto de dispositivos virtuales.

## <a name="next-steps"></a>Pasos siguientes

Para más información, vea la [información general de la referencia de interfaces de dispositivo virtual de SQL Server](reference-virtual-device-interface.md).