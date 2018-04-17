---
title: Resultados del mensaje de SQL Server | Documentos de Microsoft
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: ''
ms.component: native-client-ole-db-errors
ms.reviewer: ''
ms.suite: sql
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- SQL Server Native Client OLE DB provider, errors
- errors [OLE DB], SQL Server message results
- OLE DB error handling, SQL Server message results
ms.assetid: 6663c6f9-def1-4d9e-845b-2085e5efc401
caps.latest.revision: 29
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
monikerRange: '>= aps-pdw-2016 || = azuresqldb-current || = azure-sqldw-latest || >= sql-server-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: 649db2722e27b5d9639078f23a568d03a30fde1a
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/16/2018
---
# <a name="sql-server-message-results"></a>Resultados de los mensajes de SQL Server
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../includes/snac-deprecated.md)]

  El siguiente [!INCLUDE[tsql](../../includes/tsql-md.md)] instrucciones no generar [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] conjuntos de filas de proveedor OLE DB de Native Client o un recuento de filas afectadas al ejecutarse:  
  
-   PRINT  
  
-   RAISERROR con una gravedad de 10 o inferior  
  
-   DBCC  
  
-   SET SHOWPLAN  
  
-   SET STATISTICS  
  
 Estas instrucciones devuelven uno o varios mensajes informativos o hacen que [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] devuelva mensajes informativos en lugar de resultados de conjunto de filas o de recuento. En la ejecución correcta, el [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] proveedor OLE DB de Native Client devuelve S_OK y los mensajes están disponibles para el [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] consumidor del proveedor OLE DB de Native Client.  
  
 El [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] proveedor OLE DB de Native Client devuelve S_OK y tiene uno o más mensajes informativos disponibles después de la ejecución de muchos [!INCLUDE[tsql](../../includes/tsql-md.md)] instrucciones o la ejecución del consumidor de un [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] función de miembro de proveedor OLE DB de Native Client.  
  
 El [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] consumidor del proveedor OLE DB de Native Client que permite la especificación dinámica de texto de la consulta debe comprobar interfaces de error después de cada ejecución de la función miembro independientemente del valor de código de retorno, la presencia o ausencia de un devuelto **IRowset** o **IMultipleResults** referencia de la interfaz o un recuento de filas afectadas.  
  
## <a name="see-also"></a>Vea también  
 [Errores](../../relational-databases/native-client-ole-db-errors/errors.md)  
  
  
