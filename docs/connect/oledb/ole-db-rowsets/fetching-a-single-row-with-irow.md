---
title: Capturar una única fila con IRow | Microsoft Docs
description: Capturar una fila única mediante la interfaz IRow del controlador de OLE DB para SQL Server
ms.custom: ''
ms.date: 06/14/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.component: oledb|ole-db-rowsets
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
ms.author: pelopes
manager: craigg
ms.openlocfilehash: b83b13e1cd0c4818a21351fb5433dae89f54cd0a
ms.sourcegitcommit: 182b8f68bfb345e9e69547b6d507840ec8ddfd8b
ms.translationtype: MTE75
ms.contentlocale: es-ES
ms.lasthandoff: 08/27/2018
ms.locfileid: "43032360"
---
# <a name="fetching-a-single-row-with-irow"></a>Capturar una única fila con IRow
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

[!INCLUDE[Driver_OLEDB_Download](../../../includes/driver_oledb_download.md)]

  El **IRow** interfaz implementación en el controlador OLE DB para SQL Server se ha simplificado para aumentar el rendimiento. **IRow** permite un acceso directo a las columnas de un único objeto de fila. Si sabe de antemano que el resultado de una ejecución de comandos generará exactamente una fila, **IRow** recuperará las columnas de esa fila. Si el conjunto de resultados incluye varias filas, **IRow** solo expondrá la primera.  
  
 La implementación de **IRow** no permite cualquier navegación de la fila. Solo se obtiene acceso una vez a cada columna de la fila, con una excepción: se puede obtener acceso a una columna una primera vez para buscar el tamaño de la columna y una segunda vez para capturar los datos.  
  
> [!NOTE]  
>  **IRow::Open** solo permite la apertura de objetos de tipo DBGUID_STREAM y DBGUID_NULL.  
  
 Para obtener un objeto de fila mediante el método **ICommand::Execute**, tiene que pasarse IID_IRow. La interfaz **IMultipleResults** tiene que usarse para controlar varios conjuntos de resultados. **IMultipleResults** admite **IRow** e **IRowset**. **IRowset** se usa para las operaciones masivas.  
  
## <a name="in-this-section"></a>En esta sección  
  
-   [Utilizar IRow:: GetColumns](../../oledb/ole-db-rowsets/using-irow-getcolumns.md)   
  
## <a name="see-also"></a>Ver también  
 [Conjuntos de filas](../../oledb/ole-db-rowsets/rowsets.md)  
  
  
