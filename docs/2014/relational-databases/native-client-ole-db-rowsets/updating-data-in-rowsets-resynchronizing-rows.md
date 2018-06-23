---
title: Volver a sincronizar filas | Documentos de Microsoft
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
- docset-sql-devref
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- synchronization [OLE DB]
- IRowsetResynch interface
- resynchronizing rows
- data updates [SQL Server], OLE DB
ms.assetid: d2d30505-a878-4aa9-b821-53d8118a45a5
caps.latest.revision: 30
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.openlocfilehash: cca92fb4efe3b829ba148e5ddd2529ce9a42dd40
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/19/2018
ms.locfileid: "36103068"
---
# <a name="resynchronizing-rows"></a>Volver a sincronizar filas
  El [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] admite el proveedor OLE DB de Native Client **IRowsetResynch** en [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] compatible con cursores conjuntos de filas solo. **IRowsetResynch** no está disponible a petición. El consumidor debe solicitar la interfaz antes de abrir el conjunto de filas.  
  
## <a name="see-also"></a>Vea también  
 [Actualizar datos en conjuntos de filas](updating-data-in-rowsets.md)  
  
  