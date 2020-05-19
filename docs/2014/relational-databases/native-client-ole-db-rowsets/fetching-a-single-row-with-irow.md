---
title: Captura de una sola fila con IRow | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- fetching rows
- IRow interface
- single row fetching [SQL Server Native Client]
- OLE DB rowsets, fetching
- rowsets [OLE DB], fetching
- SQL Server Native Client OLE DB provider, fetching
ms.assetid: 07c803ca-299a-42c5-ba02-360b9631d15f
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: d47e668a2c31e9fb00a8f3582a3538fa9127ef65
ms.sourcegitcommit: b72c9fc9436c44c6a21fd96223c73bf94706c06b
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/01/2020
ms.locfileid: "82694662"
---
# <a name="fetching-a-single-row-with-irow"></a>Capturar una única fila con IRow
  La implementación de la interfaz **IRow** en el [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] proveedor de OLE DB de Native Client se ha simplificado para aumentar el rendimiento. **IRow** permite un acceso directo a las columnas de un único objeto de fila. Si sabe de antemano que el resultado de una ejecución de comandos generará exactamente una fila, **IRow** recuperará las columnas de esa fila. Si el conjunto de resultados incluye varias filas, **IRow** solo expondrá la primera.  
  
 La implementación de **IRow** no permite cualquier navegación de la fila. Solo se obtiene acceso una vez a cada columna de la fila, con una excepción: se puede obtener acceso a una columna una primera vez para buscar el tamaño de la columna y una segunda vez para capturar los datos.  
  
> [!NOTE]  
>  **IRow::Open** solo permite la apertura de objetos de tipo DBGUID_STREAM y DBGUID_NULL.  
  
 Para obtener un objeto de fila mediante el método **ICommand::Execute**, tiene que pasarse IID_IRow. La interfaz **IMultipleResults** tiene que usarse para controlar varios conjuntos de resultados. **IMultipleResults** admite **IRow** e **IRowset**. **IRowset** se usa para las operaciones masivas.  
  
## <a name="in-this-section"></a>En esta sección  
  
-   [Usar IRow::GetColumns](using-irow-getcolumns.md)  
  
-   [Capturar datos BLOB mediante IRow](../../database-engine/dev-guide/fetching-blob-data-using-irow.md)  
  
## <a name="see-also"></a>Consulte también  
 [Conjuntos de filas](rowsets.md)  
  
  
