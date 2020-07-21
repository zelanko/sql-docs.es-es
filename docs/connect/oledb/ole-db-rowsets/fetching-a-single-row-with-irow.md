---
title: Captura de una sola fila con IRow | Microsoft Docs
description: Captura de una sola fila mediante la interfaz IRow de OLE DB Driver for SQL Server
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
author: pmasl
ms.author: pelopes
ms.openlocfilehash: 542875dc322cd94970c238747db0adb139b9a480
ms.sourcegitcommit: ff82f3260ff79ed860a7a58f54ff7f0594851e6b
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 03/29/2020
ms.locfileid: "67994293"
---
# <a name="fetching-a-single-row-with-irow"></a>Capturar una única fila con IRow
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

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
  
  
