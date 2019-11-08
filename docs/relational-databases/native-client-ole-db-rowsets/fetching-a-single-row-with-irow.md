---
title: Capturar una única fila con IRow | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
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
author: MightyPen
ms.author: genemi
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: c73bb76df097d259422f2c5626ecfb08668036c6
ms.sourcegitcommit: 856e42f7d5125d094fa84390bc43048808276b57
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/07/2019
ms.locfileid: "73761748"
---
# <a name="fetching-a-single-row-with-irow"></a>Capturar una única fila con IRow
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  La implementación de la interfaz **IRow** en el proveedor de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] de OLE DB Native Client se ha simplificado para aumentar el rendimiento. **IRow** permite un acceso directo a las columnas de un único objeto de fila. Si sabe de antemano que el resultado de una ejecución de comandos generará exactamente una fila, **IRow** recuperará las columnas de esa fila. Si el conjunto de resultados incluye varias filas, **IRow** solo expondrá la primera.  
  
 La implementación de **IRow** no permite cualquier navegación de la fila. Solo se obtiene acceso una vez a cada columna de la fila, con una excepción: se puede obtener acceso a una columna una primera vez para buscar el tamaño de la columna y una segunda vez para capturar los datos.  
  
> [!NOTE]  
>  **IRow::Open** solo permite la apertura de objetos de tipo DBGUID_STREAM y DBGUID_NULL.  
  
 Para obtener un objeto de fila mediante el método **ICommand::Execute**, tiene que pasarse IID_IRow. La interfaz **IMultipleResults** tiene que usarse para controlar varios conjuntos de resultados. **IMultipleResults** admite **IRow** e **IRowset**. **IRowset** se usa para las operaciones masivas.  
  
## <a name="in-this-section"></a>En esta sección  
  
-   [Utilizar IRow:: GetColumns](../../relational-databases/native-client-ole-db-rowsets/using-irow-getcolumns.md)  
  
-   [Capturar datos BLOB mediante IRow](https://msdn.microsoft.com/library/badbd6ac-20aa-4891-a14f-48d38e7f30de)  
  
## <a name="see-also"></a>Vea también  
 [Conjuntos de filas](../../relational-databases/native-client-ole-db-rowsets/rowsets.md)  
  
  
