---
title: Resultados del mensaje de SQL Server | Microsoft Docs
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
author: MightyPen
ms.author: genemi
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 3383dcd08ed5910d949608e521b3cd23f37aace8
ms.sourcegitcommit: 856e42f7d5125d094fa84390bc43048808276b57
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/07/2019
ms.locfileid: "73790155"
---
# <a name="sql-server-message-results"></a>Resultados de los mensajes de SQL Server
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  Las instrucciones [!INCLUDE[tsql](../../includes/tsql-md.md)] siguientes no generan [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] conjuntos de filas de proveedor de OLE DB de Native Client o un recuento de filas afectadas cuando se ejecutan:  
  
-   PRINT  
  
-   RAISERROR con una gravedad de 10 o inferior  
  
-   DBCC  
  
-   SET SHOWPLAN  
  
-   SET STATISTICS  
  
 Estas instrucciones devuelven uno o varios mensajes informativos o hacen que [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] devuelva mensajes informativos en lugar de resultados de conjunto de filas o de recuento. Al ejecutarse correctamente, el proveedor de OLE DB de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client Devuelve S_OK y los mensajes están disponibles para el consumidor de proveedores OLE DB de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client.  
  
 El proveedor de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] de OLE DB Native Client Devuelve S_OK y tiene uno o más mensajes informativos disponibles después de la ejecución de muchas instrucciones de [!INCLUDE[tsql](../../includes/tsql-md.md)] o la ejecución del consumidor de una [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] función miembro de proveedor OLE DB de Native Client.  
  
 El consumidor del proveedor de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB que permite la especificación dinámica del texto de la consulta debe comprobar las interfaces de error después de cada ejecución de función miembro independientemente del valor del código de retorno, la presencia o ausencia de un IRowset devueltoo una referencia de la interfaz **IMultipleResults** , o un recuento de las filas afectadas.  
  
## <a name="see-also"></a>Vea también  
 [Errores](../../relational-databases/native-client-ole-db-errors/errors.md)  
  
  
