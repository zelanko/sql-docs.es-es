---
title: Posición de captura siguiente | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology: native-client
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- fetching rows
- OLE DB rowsets, fetching
- next fetch position
- rowsets [OLE DB], fetching
ms.assetid: 9ef74b3f-c9c0-492f-9b93-d65738a61abd
caps.latest.revision: 29
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 1d6fa0247cafa0d0750f224e3b369965fd4e7989
ms.sourcegitcommit: f8ce92a2f935616339965d140e00298b1f8355d7
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/03/2018
ms.locfileid: "37423574"
---
# <a name="next-fetch-position"></a>Posición de captura siguiente
  El [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB proveedor realiza un seguimiento de la siguiente posición de captura hasta que una secuencia de llamadas a la **GetNextRows** método (sin saltos, cambios de dirección o intermedia, las llamadas a la  **FindNextRow**, **Seek**, o **RestartPosition** métodos) lee el conjunto de filas completo sin omitir ni repetir ninguna fila. La siguiente posición de captura cambia mediante una llamada a **IRowset:: GetNextRows**, **IRowset:: RestartPosition**, o **IRowsetIndex:: Seek**, o mediante una llamada a **FindNextRow** con un valor null *pBookmark* valor. Una llamada a **FindNextRow** con un nonnull *pBookmark* valor no afecta a la siguiente posición de captura.  
  
## <a name="see-also"></a>Vea también  
 [Capturar filas](fetching-rows.md)  
  
  
