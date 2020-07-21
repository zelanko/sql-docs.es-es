---
title: IClientVirtualDevice::CompleteCommand
titlesuffix: SQL Server VDI reference
description: En este artículo se proporciona una referencia para el comando IClientVirtualDevice::CompleteCommand.
ms.date: 08/30/2019
ms.prod: sql
ms.prod_service: backup-restore
ms.technology: backup-restore
ms.topic: reference
author: mashamsft
ms.author: mathoma
ms.openlocfilehash: dda70978e4daba50018b58c3cf9aeaaaa4374551
ms.sourcegitcommit: f7ac1976d4bfa224332edd9ef2f4377a4d55a2c9
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 07/02/2020
ms.locfileid: "85896946"
---
# <a name="iclientvirtualdevicecompletecommand-vdi"></a>IClientVirtualDevice::CompleteCommand (VDI)

[!INCLUDE [SQL Server](../../../includes/applies-to-version/sqlserver.md)]

La función **CompleteCommand** se usa para notificar a SQL Server que un comando ha finalizado. Se debe devolver la información de finalización adecuada para el comando.

## <a name="syntax"></a>Sintaxis

```c
HRESULT IClientVirtualDevice::CompleteCommand (
   VDC_Command*         const pCmd,
   UINT32               dwCompletionCode,
   UINT32               dwBytesTransferred,
   UINT64               dwlPosition
);
```

## <a name="parameters"></a>Parámetros

*pCmd* Es la dirección de un comando devuelto anteriormente desde IClientVirtualDevice::GetCommand.

*dwCompletionCode* Es un código de estado de WIN32 que indica el estado de finalización. Este parámetro debe devolverse para todos los comandos. El código devuelto debe ser adecuado para el comando que se va a realizar. ERROR_SUCCESS se usa en todos los casos para indicar un comando ejecutado correctamente. Para obtener una lista completa de los códigos posibles, vea el archivo Winerror.h. Una lista de códigos de estado típicos para cada comando aparece en Comandos.

*dwBytesTransferred* El número de bytes transferidos de forma correcta. Solo se devuelve para los comandos de transferencia de datos de lectura y escritura.

*dwlPosition* Una respuesta solo al comando GetPosition.

## <a name="return-value"></a>Valor devuelto

|Valor devuelto | Explicación |
|---|---|
| NOERROR | La finalización se anotó correctamente. |
| VD_E_INVALID | pCmd no era un comando activo. |
| VD_E_ABORT | Se señaló Abort. |
| VD_E_PROTOCOL | El dispositivo no está abierto. |

## <a name="next-steps"></a>Pasos siguientes

Para más información, vea la [información general de la referencia de interfaces de dispositivo virtual de SQL Server](reference-virtual-device-interface.md).
