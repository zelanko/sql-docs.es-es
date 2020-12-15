---
description: Nivel de aislamiento de las transacciones de cursores
title: Nivel de aislamiento de transacción de cursor | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
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
author: markingmyname
ms.author: maghan
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 475ad9fd8965cd74cb46691117df05815d0d2e84
ms.sourcegitcommit: 1a544cf4dd2720b124c3697d1e62ae7741db757c
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 12/14/2020
ms.locfileid: "97473706"
---
# <a name="cursor-transaction-isolation-level"></a>Nivel de aislamiento de las transacciones de cursores
[!INCLUDE [SQL Server](../../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]

  El comportamiento de bloqueo completo de cursores se basa en una interacción entre los atributos de simultaneidad y el nivel de aislamiento de transacciones establecido por el cliente. Los clientes ODBC establecen el nivel de aislamiento de transacción mediante los atributos [SQLSetConnectAttr](../../../relational-databases/native-client-odbc-api/sqlsetconnectattr.md) SQL_ATTR_TXN_ISOLATION o SQL_COPT_SS_TXN_ISOLATION. El comportamiento del bloqueo de un entorno de cursor específico se determina mediante la combinación de los comportamientos de bloqueo de las opciones de simultaneidad y de nivel de aislamiento de transacción.  
  
 El controlador ODBC de Native Client admite los siguientes niveles de aislamiento de transacción de cursor [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] :  
  
-   Lectura confirmada (SQL_TXN_READ_COMMITTED)  
  
-   Lectura no confirmada (SQL_TXN_READ_UNCOMMITTED)  
  
-   Lectura repetible (SQL_TXN_REPEATABLE_READ)  
  
-   Serializable (SQL_TXN_SERIALIZABLE)  
  
-   Instantánea (SQL_TXN_SS_SNAPSHOT)  
  
 Tenga en cuenta que la API de ODBC especifica niveles de aislamiento de transacción adicionales, pero no es compatible con [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] ni con el [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] controlador ODBC de Native Client.  
  
## <a name="see-also"></a>Consulte también  
 [Propiedades de cursor](../../../relational-databases/native-client-odbc-cursors/properties/cursor-properties.md)  
  
  
