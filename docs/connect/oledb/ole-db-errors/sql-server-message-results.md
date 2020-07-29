---
title: Resultados de mensajes de SQL Server | Microsoft Docs
description: resultados de los mensajes de SQL Server
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
author: pmasl
ms.author: pelopes
ms.openlocfilehash: dfebd7443b24d09e6bf7696caba5449c1890e0d2
ms.sourcegitcommit: f3321ed29d6d8725ba6378d207277a57cb5fe8c2
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 07/06/2020
ms.locfileid: "85998287"
---
# <a name="sql-server-message-results"></a>Resultados de los mensajes de SQL Server
[!INCLUDE [SQL Server](../../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]

[!INCLUDE[Driver_OLEDB_Download](../../../includes/driver_oledb_download.md)]

  Las instrucciones [!INCLUDE[tsql](../../../includes/tsql-md.md)] siguientes no generan conjuntos de filas del controlador OLE DB para SQL Server ni un recuento de filas afectadas al ejecutarse:  
  
-   PRINT  
  
-   RAISERROR con una gravedad de 10 o inferior  
  
-   DBCC  
  
-   SET SHOWPLAN  
  
-   SET STATISTICS  
  
 Estas instrucciones devuelven uno o varios mensajes informativos o hacen que [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] devuelva mensajes informativos en lugar de resultados de conjunto de filas o de recuento. Si la ejecución es correcta, OLE DB Driver for SQL Server devuelve S_OK y los mensajes están disponibles para el consumidor de OLE DB Driver for SQL Server.  
  
 OLE DB Driver for SQL Server devuelve S_OK y tiene uno o varios mensajes informativos disponibles después de la ejecución de muchas instrucciones [!INCLUDE[tsql](../../../includes/tsql-md.md)] o de la ejecución del consumidor de una función miembro de OLE DB Driver for SQL Server.  
  
 El consumidor del controlador OLE DB para SQL Server que permite la especificación dinámica de texto de consulta debe comprobar las interfaces de error después de cada ejecución de una función de miembro independientemente del valor del código de retorno, la presencia o ausencia de una referencia de interfaz **IRowset** o **IMultipleResults** devuelta o un recuento de filas afectadas.  
  
## <a name="see-also"></a>Consulte también  
 [Errores](../../oledb/ole-db-errors/errors.md)  
  
  
