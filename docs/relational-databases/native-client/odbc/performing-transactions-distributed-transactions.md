---
title: Crear transacciones distribuidas | Microsoft Docs
description: Las aplicaciones pueden usar MSDTC para extender o distribuir una transacción en varias instancias de SQL Server. Una clase .NET también puede distribuir una transacción.
ms.custom: ''
ms.date: 05/13/2019
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- MS DTC, performing distributed transactions
- SQL Server Native Client ODBC driver, transactions
- distributed transactions [ODBC]
- transactions [ODBC]
- ODBC, transactions
ms.assetid: 2c17fba0-7a3c-453c-91b7-f801e7b39ccb
author: markingmyname
ms.author: maghan
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: e5ace381694dcc3afdbed36e35e48af147067b32
ms.sourcegitcommit: a5398f107599102af7c8cda815d8e5e9a367ce7e
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/13/2020
ms.locfileid: "92005972"
---
# <a name="create-a-distributed-transaction"></a>Crear una transacción distribuida

[!INCLUDE [SQL Server](../../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]

<!--
The following includes .md file is Empty, as of long before 2019/May/13.
/includes/snac-deprecated.md
-->


Se puede crear una transacción distribuida para diferentes sistemas de Microsoft SQL de diferentes maneras.

## <a name="odbc-driver-calls-the-msdtc-for-sql-server-on-premises"></a>El controlador ODBC llama a MSDTC para SQL Server local

Microsoft Coordinador de transacciones distribuidas (MSDTC) permite a las aplicaciones extender o _distribuir_ una transacción en dos o más instancias de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] . La transacción distribuida funciona incluso cuando las dos instancias se hospedan en equipos independientes.

MSDTC se instala para Microsoft SQL Server local, pero no está disponible para el servicio en la nube Azure SQL Database de Microsoft.

El controlador de SQL Server Native Client llama a MSDTC para conectividad abierta de bases de datos (ODBC), cuando el programa de C++ administra una transacción distribuida. El controlador ODBC de Native Client tiene un administrador de transacciones que es compatible con el estándar XA de Open Group Distributed Transaction Processing (DTP). MSDTC requiere este cumplimiento. Normalmente, todos los comandos de administración de transacciones se envían a través de este controlador ODBC de Native Client. La secuencia es la siguiente:

1. La aplicación ODBC de C++ Native Client inicia una transacción mediante una llamada a [SQLSetConnectAttr](../../../relational-databases/native-client-odbc-api/sqlsetconnectattr.md), con el modo de confirmación automática desactivado.

2. La aplicación actualiza algunos datos en SQL Server X en el equipo A.

3. La aplicación actualiza algunos datos en SQL Server Y en el equipo B.
    - Si se produce un error en una actualización en SQL Server Y, se revierten todas las actualizaciones no confirmadas en ambas instancias de SQL Server.

4. Por último, la aplicación finaliza la transacción mediante una llamada a [SQLEndTran _(1)_](../../../relational-databases/native-client-odbc-api/sqlendtran.md), con la opción SQL_COMMIT o SQL_ROLLBACK.

_(1)_ MSDTC se puede invocar sin ODBC. En tal caso, MSDTC se convierte en el administrador de transacciones y la aplicación ya no usa **SQLEndTran**.

### <a name="only-one-distributed-transaction"></a>Solo una transacción distribuida

Supongamos que la aplicación ODBC de C++ Native Client se ha dado de alta en una transacción distribuida. Después, la aplicación se da de alta en una segunda transacción distribuida. En este caso, el [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] controlador ODBC de Native Client deja la transacción distribuida original y se da de alta en la nueva transacción distribuida.

Para obtener más información, vea [Referencia del programador de DTC](/previous-versions/windows/desktop/ms686108(v=vs.85)).

## <a name="c-alternative-for-sql-database-in-the-cloud"></a>Alternativa de C# para SQL Database en la nube

MSDTC no es compatible con Azure SQL Database o Azure Synapse Analytics.

Sin embargo, se puede crear una transacción distribuida para SQL Database haciendo que el programa de C# use la clase .NET [System. Transactions. TransactionScope](/dotnet/api/system.transactions.transactionscope).

### <a name="other-programming-languages"></a>Otros lenguajes de programación

Los siguientes lenguajes de programación podrían no proporcionar compatibilidad con las transacciones distribuidas con el servicio de SQL Database:

- C++ nativo que usa controladores ODBC
- Servidor vinculado mediante Transact-SQL
- Controladores JDBC

## <a name="see-also"></a>Vea también

[Realizar transacciones (ODBC)](performing-transactions-in-odbc.md)