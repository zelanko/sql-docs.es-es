---
title: Resultados de mensajes de SQL Server | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- SQL Server Native Client OLE DB provider, errors
- errors [OLE DB], SQL Server message results
- OLE DB error handling, SQL Server message results
ms.assetid: 6663c6f9-def1-4d9e-845b-2085e5efc401
author: markingmyname
ms.author: maghan
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 577b609fd2f878e6c97010cac004e0b10b3a4e4e
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/27/2020
ms.locfileid: "81300985"
---
# <a name="sql-server-message-results"></a>Resultados de los mensajes de SQL Server
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  Las instrucciones [!INCLUDE[tsql](../../includes/tsql-md.md)] siguientes no generan [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] conjuntos de filas de proveedor de OLE DB de cliente nativo ni un recuento de las filas afectadas cuando se ejecutan:  
  
-   PRINT  
  
-   RAISERROR con una gravedad de 10 o inferior  
  
-   DBCC  
  
-   SET SHOWPLAN  
  
-   SET STATISTICS  
  
 Estas instrucciones devuelven uno o varios mensajes informativos o hacen que [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] devuelva mensajes informativos en lugar de resultados de conjunto de filas o de recuento. Al ejecutarse correctamente, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] el proveedor de OLE DB de Native client Devuelve S_OK y los mensajes están disponibles [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para el consumidor del proveedor de OLE DB de Native Client.  
  
 El [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] proveedor de OLE DB de Native Client Devuelve S_OK y tiene uno o más mensajes informativos disponibles después de [!INCLUDE[tsql](../../includes/tsql-md.md)] la ejecución de muchas instrucciones o la [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ejecución del consumidor de una función miembro de proveedor de OLE DB de Native Client.  
  
 El [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] consumidor del proveedor de OLE DB de Native Client que permite la especificación dinámica del texto de la consulta debe comprobar las interfaces de error después de cada ejecución de función miembro independientemente del valor del código de retorno, la presencia o ausencia de una referencia de interfaz **IRowset** o **IMultipleResults** devuelta, o un recuento de filas afectadas.  
  
## <a name="see-also"></a>Consulte también  
 [Errors](../../relational-databases/native-client-ole-db-errors/errors.md)  
  
  
