---
title: Resultados del mensaje de SQL Server (OLE DB Driver)
description: Obtenga información sobre las instrucciones Transact-SQL que no generan conjuntos de filas de OLE DB Driver for SQL Server o un recuento, ni sus valores devueltos previstos.
ms.custom: ''
ms.date: 06/14/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: connectivity
ms.topic: reference
helpviewer_keywords:
- OLE DB Driver for SQL Server, errors
- errors [OLE DB], SQL Server message results
- OLE DB error handling, SQL Server message results
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: dc3701313f920eead650435ca40538ad8a4b6ef0
ms.sourcegitcommit: c95f3ef5734dec753de09e07752a5d15884125e2
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 08/25/2020
ms.locfileid: "88862506"
---
# <a name="sql-server-message-results"></a>Resultados de los mensajes de SQL Server
[!INCLUDE [SQL Server](../../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]

[!INCLUDE[Driver_OLEDB_Download](../../../includes/driver_oledb_download.md)]

Las instrucciones [!INCLUDE[tsql](../../../includes/tsql-md.md)] siguientes no generan conjuntos de filas de OLE DB Driver for SQL Server ni un recuento de las filas afectadas al ejecutarse:  
  
-   PRINT  
  
-   RAISERROR con una gravedad de 10 o inferior  
  
-   DBCC  
  
-   SET SHOWPLAN  
  
-   SET STATISTICS  
  
 Estas instrucciones devuelven uno o varios mensajes informativos o hacen que [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] devuelva mensajes informativos en lugar de resultados de conjunto de filas o de recuento. Si la ejecución es correcta, OLE DB Driver for SQL Server devuelve S_OK y los mensajes están disponibles para el consumidor de OLE DB Driver for SQL Server.  
  
 OLE DB Driver for SQL Server devuelve S_OK y tiene uno o varios mensajes informativos disponibles después de la ejecución de muchas instrucciones [!INCLUDE[tsql](../../../includes/tsql-md.md)] o de la ejecución del consumidor de una función miembro de OLE DB Driver for SQL Server.  
  
Al consumidor de OLE DB Driver for SQL Server se le permite la especificación dinámica del texto de la consulta. El consumidor debe comprobar las interfaces de errores después de _todas_ las ejecuciones de las funciones de miembro. Siempre debe realizar estas comprobaciones, sea cual sea el valor del código devuelto o independientemente de si se devuelve o no una referencia de interfaces a un objeto `IRowset` o `IMultipleResults`, sea cual sea el recuento de las filas afectadas.
  
## <a name="see-also"></a>Consulte también  
 [Errores](../../oledb/ole-db-errors/errors.md)  
  
  
