---
description: LOCALDB_ERROR_INSUFFICIENT_BUFFER
title: LOCALDB_ERROR_INSUFFICIENT_BUFFER | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: performance
ms.topic: reference
ms.assetid: ff67bda8-7e5c-4b06-8d7b-9985b6059a98
author: WilliamDAssafMSFT
ms.author: wiassaf
ms.openlocfilehash: 5c0315eb0d4318fd7e6c82ad19676af37e0391d8
ms.sourcegitcommit: 0e0cd9347c029e0c7c9f3fe6d39985a6d3af967d
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 12/02/2020
ms.locfileid: "96506204"
---
# <a name="localdb_error_insufficient_buffer"></a>LOCALDB_ERROR_INSUFFICIENT_BUFFER
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]
    
## <a name="details"></a>Detalles  
  
| Atributo | Value |
| --------- | ----- |
|Nombre de producto|SQL Server|  
|Id. de evento|276|  
|Origen de eventos|SQL Server Local Database Runtime 12.0|  
|Componente|API de Local Database Runtime|  
|Texto del mensaje|El búfer pasado el método de API de la instancia de Local Database no tiene un tamaño suficiente.|  
  
## <a name="explanation"></a>Explicación  
 El búfer de entrada es demasiado corto y no se ha solicitado truncamiento.  
  
## <a name="user-action"></a>Acción del usuario  
 Proporcione un búfer del tamaño especificado.  
  
  
