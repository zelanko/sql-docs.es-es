---
title: IClientVirtualDeviceSet2::MapBufferHandle
titlesuffix: SQL Server VDI reference
description: En este artículo se proporciona una referencia para el comando IClientVirtualDeviceSet2::MapBufferHandle.
ms.date: 08/30/2019
ms.prod: sql
ms.prod_service: backup-restore
ms.technology: backup-restore
ms.topic: reference
author: mashamsft
ms.author: mathoma
ms.openlocfilehash: 5d181d1b6ddfea034716ebb048768cd7d43fbc61
ms.sourcegitcommit: b2e81cb349eecacee91cd3766410ffb3677ad7e2
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 02/01/2020
ms.locfileid: "70847586"
---
# <a name="iclientvirtualdeviceset2mapbufferhandle-vdi"></a>IClientVirtualDeviceSet2::MapBufferHandle (VDI)

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

La función **MapBufferHandle** se usa para obtener una dirección de búfer válida de un identificador de búfer obtenido de algún otro proceso.

## <a name="syntax"></a>Sintaxis

```c
HRESULT IClientVirtualDeviceSet2::MapBufferHandle (
   DWORD      dwBuffer,
   BYTE**      ppBuffer
);
```

## <a name="parameters"></a>Parámetros

*dwBuffer* Identificador devuelto por IClientVirtualDeviceSet2::GetBufferHandle.

*ppBuffer* Dirección del búfer que es válido en el proceso actual.

## <a name="return-value"></a>Valor devuelto

|Valor devuelto | Explicación |
|---|---|
| NOERROR | La función se ha realizado correctamente. |
| VD_E_PROTOCOL | El conjunto de dispositivos virtuales no está abierto actualmente. |
| VD_E_INVALID | ppBuffer es un identificador no válido. |

## <a name="remarks"></a>Observaciones

Hay que tener cuidado de comunicar correctamente los identificadores. Los identificadores son locales para un único conjunto de dispositivos virtuales. Los procesos de asociados que comparten un identificador deben asegurarse de que los identificadores de búfer solo se usan dentro del ámbito del conjunto de dispositivos virtuales del que se obtuvo originalmente el búfer.

## <a name="next-steps"></a>Pasos siguientes

Para más información, vea la [información general de la referencia de interfaces de dispositivo virtual de SQL Server](reference-virtual-device-interface.md).