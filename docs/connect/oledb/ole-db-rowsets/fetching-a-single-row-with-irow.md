---
title: Capturar una única fila con IRow | Documentos de Microsoft
description: Capturar una sola fila mediante IRow, interfaz de controlador de OLE DB para SQL Server
ms.custom: ''
ms.date: 03/26/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.component: ole-db-rowsets
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- fetching rows
- IRow interface
- single row fetching [OLE DB Driver for SQL Server]
- OLE DB rowsets, fetching
- rowsets [OLE DB], fetching
- OLE DB Driver for SQL Server, fetching
author: pmasl
ms.author: Pedro.Lopes
manager: craigg
ms.openlocfilehash: 5046360a21e3036851ee42423f1bb2ceb7083602
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/03/2018
---
# <a name="fetching-a-single-row-with-irow"></a>Capturar una única fila con IRow
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  El **IRow** interfaz implementación en el controlador OLE DB para SQL Server se ha simplificado para aumentar el rendimiento. **IRow** permite el acceso directo a las columnas de un objeto de fila única. Si sabe de antemano que el resultado de una ejecución de comandos generará exactamente una fila, **IRow** recuperará las columnas de esa fila. Si el conjunto de resultados incluye varias filas, **IRow** expondrá solo la primera fila.  
  
 El **IRow** implementación no permite cualquier navegación de la fila. Solo se obtiene acceso una vez a cada columna de la fila, con una excepción: se puede obtener acceso a una columna una primera vez para buscar el tamaño de la columna y una segunda vez para capturar los datos.  
  
> [!NOTE]  
>  **IRow:: Open** admite solo el tipo y DBGUID_NULL de objetos que se va a abrir.  
  
 Para obtener un objeto de fila mediante **ICommand:: Execute** método, debe pasarse IID_IRow. El **IMultipleResults** interfaz debe usarse para controlar varios conjuntos de resultados. **IMultipleResults** admite **IRow** y **IRowset**. **IRowset** usadas para operaciones masivas.  
  
## <a name="in-this-section"></a>En esta sección  
  
-   [Utilizar IRow:: GetColumns](../../oledb/ole-db-rowsets/using-irow-getcolumns.md)   
  
## <a name="see-also"></a>Vea también  
 [Conjuntos de filas](../../oledb/ole-db-rowsets/rowsets.md)  
  
  
