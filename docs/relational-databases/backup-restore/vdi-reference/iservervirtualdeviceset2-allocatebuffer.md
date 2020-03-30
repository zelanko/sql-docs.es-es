---
title: IServerVirtualDeviceSet2::AllocateBuffer
titlesuffix: SQL Server VDI reference
description: En este artículo se proporciona una referencia para el comando IServerVirtualDeviceSet2::AllocateBuffer.
ms.date: 08/30/2019
ms.prod: sql
ms.prod_service: backup-restore
ms.technology: backup-restore
ms.topic: reference
author: mashamsft
ms.author: mathoma
ms.openlocfilehash: 8c28009fae8b52264b541ca3eb4281ab9abccf63
ms.sourcegitcommit: 58158eda0aa0d7f87f9d958ae349a14c0ba8a209
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 03/30/2020
ms.locfileid: "70847496"
---
# <a name="iservervirtualdeviceset2allocatebuffer-vdi"></a>IServerVirtualDeviceSet2::AllocateBuffer (VDI)

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

La función **AllocateBuffer** obtiene un búfer de memoria compartida del conjunto de dispositivos virtuales.

## <a name="syntax"></a>Sintaxis

```c
HRESULT IServerVirtualDeviceSet2::AllocateBuffer (
   LPVOID*      ppBuffer,
   UINT32      dwSize,
   UINT32      dwAlignment
);
```

## <a name="parameters"></a>Parámetros

*ppBuffer* Devuelve un puntero al principio del búfer.

*dwSize* Es el tamaño del búfer en bytes. Esto no incluye ninguna zona de prefijo solicitada por el cliente. Ese tipo de zona se oculta al servidor y habrá espacio disponible antes de que se devuelva la dirección del búfer.

*dwAlignment* Especifica el límite de alineación del búfer. Por ejemplo, un valor de 4096 garantiza que el búfer está alineado en un límite de 4096 bytes. Esto significa que la dirección devuelta tendría los 12 bits de orden inferior establecidos en cero. Este parámetro debe ser una potencia de 2.

## <a name="return-value"></a>Valor devuelto

|Valor devuelto | Explicación |
|---|---|
| NOERROR | Se devuelve el búfer. |
| VD_E_MEMORY | Se ha producido una condición de memoria insuficiente. |
| VD_E_INVALID | Un parámetro no era válido. |

## <a name="next-steps"></a>Pasos siguientes

Para más información, vea la [información general de la referencia de interfaces de dispositivo virtual de SQL Server](reference-virtual-device-interface.md).