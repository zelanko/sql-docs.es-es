---
title: IServerVirtualDeviceSet2::FreeBuffer
titlesuffix: SQL Server VDI reference
description: En este artículo se proporciona una referencia para el comando IServerVirtualDeviceSet2::FreeBuffer.
ms.date: 08/30/2019
ms.prod: sql
ms.prod_service: backup-restore
ms.technology: backup-restore
ms.topic: reference
author: mashamsft
ms.author: mathoma
ms.openlocfilehash: 2829f849ce8cd220fdabc75a0d2059c5da0c80fd
ms.sourcegitcommit: 58158eda0aa0d7f87f9d958ae349a14c0ba8a209
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 03/30/2020
ms.locfileid: "70847266"
---
# <a name="iservervirtualdeviceset2freebuffer-vdi"></a>IServerVirtualDeviceSet2::FreeBuffer (VDI)

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

La función **FreeBuffer** obtiene un búfer de memoria compartida del conjunto de dispositivos virtuales.

## <a name="syntax"></a>Sintaxis

```c
HRESULT IServerVirtualDeviceSet2::FreeBuffer (
   LPVOID   pBuffer,
   UINT32   dwSize
);
```

## <a name="parameters"></a>Parámetros

*pBuffer* Devuelve un búfer devuelto por IServerVirtualDeviceSet2::AllocateBuffer.

*dwSize* Es el tamaño del búfer en bytes. Esto no incluye ninguna zona de prefijo solicitada por el cliente. Ese tipo de zona se oculta al servidor y habrá espacio disponible antes de que se devuelva la dirección del búfer.

## <a name="return-value"></a>Valor devuelto

|Valor devuelto | Explicación |
|---|---|
| NOERROR | Se devuelve el búfer. |
| VD_E_INVALID | Un parámetro no era válido. |

## <a name="next-steps"></a>Pasos siguientes

Para más información, vea la [información general de la referencia de interfaces de dispositivo virtual de SQL Server](reference-virtual-device-interface.md).