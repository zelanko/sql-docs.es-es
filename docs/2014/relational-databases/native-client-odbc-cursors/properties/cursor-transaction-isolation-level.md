---
title: Nivel de aislamiento de transacción de cursor | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology: native-client
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- isolation levels [ODBC]
- ODBC applications, row versioning
- cursors [ODBC], isolation levels
- ODBC cursors, isolation levels
- row versioning [SQL Server], ODBC
ms.assetid: 0c6663a4-5a25-44aa-8fe4-e35af9bf4a83
caps.latest.revision: 31
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 045ad6a09adc3ff4127c04c4dae4281dd413c5b8
ms.sourcegitcommit: f8ce92a2f935616339965d140e00298b1f8355d7
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/03/2018
ms.locfileid: "37430894"
---
# <a name="cursor-transaction-isolation-level"></a>Nivel de aislamiento de las transacciones de cursores
  El comportamiento de bloqueo completo de cursores se basa en una interacción entre los atributos de simultaneidad y el nivel de aislamiento de transacciones establecido por el cliente. Los clientes ODBC establecen la transacción nivel de aislamiento mediante el [SQLSetConnectAttr](../../native-client-odbc-api/sqlsetconnectattr.md) atributos SQL_ATTR_TXN_ISOLATION o SQL_COPT_SS_TXN_ISOLATION. El comportamiento del bloqueo de un entorno de cursor específico se determina mediante la combinación de los comportamientos de bloqueo de las opciones de simultaneidad y de nivel de aislamiento de transacción.  
  
 Se admiten los siguientes niveles de aislamiento de transacción de cursor por la [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] controlador ODBC de Native Client:  
  
-   Lectura confirmada (SQL_TXN_READ_COMMITTED)  
  
-   Lectura no confirmada (SQL_TXN_READ_UNCOMMITTED)  
  
-   Lectura repetible (SQL_TXN_REPEATABLE_READ)  
  
-   Serializable (SQL_TXN_SERIALIZABLE)  
  
-   Instantánea (SQL_TXN_SS_SNAPSHOT)  
  
 Tenga en cuenta que la API de ODBC especifica niveles de aislamiento de transacción adicionales, pero no son compatibles con [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] o [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] controlador ODBC de Native Client.  
  
## <a name="see-also"></a>Vea también  
 [Propiedades de cursor](cursor-properties.md)  
  
  
