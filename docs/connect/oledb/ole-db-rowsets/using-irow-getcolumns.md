---
title: 'Mediante IRow:: GetColumns | Microsoft Docs'
description: 'Mediante IRow:: GetColumns para tener acceso a todas las columnas de una fila'
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
- GetColumns method
author: pmasl
ms.author: pelopes
manager: craigg
ms.openlocfilehash: b92b76eca593259457727f9f870eb45b66cb477d
ms.sourcegitcommit: 182b8f68bfb345e9e69547b6d507840ec8ddfd8b
ms.translationtype: MTE75
ms.contentlocale: es-ES
ms.lasthandoff: 08/27/2018
ms.locfileid: "43025763"
---
# <a name="using-irowgetcolumns"></a>Usar IRow::GetColumns
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

[!INCLUDE[Driver_OLEDB_Download](../../../includes/driver_oledb_download.md)]

  La implementación de **IRow** permite el acceso secuencial a las columnas de solo avance. Puede tener acceso a todas las columnas de la fila con una sola llamada a **IRow::GetColumns** o llamar a **IRow::GetColumns** varias veces, cada vez que tenga acceso a varias columnas de la fila.  
  
 Se debe evitar que se superpongan varias llamadas a **IRow::GetColumns**. Por ejemplo, si la primera llamada a **IRow::GetColumns** recupera las columnas 1, 2 y 3, la segunda llamada a **IRow::GetColumns** debería recuperar las columnas 4, 5 y 6. Si se superponen las llamadas posteriores a **IRow::GetColumns**, la marca de estado (campo dwstatus en DBCOLUMNACCESS) se establece en DBSTATUS_E_UNAVAILABLE.  
  
## <a name="see-also"></a>Ver también  
 [Capturar una única fila con IRow](../../oledb/ole-db-rowsets/fetching-a-single-row-with-irow.md)  
  
  
