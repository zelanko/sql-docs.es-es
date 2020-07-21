---
title: Nivel de aislamiento de transacción de cursor | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- isolation levels [ODBC]
- ODBC applications, row versioning
- cursors [ODBC], isolation levels
- ODBC cursors, isolation levels
- row versioning [SQL Server], ODBC
ms.assetid: 0c6663a4-5a25-44aa-8fe4-e35af9bf4a83
author: rothja
ms.author: jroth
ms.openlocfilehash: 30f3dc8a9136a7cbe1d5897cb0bcc9fff8c35ab2
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/18/2020
ms.locfileid: "85020677"
---
# <a name="cursor-transaction-isolation-level"></a>Nivel de aislamiento de las transacciones de cursores
  El comportamiento de bloqueo completo de cursores se basa en una interacción entre los atributos de simultaneidad y el nivel de aislamiento de transacciones establecido por el cliente. Los clientes ODBC establecen el nivel de aislamiento de transacción mediante los atributos [SQLSetConnectAttr](../../native-client-odbc-api/sqlsetconnectattr.md) SQL_ATTR_TXN_ISOLATION o SQL_COPT_SS_TXN_ISOLATION. El comportamiento del bloqueo de un entorno de cursor específico se determina mediante la combinación de los comportamientos de bloqueo de las opciones de simultaneidad y de nivel de aislamiento de transacción.  
  
 El controlador ODBC de Native Client admite los siguientes niveles de aislamiento de transacción de cursor [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] :  
  
-   Lectura confirmada (SQL_TXN_READ_COMMITTED)  
  
-   Lectura no confirmada (SQL_TXN_READ_UNCOMMITTED)  
  
-   Lectura repetible (SQL_TXN_REPEATABLE_READ)  
  
-   Serializable (SQL_TXN_SERIALIZABLE)  
  
-   Instantánea (SQL_TXN_SS_SNAPSHOT)  
  
 Tenga en cuenta que la API de ODBC especifica niveles de aislamiento de transacción adicionales, pero no es compatible con [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] ni con el [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] controlador ODBC de Native Client.  
  
## <a name="see-also"></a>Consulte también  
 [Propiedades de cursor](cursor-properties.md)  
  
  
