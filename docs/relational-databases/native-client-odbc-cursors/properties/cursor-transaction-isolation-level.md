---
title: Nivel de aislamiento de transacción de cursor | Documentos de Microsoft
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.suite: sql
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- isolation levels [ODBC]
- ODBC applications, row versioning
- cursors [ODBC], isolation levels
- ODBC cursors, isolation levels
- row versioning [SQL Server], ODBC
ms.assetid: 0c6663a4-5a25-44aa-8fe4-e35af9bf4a83
caps.latest.revision: 32
author: MightyPen
ms.author: genemi
manager: craigg
monikerRange: '>= aps-pdw-2016 || = azuresqldb-current || = azure-sqldw-latest || >= sql-server-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: 9433f3657d9db6f878ed6ce295d200325b3f3e14
ms.sourcegitcommit: a78fa85609a82e905de9db8b75d2e83257831ad9
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/18/2018
ms.locfileid: "35696246"
---
# <a name="cursor-transaction-isolation-level"></a>Nivel de aislamiento de las transacciones de cursores
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../../includes/snac-deprecated.md)]

  El comportamiento de bloqueo completo de cursores se basa en una interacción entre los atributos de simultaneidad y el nivel de aislamiento de transacciones establecido por el cliente. Los clientes ODBC establecen la transacción nivel de aislamiento mediante el [SQLSetConnectAttr](../../../relational-databases/native-client-odbc-api/sqlsetconnectattr.md) atributos SQL_ATTR_TXN_ISOLATION o SQL_COPT_SS_TXN_ISOLATION. El comportamiento del bloqueo de un entorno de cursor específico se determina mediante la combinación de los comportamientos de bloqueo de las opciones de simultaneidad y de nivel de aislamiento de transacción.  
  
 Se admiten los siguientes niveles de aislamiento de transacción de cursor por la [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] controlador ODBC Native Client:  
  
-   Lectura confirmada (SQL_TXN_READ_COMMITTED)  
  
-   Lectura no confirmada (SQL_TXN_READ_UNCOMMITTED)  
  
-   Lectura repetible (SQL_TXN_REPEATABLE_READ)  
  
-   Serializable (SQL_TXN_SERIALIZABLE)  
  
-   Instantánea (SQL_TXN_SS_SNAPSHOT)  
  
 Tenga en cuenta que la API de ODBC especifica niveles de aislamiento de transacción adicionales, pero estos no son compatibles con [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] o [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] controlador ODBC Native Client.  
  
## <a name="see-also"></a>Vea también  
 [Propiedades de cursor](../../../relational-databases/native-client-odbc-cursors/properties/cursor-properties.md)  
  
  
