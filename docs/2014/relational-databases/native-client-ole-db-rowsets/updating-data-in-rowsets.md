---
title: Actualización de datos de conjuntos de filas | Microsoft Docs
ms.custom: ''
ms.date: 04/27/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- updating data [SQL Server]
- rowsets [OLE DB], updating data
- SQL Server Native Client OLE DB provider, rowsets
- OLE DB rowsets, updating data
- SQL Server Native Client OLE DB provider, data updates
- data updates [SQL Server], OLE DB
ms.assetid: 37769b1c-c480-419a-8c54-5cc420bf73db
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: 2d1c1e70e704c50b619a34b28a899ce10316d446
ms.sourcegitcommit: b72c9fc9436c44c6a21fd96223c73bf94706c06b
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/01/2020
ms.locfileid: "82704709"
---
# <a name="updating-data-in-rowsets"></a>Actualizar datos en conjuntos de filas
  El [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] proveedor de OLE DB de Native Client actualiza los [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] datos cuando un consumidor actualiza un conjunto de filas modificable que contiene los datos. Se crea un conjunto de filas modificable cuando el consumidor solicita compatibilidad para las interfaces **IRowsetUpdate** o **IRowsetChange**.  
  
 Todos los [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] conjuntos de filas modificables del proveedor de OLE DB de Native Client utilizan [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] cursores para admitir el conjunto de filas. La propiedad de conjunto de filas DBPROP_LOCKMODE modifica el comportamiento de control de simultaneidad de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] en cursores y determina el comportamiento de la captura de filas del conjunto de filas y la generación de errores de integridad de datos en los conjuntos de filas actualizables.  
  
 El [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] proveedor de OLE DB de Native Client admite la sincronización de filas antes o después de una actualización.  
  
> [!NOTE]  
>  IRowChange::SetColumns está disponible para establecer los valores de una o más columnas con nombre de un objeto de fila.  
  
## <a name="in-this-section"></a>En esta sección  
  
-   [Actualizar datos en cursores de SQL Server](updating-data-in-sql-server-cursors.md)  
  
-   [Volver a sincronizar filas](updating-data-in-rowsets-resynchronizing-rows.md)  
  
## <a name="see-also"></a>Consulte también  
 [Conjuntos de filas](rowsets.md)  
  
  
