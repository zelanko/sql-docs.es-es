---
title: Captura de una sola fila mediante IRow (controlador OLE DB) | Microsoft Docs
description: IRow permite un acceso directo a las columnas de un único objeto de fila. La interfaz IRow en OLE DB Driver for SQL Server se ha simplificado para aumentar el rendimiento.
ms.custom: ''
ms.date: 06/14/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: connectivity
ms.topic: reference
helpviewer_keywords:
- fetching rows
- IRow interface
- single row fetching [OLE DB Driver for SQL Server]
- OLE DB rowsets, fetching
- rowsets [OLE DB], fetching
- OLE DB Driver for SQL Server, fetching
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: a305692bb544d9a9bbb0572cbd93449781aaabe9
ms.sourcegitcommit: c95f3ef5734dec753de09e07752a5d15884125e2
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 08/25/2020
ms.locfileid: "88862475"
---
# <a name="fetching-a-single-row-with-irow-ole-db-driver"></a>Captura de una sola fila mediante IRow (controlador OLE DB)
[!INCLUDE [SQL Server](../../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]

[!INCLUDE[Driver_OLEDB_Download](../../../includes/driver_oledb_download.md)]

  La implementación de la interfaz **IRow** en OLE DB Driver for SQL Server se ha simplificado para aumentar el rendimiento. **IRow** permite un acceso directo a las columnas de un único objeto de fila. Si sabe de antemano que el resultado de una ejecución de comandos generará exactamente una fila, **IRow** recuperará las columnas de esa fila. Si el conjunto de resultados incluye varias filas, **IRow** solo expondrá la primera.  
  
 La implementación de **IRow** no permite cualquier navegación de la fila. Solo se obtiene acceso una vez a cada columna de la fila, con una excepción: se puede obtener acceso a una columna una primera vez para buscar el tamaño de la columna y una segunda vez para capturar los datos.  
  
> [!NOTE]  
>  **IRow::Open** solo permite la apertura de objetos de tipo DBGUID_STREAM y DBGUID_NULL.  
  
 Para obtener un objeto de fila mediante el método **ICommand::Execute**, tiene que pasarse IID_IRow. La interfaz **IMultipleResults** tiene que usarse para controlar varios conjuntos de resultados. **IMultipleResults** admite **IRow** e **IRowset**. **IRowset** se usa para las operaciones masivas.  
  
## <a name="in-this-section"></a>En esta sección  
  
-   [Utilizar IRow:: GetColumns](../../oledb/ole-db-rowsets/using-irow-getcolumns.md)   
  
## <a name="see-also"></a>Consulte también  
 [Conjuntos de filas](../../oledb/ole-db-rowsets/rowsets.md)  
  
  
