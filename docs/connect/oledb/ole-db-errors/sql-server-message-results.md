---
title: Resultados del mensaje de SQL Server | Documentos de Microsoft
description: resultados de los mensajes de SQL Server
ms.custom: ''
ms.date: 06/14/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.component: oledb|ole-db-errors
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- OLE DB Driver for SQL Server, errors
- errors [OLE DB], SQL Server message results
- OLE DB error handling, SQL Server message results
author: pmasl
ms.author: Pedro.Lopes
manager: craigg
ms.openlocfilehash: 87dbfd1740223f6d3d2116ada8d8c0c109aba15f
ms.sourcegitcommit: e1bc8c486680e6d6929c0f5885d97d013a537149
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/15/2018
ms.locfileid: "35665521"
---
# <a name="sql-server-message-results"></a>Resultados de los mensajes de SQL Server
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-asdbmi-md](../../../includes/appliesto-ss-asdb-asdw-pdw-asdbmi-md.md)]

[!INCLUDE[Driver_OLEDB_Download](../../../includes/driver_oledb_download.md)]

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
  
  
