---
title: IServerVirtualDeviceSet2::GetConfiguration
titlesuffix: SQL Server VDI reference
description: En este artículo se proporciona una referencia para el comando IServerVirtualDeviceSet2::GetConfiguration.
ms.date: 08/30/2019
ms.prod: sql
ms.prod_service: backup-restore
ms.technology: backup-restore
ms.topic: reference
author: mashamsft
ms.author: mathoma
ms.openlocfilehash: e27277c5626cbc6922d6f7370327da34e257b5b0
ms.sourcegitcommit: f7ac1976d4bfa224332edd9ef2f4377a4d55a2c9
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 07/02/2020
ms.locfileid: "85881854"
---
# <a name="iservervirtualdeviceset2getconfiguration-vdi"></a>IServerVirtualDeviceSet2::GetConfiguration (VDI)

[!INCLUDE [SQL Server](../../../includes/applies-to-version/sqlserver.md)]

La función **GetConfiguration** obtiene la configuración solicitada por el cliente.

## <a name="syntax"></a>Sintaxis

```c
HRESULT IServerVirtualDeviceSet2::GetConfiguration (
   VDConfig*   pCfg
);
```

## <a name="parameters"></a>Parámetros

*pCfg* Es la configuración especificada por el cliente mediante IClientVirtualDeviceSet2::Create.

## <a name="return-value"></a>Valor devuelto

Devuelve *HRESULT* que indica si la llamada al método se realizó correctamente o no. Un valor de NOERROR indica que la llamada al método se ha realizado correctamente. Un valor distinto de cero indica que se ha producido un error.

## <a name="remarks"></a>Observaciones

Se espera que el servidor inspeccione y responda a la configuración proporcionada por el cliente. Para más información, vea Configuración. El servidor puede usar SignalAbort si determina que no puede funcionar correctamente con la configuración proporcionada.

## <a name="next-steps"></a>Pasos siguientes

Para más información, vea la [información general de la referencia de interfaces de dispositivo virtual de SQL Server](reference-virtual-device-interface.md).