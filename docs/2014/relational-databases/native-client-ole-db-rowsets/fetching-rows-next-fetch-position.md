---
title: Siguiente posición de captura | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- fetching rows
- OLE DB rowsets, fetching
- next fetch position
- rowsets [OLE DB], fetching
ms.assetid: 9ef74b3f-c9c0-492f-9b93-d65738a61abd
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: 05d2c63c2d973416883562512ac45dd391f6c4b6
ms.sourcegitcommit: b72c9fc9436c44c6a21fd96223c73bf94706c06b
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/01/2020
ms.locfileid: "82694517"
---
# <a name="next-fetch-position"></a>Posición de captura siguiente
  El [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] proveedor de OLE DB de Native Client realiza un seguimiento de la siguiente posición de captura para que una secuencia de llamadas al método **GetNextRows** (sin omitidos, cambios de dirección o llamadas intermedias a los métodos **FindNextRow**, **Seek**o **RestartPosition** ) Lea todo el conjunto de filas sin omitir o repetir ninguna fila. La siguiente posición de captura cambia mediante una llamada a **IRowset::GetNextRows**, **IRowset::RestartPosition** o **IRowsetIndex::Seek**, o bien mediante una llamada a **FindNextRow** con un valor *pBookmark* NULL. La llamada a **FindNextRow** con un valor *pBookmark* que no sea NULL no afecta a la siguiente posición de captura.  
  
## <a name="see-also"></a>Consulte también  
 [Capturar filas](fetching-rows.md)  
  
  
