---
title: Resultados del mensaje de SQL Server | Documentos de Microsoft
description: resultados de los mensajes de SQL Server
ms.custom: ''
ms.date: 03/26/2018
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: ''
ms.component: ole-db-errors
ms.reviewer: ''
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- OLE DB Driver for SQL Server, errors
- errors [OLE DB], SQL Server message results
- OLE DB error handling, SQL Server message results
author: pmasl
ms.author: Pedro.Lopes
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 08c47b78d764e62d3e13f55b8a9aa1081d234782
ms.sourcegitcommit: 9351e8b7b68f599a95fb8e76930ab886db737e5f
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/06/2018
---
# <a name="sql-server-message-results"></a>Resultados de los mensajes de SQL Server
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  El siguiente [!INCLUDE[tsql](../../../includes/tsql-md.md)] instrucciones no generan controlador OLE DB para conjuntos de filas de SQL Server o un recuento de filas afectadas cuando se ejecuta:  
  
-   PRINT  
  
-   RAISERROR con una gravedad de 10 o inferior  
  
-   DBCC  
  
-   SET SHOWPLAN  
  
-   SET STATISTICS  
  
 Estas instrucciones devuelven uno o varios mensajes informativos o hacen que [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] devuelva mensajes informativos en lugar de resultados de conjunto de filas o de recuento. En la ejecución correcta, el controlador OLE DB para SQL Server devuelve S_OK y los mensajes están disponibles para el controlador OLE DB para el consumidor de SQL Server.  
  
 El controlador OLE DB para SQL Server devuelve S_OK y tiene uno o más mensajes informativos disponibles después de la ejecución de muchos [!INCLUDE[tsql](../../../includes/tsql-md.md)] instrucciones o la ejecución del consumidor de un controlador de OLE DB para la función de miembro de SQL Server.  
  
 El controlador OLE DB para los consumidores de SQL Server que permite la especificación dinámica de texto de la consulta debe comprobar interfaces de error después de cada ejecución de la función miembro independientemente del valor de código de retorno, la presencia o ausencia de un devuelto **IRowset** o **IMultipleResults** referencia de la interfaz o un recuento de filas afectadas.  
  
## <a name="see-also"></a>Vea también  
 [Errores](../../oledb/ole-db-errors/errors.md)  
  
  
