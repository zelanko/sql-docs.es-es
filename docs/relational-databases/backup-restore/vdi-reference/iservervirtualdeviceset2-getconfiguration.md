---
title: IServerVirtualDeviceSet2::GetConfiguration
titlesuffix: SQL Server VDI reference
description: En este artículo se proporciona una referencia para el comando IServerVirtualDeviceSet2::GetConfiguration.
ms.date: 08/30/2019
ms.prod: sql
ms.prod_service: backup-restore
ms.technology: backup-restore
ms.topic: reference
author: cawrites
ms.author: chadam
ms.openlocfilehash: a70217da1fad6461ee5d20cdc6228f3984c367ff
ms.sourcegitcommit: 5a1ed81749800c33059dac91b0e18bd8bb3081b1
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 11/23/2020
ms.locfileid: "96128872"
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