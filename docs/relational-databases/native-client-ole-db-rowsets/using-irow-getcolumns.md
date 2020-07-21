---
title: Uso de IRow::GetColumns | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
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
- GetColumns method
ms.assetid: 1f5d2e03-e6fe-4ea1-b71d-55d02b5d59ae
author: markingmyname
ms.author: maghan
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 092c573e808aefc0f35f04e73b54e150a62bebac
ms.sourcegitcommit: f3321ed29d6d8725ba6378d207277a57cb5fe8c2
ms.contentlocale: es-ES
ms.lasthandoff: 07/06/2020
ms.locfileid: "86013074"
---
# <a name="using-irowgetcolumns"></a>Usar IRow::GetColumns
[!INCLUDE[SQL Server Azure SQL Database Synapse Analytics PDW ](../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]

  La implementación de **IRow** permite el acceso secuencial a las columnas de solo avance. Puede tener acceso a todas las columnas de la fila con una sola llamada a **IRow::GetColumns** o llamar a **IRow::GetColumns** varias veces, cada vez que tenga acceso a varias columnas de la fila.  
  
 Se debe evitar que se superpongan varias llamadas a **IRow::GetColumns**. Por ejemplo, si la primera llamada a **IRow::GetColumns** recupera las columnas 1, 2 y 3, la segunda llamada a **IRow::GetColumns** debería recuperar las columnas 4, 5 y 6. Si se superponen las llamadas posteriores a **IRow::GetColumns**, la marca de estado (campo dwstatus en DBCOLUMNACCESS) se establece en DBSTATUS_E_UNAVAILABLE.  
  
## <a name="see-also"></a>Consulte también  
 [Capturar una única fila con IRow](../../relational-databases/native-client-ole-db-rowsets/fetching-a-single-row-with-irow.md)  
  
  
