---
title: IServerVirtualDevice::SendCommand
titlesuffix: SQL Server VDI reference
description: En este artículo se proporciona una referencia para el comando IServerVirtualDevice::SendCommand.
ms.date: 08/30/2019
ms.prod: sql
ms.prod_service: backup-restore
ms.technology: backup-restore
ms.topic: reference
author: cawrites
ms.author: chadam
ms.openlocfilehash: f03e87863d21abfc4abf91811616cbacd14caff2
ms.sourcegitcommit: 5a1ed81749800c33059dac91b0e18bd8bb3081b1
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 11/23/2020
ms.locfileid: "96125375"
---
# <a name="iservervirtualdevicesendcommand-vdi"></a>IServerVirtualDevice::SendCommand (VDI)

[!INCLUDE [SQL Server](../../../includes/applies-to-version/sqlserver.md)]

La función **SendCommand** envía un comando al cliente mediante un objeto de dispositivo virtual devuelto desde IServerVirtualDeviceSet2::OpenDevice.

## <a name="syntax"></a>Sintaxis

```c
HRESULT IServerVirtualDevice::SendCommand (
   VDS_Command*   pCmd
);
```

## <a name="parameters"></a>Parámetros

*pCmd* Un puntero a un bloque de solicitud de comando. Para más información, vea Comandos. El campo completionFunction se debe establecer para que apunte a la dirección de una función con la firma siguiente:

```c
void callbackFunction ( VDS_Command *pCmd);
```

El agente de finalización realiza esta devolución de llamada cuando el cliente indica que se ha completado un comando. SQL Server establece el campo completionContext de pCmd. Su finalidad es proporcionar contexto a la función de devolución de llamada.

## <a name="return-value"></a>Valor devuelto

|Valor devuelto | Explicación |
|---|---|
| NOERROR | El comando se ha puesto correctamente en cola en el cliente. |
| VD_E_QUEUE_FULL | La cola del dispositivo está llena. |
| VD_E_IO_ERROR | El dispositivo se encuentra en un estado de IO-ERROR. |
| VD_E_PROTOCOL | El dispositivo no está activo. |

## <a name="remarks"></a>Observaciones

Cuando se produce un error al intentar enviar el comando, se invoca la función de devolución de llamada y el valor completionCode del búfer de comandos se establece de esta forma:

| completionCode | Error |
|---|---|
| VD_E_QUEUE_FULL | ERROR_NO_SYSTEM_RESOURCES |
| VD_E_IO_ERROR   | ERROR_IO_DEVICE |
| VD_E_PROTOCOL   | ERROR_INVALID_HANDLE |
| VD_E_ABORT      | ERROR_OPERATION_ABORTED |

## <a name="next-steps"></a>Pasos siguientes

Para más información, vea la [información general de la referencia de interfaces de dispositivo virtual de SQL Server](reference-virtual-device-interface.md).